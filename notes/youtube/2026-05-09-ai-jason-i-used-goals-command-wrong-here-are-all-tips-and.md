---
title: "What /goal Actually Fixes (and Where It Breaks)"
source_url: https://www.youtube.com/watch?v=rIs802-bXDY
channel: AI Jason
video_title: "I used /goals command wrong... Here are all tips & mistakes"
captured: 2026-05-09
tags: [ai-agents, coding-agents, agent-design, prompting]
---

# What /goal Actually Fixes (and Where It Breaks)

**Source:** [AI Jason — "I used /goals command wrong... Here are all tips & mistakes"](https://www.youtube.com/watch?v=rIs802-bXDY)

A walkthrough of OpenAI Codex's `/goal` feature (and Hermes' near-identical "persistent goal" mode): the failure mode it exists to contain, how it's wired under the hood, how to prompt it well, and the harder class of long-horizon goal it can't yet handle.

## The problem it's solving

Long-running coding agents have a laziness problem: as a task grows, an agent's internal "I'm done" heuristic gets cheaper than continuing, so it declares victory early — not because the work is finished. `/goal` is a containment device for that specific failure, not a general productivity feature. It's the next step after the "rough loop" pattern (running an agent in a while-loop with a hard iteration cap): instead of a dumb counter, the stop condition becomes an LLM judge, which lets the loop handle ambiguous goals you can't pre-enumerate steps for.

Two vendors shipping the same primitive around the same time — Codex's `/goal` and Hermes' persistent-goal mode — is a signal this is becoming a category, not one company's feature.

## How it works

The loop: the agent works → a judge call evaluates whether the goal is satisfied → if not, the agent is re-triggered with a continuation prompt that re-injects the goal plus the accumulated state (not a repeat of the original prompt — that would lose progress).

The two implementations diverge in a way that matters:
- **Codex** has the agent mark its own goal complete — cheaper, but trust-dependent, since the same agent prone to declaring victory early is also judging itself. The workaround is an explicit instruction in the continuation prompt: don't accept a proxy signal as completion, only mark done when an audit shows the objective was actually achieved.
- **Hermes** uses a separate, larger judge model to evaluate completion — a token tax, but harder for the working agent to game.

The judge is fed the definition of done, the expected output format, the goal, and the agent's latest response, and returns a status plus reasoning — the reasoning is what gets folded into the next continuation prompt, so a weak judge produces weak follow-up prompts.

## Setting it up

`/goal` ships behind an experimental flag: `codex features list` to see what's gated, `codex features enable goal` to turn it on, then `/goal <prompt>` inside a session. Re-running `/goal` mid-flight reports runtime and token usage — the main way to monitor a multi-hour run you can't tail in real time. `goal pause` and `goal clear` are the only controls; there's no partial undo once a long run is underway. A separate `/side` command forks the conversation without interrupting the goal loop, so you can ask questions or debug while the main run keeps going — this is what makes multi-hour unattended sessions usable rather than a lockout. The presenter ran a 9-hour overnight migration this way.

## How to prompt a goal well

The operating envelope: a goal should be bigger than a single prompt but smaller than an open-ended backlog. A good goal prompt specifies four things — what to achieve, what *not* to change, how to validate progress, and when to stop. The "don't touch" and "how to validate" pieces are load-bearing: they're what stop the agent from declaring victory via regression or hallucinated success.

Validation has to be machine-checkable — visual diffs via a browser-automation tool, eval scores, or a test created per milestone. Every goal needs a closed feedback loop the agent can run on its own, or the judge has nothing to evaluate against.

One contributor's pattern after running goals for three days across 30 rounds: don't start by pasting a prompt. Have the agent interview you first — project context, what you care about, what "bad" looks like to users, what's already been tried, recurring bugs — then ask the model what else it needs to know. Skipping that alignment step is, in his telling, why most goal runs return garbage. His other rule: never write "until everything is fixed" as a stop condition — that fuzzy-done phrasing makes the model either quit too early or spiral. Use a number instead (e.g., "find 20 discrete issues, produce a repro and a proposed fix for each, push to a branch").

Even greenfield, from-scratch projects need explicit success criteria — "improve the UX" isn't a stop condition. The broader lesson: a goal prompt is where you front-load the spec work you'd otherwise do during review, not where you save time by staying vague.

## Goal-buddy: outsourcing the prompt-writing

Goal-buddy is an open-source helper that automates the interview step: install it, then inside a session type `$` to list installed tools, then run a prep command that triggers an interview. It outputs a structured `goal.md` (requests, constraints, stop rules, detail loop) and a `state.yaml` (a derived task list). You then point `/goal` at `goal.md` instead of typing a raw prompt; the agent updates `state.yaml` each loop and re-reads `goal.md` every iteration.

The generalizable idea here isn't the tool itself — it's the three-file separation: spec (`goal.md`), state (`state.yaml`), and execution (the loop). Anyone running long agent sessions can adopt that pattern without the specific tool.

## Where /goal breaks: the missions idea

`/goal` requires an immediate, verifiable feedback signal inside the loop. Anything without one — SEO, ad-spend optimization, growth strategy, audience building — breaks the feature, because the duration isn't the real constraint, the absence of a checkable signal is.

The presenter's team is experimenting with a separate "mission" concept as the architectural answer: instead of a tight loop, a mission schedules its next run hours, days, or weeks out — matching the natural cadence of the underlying signal (you can't measure ad performance every 30 seconds). A `mission.md` defines the metrics to optimize; each run receives that file plus a summary of the previous step, forms a hypothesis, executes one step, outputs an artifact, and schedules the next run. The agent can escalate to a human if it wants to try something dramatic or decides the mission is unverifiable — a safety valve `/goal` doesn't have.

Demo example cited: a "grow this account's followers to 10,000" mission that posted, measured, hypothesized a style change (more personal voice), and iterated based on what performed better each cycle. The same shape — hypothesize, act, measure, reschedule — should generalize to ad-campaign optimization or any slow-feedback growth problem.

> "The model can sometimes get lazy and declare the victory too early." — AI Jason

## Takeaways

- Long-running agents fail by declaring victory early, not by running out of ideas — build in an external or self-audit check.
- A goal prompt needs four parts: what to achieve, what not to touch, how to validate, when to stop. Vague goals get vague (or fabricated) results.
- Separate spec, state, and execution into their own files for any long agent run — it's what makes a multi-hour session survivable and resumable.
- Tasks without a fast, checkable feedback signal (growth, SEO, brand work) need a slower "hypothesize → act → measure → reschedule" loop, not a tight while-loop.
