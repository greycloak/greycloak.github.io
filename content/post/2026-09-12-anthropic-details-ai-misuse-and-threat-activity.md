---
title: What Anthropic's Misuse Report Reveals About Providers
date: '2026-09-12'
description: Anthropic's threat report shows distillation attacks, competitors relaying user traffic to Claude, and a blocked bioweapon grant, and what it means for API buyers.
tags:
- ai-security
- model-providers
- distillation
- threat-intelligence
- data-governance
categories:
- ai
draft: false
thumbnail: /images/stable-diffusion.png
featureImage: /images/stable-diffusion.png
featureImageAlt: Stable Diffusion rings
---

If you run workloads on a third-party model API, you are also inheriting that provider's enforcement decisions and its threat surface. A report from Anthropic this week makes both concrete, and it is worth reading for anyone weighing where to route sensitive data or how much to trust an intermediary in the chain. The company documented distillation attacks, competitors quietly relaying user traffic to Claude, and a blocked grant application that sought to make a mosquito-borne virus more dangerous. These are described as the most notable cases the company has found, not the typical ones, but they map the kinds of abuse any large provider now has to police.

## Competitors mining and relaying traffic

Anthropic said it disrupted distillation attacks tied to Alibaba, DeepSeek, and Xiaomi. Each reportedly used networks of fraudulent accounts to extract reasoning traces from Anthropic's models for use as training data. Distillation is the practice of training one model on another model's outputs, and doing it at scale through fake accounts is what Anthropic flagged as abuse.

More striking for anyone thinking about data governance: Anthropic reported catching both DeepSeek and Moonshot, the lab behind the Kimi models, routing their own users' requests to Claude and serving Claude's responses back. In one instance, over a ten-day period, Moonshot relayed almost 300,000 customer requests to Anthropic, the vast majority handled by Opus. Based on the report, the aim appears to have been gathering realistic user queries for a distillation pipeline rather than spoofing a more capable model. The consequence is the part that should give buyers pause: Anthropic noted the method exposed sensitive information from Chinese government and corporate users on multiple occasions. If your queries pass through an intermediary, you may not know whose backend actually sees them.

## Dual-use enforcement and its false positives

The report's biology section described a May incident where a classifier blocked work on a grant application. The application discussed gain-of-function research on Chikungunya, a mosquito-borne virus. Anthropic's concern was specific: because Chikungunya circulates naturally, a deliberate release as a weapon would be hard to distinguish from an outbreak. The grant sought to identify enhancing mutations, engineer them into infectious clones, and select for virulence in live animals, keeping the most disease-causing variants each round.

Anthropic acknowledged the same research could have legitimate vaccine applications. What tipped its judgment was that the work was intended for a military research institute, though the report did not name the sponsoring nation. It also noted the prompts continued through gray-market resellers after the original accounts were banned. That detail matters for engineers: enforcement at the account level does not stop a determined actor who can buy access elsewhere. The rest of the report catalogs the expected roster, including Russian actors using Claude for espionage and propaganda, actors from several countries drafting software for conventional weapons, and assorted cyberattacks and financial scams.

## What it tells buyers and builders

Two practical signals come out of this. First, provider-side classifiers are active and will sometimes block legitimate work. The Chikungunya case had a plausible innocent reading and was stopped anyway. If your team does anything in a sensitive domain, plan for false positives and build a path to appeal or escalate rather than assuming clean API access.

Second, the routing findings are a reminder that the model you think you are using is not always the model handling your data. Anthropic's report was almost entirely about misuse of its own Claude tiers, which is a narrow lens by design. The pattern of one provider relaying traffic to another, sometimes exposing sensitive queries, is a supply-chain problem rather than a Claude-specific one. Anyone routing regulated or confidential data through resellers or wrapper services should verify where requests actually terminate.

The disclosure itself is also a data point. Anthropic framed publishing as a responsibility, and voluntary transparency of this kind, arriving during a week when the industry was loudly debating how to police itself, reads as an argument for what safety work should look like in practice.

**My take:** Treat this report as due-diligence material, not PR. If you are building on any hosted model, ask your provider and any intermediary exactly where requests are processed and how misuse enforcement could hit your legitimate workloads, and get those answers before you move sensitive data. The distillation and routing findings are the ones to watch; expect them to shape contract terms and data-residency questions across every model vendor, not just Anthropic.
