---
layout: post
title: "Creating and using Postgres MCP with Codex"
date: 2026-02-12
thumbnail: /images/stable-diffusion.png
featureImage: /images/stable-diffusion.png
featureImageAlt: "Stable Diffusion rings"
tags: ["ai", "codex", "Fedora", "Linux"]
categories: ["ai"]
draft: false
---

# Creating and Using MCP Postgres

If you are using Codex and a Postgres database, adding a Postgres MCP server gives the agent direct DB tooling for schema inspection, query support, and migration verification.

This guide shows how to install it, start it, and stop it.

## Why Use Postgres MCP

- Lets Codex use DB tools directly instead of guessing from source files.
- Speeds up debugging and migration checks.
- Helps verify real database state during task execution.

## Prerequisites

- `codex` CLI installed and authenticated.
- Node.js and `npx` available.
- A running Postgres instance.

For Docker-based Postgres, make sure the container is up and port-mapped:

```bash
docker ps --format 'table {{.Names}}\t{{.Ports}}\t{{.Status}}'
```

## 1) Install and Register Postgres MCP in Codex

For a Docker Postgres exposed on localhost:

```bash
codex mcp add postgres-wotw -- \
  npx -y @modelcontextprotocol/server-postgres \
  'postgresql://wotw:wotw_dev_password@localhost:5432/wotw'
```

This writes a global MCP server config into `~/.codex/config.toml`.

## 2) Verify It Is Registered

```bash
codex mcp list
codex mcp get postgres-wotw --json
```

You should see the server with `Status: enabled`.

## 3) Start It

You have two ways to start MCP Postgres.

### Option A: Codex-managed (recommended)

Once registered with `codex mcp add`, Codex starts it automatically for sessions that use MCP tools.

Run your normal Codex flow:

```bash
codex exec "inspect database schema"
```

### Option B: Manual start (debug mode)

```bash
npx -y @modelcontextprotocol/server-postgres \
  'postgresql://wotw:wotw_dev_password@localhost:5432/wotw'
```

This runs as a long-lived stdio process.

## 4) Stop It

### Stop manual debug run

Press `Ctrl+C` in that terminal.

### Stop Codex from using it permanently

Remove the MCP server config:

```bash
codex mcp remove postgres-wotw
```

## 5) Common Docker Connectivity Notes

- If MCP runs on your host, use `localhost:5432` (or your mapped port).
- If MCP runs in another container, use Docker network hostnames (for example `wotw-db:5432`), not `localhost`.
- Verify DB access separately when debugging:

```bash
docker exec -i wotw-db psql -U wotw -d wotw -c "select now();"
```

## Security Note

If you pass a full DB URL in args, credentials are stored in config.
For stronger hygiene, use environment variables or a wrapper script so secrets are not embedded directly in command arguments.
