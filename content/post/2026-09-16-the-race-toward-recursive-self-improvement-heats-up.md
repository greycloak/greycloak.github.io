---
title: China's open-source labs are racing toward self-improving AI
date: '2026-09-16'
description: A Chinese lab and a ByteDance-backed research team both moved on recursive self-improvement this week, undercutting the case for a coordinated AI slowdown.
tags:
- recursive-self-improvement
- ai-safety
- open-source
- china
- model-training
categories:
- ai
draft: false
thumbnail: /images/stable-diffusion.png
featureImage: /images/stable-diffusion.png
featureImageAlt: Stable Diffusion rings
---

Any company betting its roadmap on an AI slowdown should reconsider the timeline. The pacing proposals dominating the industry conversation this month all assume the major labs can coordinate to slow the release of ever-more-capable models. That assumption weakens the moment a lab outside that circle announces it is building the exact capability the slowdown is meant to contain. This week, one did, and the practical takeaway for planning is that a regulatory or voluntary pause is unlikely to actually stop the technology from advancing.

## What ZAI and ByteDance actually announced

It was reported that ZAI, a Chinese open-source model company, plans to raise $5 billion, split between new stock issuance and convertible bonds. Around 60% of the proceeds are earmarked for training its next generation of models, and that spend explicitly includes building what the company described as a fully self-training loop. As reported, this is the first time a Chinese lab has openly declared it intends to pursue recursive self-improvement, the ability of an AI system to build and refine its successors.

The same week, a group of 33 researchers with backing from ByteDance published a paper titled "The Last AI Built by Humans," laying out a theoretical roadmap toward genuine recursive self-improvement. Their conclusion was more measured than the headline suggests. The method is not there yet. AI can already automate parts of the training process, but at this stage the researchers found no evidence that it can improve on the process itself. So we have one lab committing capital to the goal and a second group of researchers mapping the path while marking clearly how far the destination still is.

## Why recursive self-improvement is the whole debate

Recursive self-improvement, or RSI, is the specific fear underneath nearly every call for a slowdown this month. In his essay arguing that the frontier labs must pace their development, Anthropic's Dario Amodei named the early stages of RSI as one of the two developments that changed his mind. His worry is straightforward: if AI starts building next-generation models faster than people can understand and control them, the systems could outrun our ability to align them. That is the mechanism the pacing proposals, the embedded evaluators, and the talk of government coordination are all designed to slow.

The honest counterweight comes from inside the labs themselves. An OpenAI researcher pushed back plainly, arguing that RSI is not here, that models are not autonomously producing research ideas, and that helping run experiments on the margin is not the same thing. The ByteDance paper lands in roughly the same place. Both the loudest safety warnings and the on-the-ground research agree the capability is on the horizon rather than in production. What changed this week is that a Chinese open-source lab said out loud that it is aiming for it.

## What this does to the coordination story

The pacing plans only work if everyone paces. That was always their weakest joint, and the ZAI announcement drives a wedge straight into it. Chinese frontier models are open-weight, which means their capabilities diffuse quickly and cannot be recalled once released. If US labs slow down while a well-funded competitor races toward a self-training loop and ships the weights, the slowdown buys alignment time for some of the ecosystem and none of the rest.

This is the part of the debate that stays true regardless of where you sit on AI risk. You can believe the extinction rhetoric is overblown and still see that a coordinated pause requires the participation of labs that have shown no interest in participating. Coverage of a possible US-China summit this month framed exactly this problem, with commentators noting that any real pacing agreement would need something the Chinese side would trade for, and that open-weight releases make compliance almost impossible to verify. For a company deciding how much to invest in adapting to a specific model generation, the signal is that the release cadence is not going to ease on its own.

**My take:** Plan as if no slowdown is coming, because the incentives now point against one holding. RSI is worth watching closely as a capability milestone, but this week it is a marketing declaration and an unfinished research roadmap, not a shipped feature, so I would not let the term drive near-term architecture decisions. The durable lesson is the diffusion dynamic: open-weight models mean capabilities spread on their own timeline, and building your systems to swap models cleanly matters far more than betting on any pause in the pace.
