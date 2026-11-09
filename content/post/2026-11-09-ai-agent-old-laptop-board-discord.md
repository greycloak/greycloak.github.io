---
title: "I gave an AI agent an old laptop board and a Discord server"
date: 2026-11-09
summary: "My first try at a personal AI agent on a Raspberry Pi was more hassle than it was worth. My second, Hermes on a spare Framework mainboard, now runs my lights, music, plants, newsletter and a lot of my day. Here's how it's set up, what it saves me, and the rules I keep it on."
categories: ["Curiosity & Creation"]
tags: ["AI", "AI agents", "Hermes Agent", "self-hosted", "Framework Laptop", "Discord"]
draft: false
thumbnail: /images/agent-board.png
featureImage: /images/agent-discord-channels.png
featureImageAlt: "My Discord setup: channels down the left, threads in the middle, one thread open on the right"
---

I had previously tried to jump on the AI agent train using Picoclaw on a Raspberry Pi. It was an interesting experience, but it turned out to be hard mode before I was ready for it. After a few failed attempts to get it working with Resy and OpenTable and doing some scouting for me, I decided it was more hassle than it was worth and gave up.

A few months later I gave [Hermes](https://hermes-agent.nousresearch.com) a try and it has been a game changer. I run it on Anthropic's Claude models, with Opus for the channels that matter and Haiku for the lighter ones, and OpenRouter for image generation (Nano Banana) and as a backup in case Anthropic goes down. Hermes is excellent, and if I need something improved I just ask it.

The biggest win for me was using Discord as the main way to talk to it and breaking everything into personal and work channels. I'm able to assign different models to different channels and keep work and personal notes in separate places.

## The channels

**#setup** is where I ask it to build new things. It can now manage my Lutron lights, my Sonos system and music library, install local models for testing, and connect to various MCPs. This is also where I had it move itself from the Pi to a Framework mainboard.

**#work-general** connects to my work MCPs, email, Slack, calendar, Notion and note taker to give me a better view into my day and make sure I'm not forgetting anything.

**#personal-general** helps me organize date ideas, gives me advice on purchases, and handles general personal things.

**#personal-finance** helps me plan for retirement and spot any fraudulent purchases or stale subscriptions.

There are a lot more channels. The beauty is that each channel can use a different model, so something critical like my finances gets Opus while everyday stuff runs on the cheaper Haiku. I even have an experimental channel with a local LLM and image model.

## Why self-host

Eventually I think local models will be capable enough to handle my files without sending them up to the cloud, and I'd like to be ready when that happens. As mentioned, I already run a few small models locally for testing.

As a side note, I love my Framework 12 laptop. When I upgraded its mainboard, the original i5 board became the agent's new home, replacing the Pi. The setup also uses Nextcloud for file storage, so a lot of my data is local and accessible to Hermes.

## What it's saved me

**1. Moving our Notion docs to Google Drive.** We already use Google Workspace, so having documents split across two places was just confusing. Hermes moved all our Notion docs and attachments into organized shared drives. Now there's one source of truth next to our email, I can manage sharing and organization easily, and it saves us over $2,500 a year. Anything Notion does that Google Drive can't handle gets built by our [Econify Code Factory](https://www.econify.com/products/econify-charm).

**2. Managing my music.** It put my entire MP3 collection (stored on Nextcloud) into playlists it can play on my Sonos system. On the go, I keep music on my iPhone and play it with an MP3 app (Flacbox). No more paying for Spotify or Pandora.

**3. Watering my plants.** I've got pictures of my 25+ plants in a channel, and I get reminders of when to water each one, plus how often to fertilize and with what.

**4. Keeping an eye out.** It watches for things I'm interested in but tend to forget about, like couples yoga classes or a favorite band coming to town.

**5. Everything else.** It pulls reservations, train times and the weather so I don't have to. It runs the pipeline behind our weekly AI newsletter. It even generates images locally on the CPU. (The thumbnails on this blog were made that way using Z-Image Turbo.)

## Guardrails

So far, nothing has broken or done anything catastrophic. It does have delete access to my Google Drive and there are a few other areas where I am taking a risk. I'll admit I need to add some more guardrails. But other than that, the important thing is to have trusted sources and keep write access away. My agent drafts, and I send. It doesn't book, buy, post or email as me without my OK, and an OK for one thing isn't an OK for the next. Outside of Google Drive, most of my accounts are connected read-only.


## Is it worth it?

If you've got some spare, always-on hardware around, then definitely. If it can run on an old 4GB Pi 4 with a cloud model and be useful, it can most likely run on whatever you have. You're investing in memory, skills, and habits that you can keep no matter what OpenAI, Anthropic, Google, Meta or any other frontier provider changes underneath you. 

## What I have yet to try

Still pending is improving memory management beyond Obsidian. Maybe Hindsight or something else. I also haven't seen how the personality and effectiveness of my assistant change depending on the backend. Right now it's almost exclusively Anthropic, but I don't know yet how it behaves if I switch to OpenAI or an open model. I'm looking forward to experimenting and getting a handle on all of it but so far I'm much happier in this play space than on Grokbot, Muse, Dots, or Duet.
