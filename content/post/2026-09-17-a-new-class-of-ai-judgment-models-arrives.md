---
title: When to Reach for a Judgment Model Instead of an LLM
date: '2026-09-17'
description: Typesafe's JEV outputs calibrated probabilities for narrow decisions instead of text, changing how teams build routing, checking, and automation.
tags:
- ai-agents
- machine-learning
- automation
- llms
- architecture
categories:
- ai
draft: false
thumbnail: /images/stable-diffusion.png
featureImage: /images/stable-diffusion.png
featureImageAlt: Stable Diffusion rings
---

If you have been wiring an LLM into every classification and routing decision in your product, there is now a reason to reconsider the pattern. A new model called JEV, from a company named Typesafe, is built to answer narrow questions with probabilities rather than prose. The practical consequence is that a check you could previously afford to run only on selected cases, or at the end of a task, becomes cheap and fast enough to run on every incoming request, after every draft, across every candidate document. That changes the economics of self-checking, ticket routing, and agent orchestration, which is where a lot of real automation quietly succeeds or fails.

JEV comes from Diogo Almeida, who is credited as a co-inventor of ChatGPT. The company describes a different training method, which it calls Reinforcement Learning for Calibrated Decisions, and a different objective. Where a chat model is tuned toward responses people prefer to read, JEV is tuned to produce calibrated probabilities: honest confidence numbers you can act on in code.

## What it actually produces

Ask JEV a question like "does this customer sound angry?" and it returns something like 0.9, meaning an estimated 90% probability that the answer is yes. Give it defined categories, and it distributes probability across them: 60% likely furious, 10% likely enraged, and so on. The surrounding software does the rest. An if statement escalates the ticket, a threshold deprioritizes it, a confidence score decides whether a human needs to look.

That sounds small until you see the design pattern it enables. Typesafe's own guidance is to keep control flow, deterministic rules, and side effects in code, break a broad judgment into narrow typed questions, give each question only the context it needs, ask independent questions together, then compose the answers in code. A generative model would choke here. Asked whether a customer is angry, a chatbot might reply, "You're absolutely right, this customer does sound frustrated. Would you like me to draft a response?" That is an essay where your program expected a number, and it crashes the workflow. JEV is built to hand back the number.

The reported performance is what makes the pattern viable. The company claims JEV runs 20 to 200 times faster and 40 to 400 times cheaper than LLMs, with output tokens free. In one demonstration, a writer fed the model 27 of his own articles alongside 10 deliberately AI-styled counterpoints, then ran 21 questions across all 37 documents to check for tells like repeating an idea without evidence or forcing a both-sides symmetry. He reported 777 judgments returned in under 0.7 seconds for an estimated quarter of a cent. At that price, checking everything anyone in a company has ever written stops being a thought experiment.

## Where it fits in a stack

The useful framing is JEV alongside the LLM. A common shape people are describing: the LLM proposes options, JEV decides, code executes. A support flow can ask several questions at once (is this a product problem, does the message show repeated failed contact, is a deadline near, which team should own it), combine those signals with the actual account record, and escalate. You still have a generative model draft the reply. Then JEV checks that draft against narrow criteria: does it acknowledge the repeated contacts, does it address the stated problem, does it promise anything the source data does not support.

Think of it as a linter for knowledge work. A code linter flags syntax errors and bad patterns almost instantly; a cheap judgment model can flag unsupported claims, missed requirements, and style violations at the same speed. Give a coding agent access to JEV and a list of things to avoid, and it can check its own output before shipping.

## The honest caveat

This is not a replacement for LLMs, and it does not pretend to be. A judgment model produces no text, so it is an incomplete category by definition and only works as part of a larger model stack. There is also a sharper way to read what is happening here. Many of the problems teams now throw at LLMs are classic classification or regression tasks that classical machine learning already handles well, sometimes better. The trouble was that classical ML meant labeling data, training a model, and hosting it, which most teams never invested in. One reasonable reading of JEV is a friendlier interface onto that older, well-understood territory, minus the setup cost.

**My take:** Treat this as a real architectural option, not a new chatbot. If you have LLM calls doing yes/no routing, scoring, or draft-checking, those are the first candidates to move behind a judgment model, and the payoff is running checks on everything instead of a sample. It is one model, one day old, from a two-year-old effort, so build the seam cleanly and keep the LLM in the loop for anything that has to generate. Watch whether the calibration holds up on your data before you let a probability trigger an irreversible action.
