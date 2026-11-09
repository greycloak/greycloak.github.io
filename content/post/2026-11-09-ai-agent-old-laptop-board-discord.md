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

## What it looks like

Reservations were where Picoclaw gave up, so this is the test I care about. I wanted lunch or dinner for two at the Roundhouse in Beacon on a Saturday. It checked Tock, found it fully booked, and pointed me to Hudson House River Inn in Cold Spring as the closest match. Here's the rest, trimmed:

{{< chat >}}
{{< say me >}}
If we go to Cold Spring, what else is there to do there? Can you build me a day trip from Manhattan round trip by train?
{{< /say >}}
{{< say agent >}}
Here's a plan for Saturday, Oct 31, by train from Grand Central. Train times come from Metro-North's published schedule for that date.

- 8:56am leave Grand Central, arrive Cold Spring 10:16. Sit on the left side for the river view.
- 10:30–1:30, hike Bull Hill. The Washburn trailhead is about a 15-minute walk from the station.
- 3:00–5:30, Main Street and the river. Antique shops and galleries, then Dockside Park, a lawn on the water facing Storm King. Sunset is around 6.
- 5:30pm, Hudson House River Inn, River Room. The inn is a 2-minute walk from the platform.
- 7:24pm train home, into Grand Central at 8:51.

A Saturday in October is packed in Cold Spring, and Halloween adds trick-or-treaters on Main Street.
{{< /say >}}
{{< say note >}}
I asked to swap dinner for lunch there. It reworked the day around a 1:45 table in the River Room.
{{< /say >}}
{{< say me >}}
Which view is better? Bull Hill short loop or Foundry Preserve? Ideally I'd like to be back by 1p for lunch.
{{< /say >}}
{{< say agent >}}
Bull Hill, and it isn't close. The short loop climbs to open rock ledges looking over the Hudson to Storm King and down toward West Point. The Foundry Preserve is a pleasant walk through woods, but you barely see the river. Being back by 1 is tight on the 8:56 train. Take the 8:31am instead. That puts you on the trail by about 10:05 and back in the village around 12:30.
{{< /say >}}
{{< say me >}}
What are my best options to have a snack before the 1:45 reservation (I made it) and how do I deal with clothes suitable for both hiking and lunch?
{{< /say >}}
{{< say agent >}}
Cold Spring Coffeehouse on Main St. You walk right past it from the train. Grab something to carry and eat it at the overlook. Wear clothes that pass at lunch: trail runners, dark pants with some stretch, a light jacket. Pack a fresh shirt and change in the restroom at Hudson House. Since it's an inn, ask them to hold your bag. Worth a call Friday.
{{< /say >}}
{{< /chat >}}

It offered to book Hudson House at every step. I booked it myself, which is how I want it. We had a great time.

## Why self-host

Self-hosted doesn't mean private, at least not yet. Everything I ask still goes to Anthropic, along with whatever files it reads to answer me. What I own is everything around the model: its memory, the skills it has learned, my notes, my files and the hardware. If Anthropic changes its prices or terms, I can point it at a different model and keep all of that.

Eventually I think local models will be good enough to handle my files without sending them to the cloud, and I'd like to be ready when that happens. I already run a few small ones here for testing.

As a side note, I love my Framework 12 laptop. When I upgraded its mainboard, the original i5 board became the agent's new home, replacing the Pi. The setup also uses Nextcloud for file storage, so a lot of my data is local and accessible to Hermes.

## What it's saved me

**1. Moving our Notion docs to Google Drive.** We already use Google Workspace, so having documents split across two places was just confusing. Hermes moved all our Notion docs and attachments into organized shared drives. Now there's one source of truth next to our email, I can manage sharing and organization easily, and it saves us over $2,500 a year. Anything Notion does that Google Drive can't handle gets built by our [Econify Code Factory](https://www.econify.com/products/econify-charm).

**2. Managing my music.** It put my entire MP3 collection (stored on Nextcloud) into playlists it can play on my Sonos system. On the go, I keep music on my iPhone and play it with an MP3 app (Flacbox). No more paying for Spotify or Pandora.

**3. Watering my plants.** I've got pictures of my 25+ plants in a channel, and I get reminders of when to water each one, plus how often to fertilize and with what.

**4. Keeping an eye out.** It watches for things I'm interested in but tend to forget about, like couples yoga classes or a favorite band coming to town.

**5. Everything else.** It pulls reservations, train times and the weather so I don't have to. It runs the pipeline behind our weekly AI newsletter. It even generates images locally on the CPU. (The thumbnails on this blog were made that way using Z-Image Turbo.)

## What it costs

The mainboard was a sunk cost from my laptop upgrade. The extra RAM and SSD were about $550, and I run it on a $20/month Anthropic plan.

On the other side, it's replaced Notion ($2,500 a year), Pandora ($12 a month) and my iCloud storage, now that my photos are mirrored to Nextcloud. That's roughly $2,650 a year saved against $240 a year spent, so the hardware paid for itself in under three months.

The part I can't put a price on is everything else. It remembers what I forget, it turns a vague idea like a day in Cold Spring into a plan with train times, and it answers the questions I'd never have taken the time to look up. That's the real return.

## Guardrails

Nothing catastrophic has happened, but it does make mistakes, and they tend to be quiet ones. A couple of times it finished a long job and the results never showed up, because the message saying it was done got dropped. Now it posts its own results to Discord. A reboot once silently killed a job I'd scheduled for that night, so scheduled jobs now live in files that survive a restart. And while merging its changes to this blog, it overwrote an edit I'd made to my About page, which we had to restore.

None of that did real damage, but I only found it because I was paying attention. It also has delete access to my Google Drive, and there are a few other places where I'm taking a risk, so I need more guardrails. What has held up best is keeping write access away. My agent drafts, and I send. It doesn't book, buy, post or email as me without my OK, and an OK for one thing isn't an OK for the next. Outside of Google Drive, most of my accounts are connected read-only.

## Is it worth it?

If you've got some spare, always-on hardware around, then definitely. If it can run on an old 4GB Pi 4 with a cloud model and be useful, it can most likely run on whatever you have.

## What I have yet to try

Still pending is improving memory management beyond Obsidian. Maybe Hindsight or something else. I also haven't seen how the personality and effectiveness of my assistant change depending on the backend. Right now it's almost exclusively Anthropic, but I don't know yet how it behaves if I switch to OpenAI or an open model. I'm looking forward to experimenting and getting a handle on all of it but so far I'm much happier in this play space than on Grokbot, Muse, Dots, or Duet.
