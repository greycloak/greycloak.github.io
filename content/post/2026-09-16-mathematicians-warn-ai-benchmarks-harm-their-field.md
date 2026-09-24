---
title: When AI Solves the Problem but Skips the Understanding
date: '2026-09-16'
description: Fields Medalists warn that using famous math problems as AI benchmarks erodes the understanding expert work is meant to produce. What it means for deploying AI.
tags:
- ai
- knowledge-work
- automation
- expertise
- research
categories:
- ai
draft: false
thumbnail: /images/stable-diffusion.png
featureImage: /images/stable-diffusion.png
featureImageAlt: Stable Diffusion rings
---

If your organization is deploying AI to produce the output of expert work, a letter published this week by some of the world's most accomplished mathematicians names a cost that won't show up on next quarter's productivity dashboard: the erosion of the judgment that made the work valuable in the first place. The argument is narrow on its surface and much broader underneath, and it's worth reading before you sign off on the next automation project aimed at your senior people.

Terence Tao led a group of 25 Fields Medalists in signing an open letter titled "A Severe Misalignment of AI in Mathematics." The trigger was a run of results reported over recent weeks. OpenAI was said to have solved a millennium prize problem and claimed progress on a second, and Anthropic was rumored to have solved yet another, raising the prospect that three of the six outstanding problems could fall this year. These are problems that have stood for decades. One of the researchers who had been working on a problem using AI tools, NYU's Tristan Buckmaster, questioned whether OpenAI could have accessed his logs to reach the result first. OpenAI denied it. The specifics matter less than the reaction they provoked.

## What the letter actually argues

The misalignment the mathematicians point to falls between the goals of AI companies and the goals of the field they're entering, a different thing from the science-fiction fear about AI and humanity. Companies treat solving famous problems as a benchmark, a scoreboard entry. Mathematicians treat those problems as landmarks. As the letter puts it, solving one has historically been a sign of new insight and new methods, which then get studied, discussed, and simplified by a community over years, sometimes centuries, until the ideas become tools the wider world can use.

The core line is the one to sit with: solving problems is only a proxy for the real goal, which is conceptual understanding. Forget that, the signatories argue, and you can turn the tool against the purpose. Producing true statements faster and faster could bury the ground that new ideas grow from rather than cultivate it. Their worry extends to training. Years of grappling with hard problems is how people learn to formulate the next question, not just answer the current one. If AI produces the answer directly, that training loop breaks.

This isn't reflexive resistance. Tao himself was a slow convert, skeptical of AI-assisted mathematics until recently, and now uses the tools in his own process. The mathematician Stephen Strogatz, who is 67 and near retirement, described getting choked up while explaining to a reporter the 4,000-year tradition he feels part of. His point was not job loss. It was that rapid change carries real loss even when the change also brings good things.

## The pattern beyond mathematics

The signatories were explicit that they see their field as an early case, not a special one. Mathematics happens to be exposed sooner than most, because so much of its work can be expressed as a clean problem with a checkable answer. The same structure sits underneath a lot of professional work: a body of prior human effort, years of training, and a final output that increasingly a model can generate on its own. When that happens, the letter argues, the output and the understanding that used to come bundled with it come apart.

That separation is the operational risk for any company automating knowledge work. You can capture the deliverable and quietly lose the capability that produced good deliverables. The junior analyst who never builds the model by hand doesn't develop the instinct to know when a model is wrong. The reviewer who only ever reviews AI output loses the feel for what a hard problem actually requires. None of this shows up in a velocity metric. It shows up two or three years later as a team that ships fast and can no longer tell when it's shipping something broken.

## What this means for deploying AI on expert work

The practical move is to be deliberate about which parts of a workflow you automate for output and which you preserve for learning. Automating a genuine bottleneck is different from automating the part where your people build judgment. On real client engagements, we treat that distinction as a design decision, not an afterthought: the AI handles the volume, and humans stay in the loop on the reasoning that has to survive past this quarter. The goal is a team that can still evaluate what the machine produces after a year of the machine producing most of it.

**My take:** Read the letter, and don't dismiss it as guild self-interest, because the underlying mechanism applies directly to how you staff and train around AI. When you automate expert work, decide on purpose whether you're removing drudgery or removing the path by which people learn to judge the output, and keep humans doing the reasoning on enough of the work that your team retains the ability to catch a confident, wrong answer. Watch for capability decay the way you'd watch for technical debt: it accrues silently and gets expensive to unwind.
