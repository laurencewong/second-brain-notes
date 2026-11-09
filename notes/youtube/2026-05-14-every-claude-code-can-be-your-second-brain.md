---
title: "Claude Code Can Be Your Second Brain"
source_url: https://youtu.be/in7i-EVDDlk
channel: Every
video_title: "Claude Code Can Be Your Second Brain"
captured: 2026-05-14
tags: [ai-agents, personal-knowledge-management, voice-ai, note-taking]
---

# Claude Code Can Be Your Second Brain

**Source:** [Every — "Claude Code Can Be Your Second Brain"](https://youtu.be/in7i-EVDDlk), Dan Shipper interviewing Noah Brier (Alephic, BRXND, formerly Percolate)

Dan Shipper interviews Noah Brier about running a coding-agent-on-notes setup from a home server that lets him do real research and writing from his phone. His central claim: AI's most overlooked use isn't writing — it's reading, and configuring an agent as a "thinking partner" that's explicitly forbidden from producing drafts is what unlocks deep work in small pockets of time.

## Doing deep work from a phone

The non-obvious unlock: a phone can become a serious thinking device. Before AI, phones were fine for quick triage but useless for research, coding, or real writing; voice models paired with a coding agent running against a personal knowledge base invert that. Brier describes doing real research while driving, shipping a small code fix from outside, and working on a talk from his phone during short windows between other commitments. The bottleneck was never the phone's hardware — it was the lack of an interface that could absorb half-formed thoughts and turn them into structured output.

On voice assistants specifically, Brier argues the value of a voice model is downstream of whether its tool-calling actually works mid-conversation — a voice model that can't fetch real information while talking is just a chatbot, while one that can becomes a genuine research partner.

## The notes-system setup

The architecture, in outline: a coding agent runs at the root of a large, folder-organized notes system (around 1,500 notes) rather than in a subfolder, so it has access to everything. He adds a small config file at the notes-root to give the agent custom commands. For each project (a talk, an essay), he spins up a folder containing full transcripts of past AI conversations, source research (articles, PDFs), daily AI-written progress summaries, and his own thinking notes — turning the whole notes system into a cross-tool memory layer the agent reads against. He's explicit that this doesn't require the agent to make conceptual leaps; it's doing a glorified search across notes he already knows are relevant. The capability is simple file traversal — the value is in the integration.

One talk he built this way was centered on the 1944 OSS *Simple Sabotage Field Manual* — wartime advice to citizen-saboteurs (refer things to committee, revisit decisions already made, demand excessive process) that reads uncomfortably like ordinary corporate behavior today. His argument is that AI can sidestep organizational bureaucracy precisely because it acts as a flexible interface that doesn't require restructuring how a team already works, rather than forcing a new process on top of it.

## The "thinking partner" pattern

The most replicable idea in the conversation: a dedicated agent whose system prompt explicitly forbids it from writing anything. Something close to: *you are a collaborative thinking partner; your role is to facilitate thinking; do not under any circumstances try to write it.* Brier's observation is that models default toward producing finished output even when told not to, because that's what they're optimized to deliver — so the instruction has to be forceful and structurally enforced through a separate, narrowly-scoped agent rather than a casual aside in a longer prompt.

In practice, the thinking-partner agent asks sharp clarifying questions, logs the running Q&A as notes in the project folder, and supports a simple recurring query — "catch me up on the last few days of research" — which he describes as the single highest-value way to re-enter deep work after an interruption.

## The "English muffin" theory of AI adoption

Brier's broader thesis on organizational AI adoption: past enterprise software forced teams to standardize on one tool or suffer a painful, centrally-driven migration (one team on tool A, another on tool B, consultants brought in, most of the company unhappy with the result). AI is different because it can absorb structural difference instead of forcing uniformity — it gets into "the nooks and crannies" of however each team already works, without requiring everyone to adopt the same system. He gives an example from his own small company: instead of building a shared library when two different teams needed similar functionality, they just had one team ask the agent to study how the other team's code worked and build their own version — tacit code-sharing without the overhead of formal abstraction, because for a small team the cost of re-implementing is sometimes lower than the cost of maintaining a shared dependency.

> "It gets into the nooks and crannies." — Noah Brier

## White space and building new intuition

Brier traces his own "aha" moment to an early AI plugin specification, where a developer could describe their own data contract and have the assistant adapt to it — a reversal of a career spent integrating with other companies' APIs on their terms. His broader point: most people's intuition about how software integration works is now actively miscalibrated for this new environment, and the only way to build correct intuition is through direct use, not reasoning about it in the abstract. His pushback to people who feel like they've already fallen behind: almost no one is more than a few steps ahead of anyone else right now, because the territory is still this unmapped.

> "What's really lacking is the vocabulary." — Noah Brier, on why ordinary deterministic-software language doesn't fit probabilistic AI tools

## AI and how kids learn

Brier describes his child building a small app with an AI coding tool across many iterations, unprompted discovering the idea of generalizing specific categories ("adults" and "kids" becoming "groups") — his takeaway being that if a child can build a working piece of software this way, the underlying technology is real regardless of hype cycles. On AI and cheating in schools, his view is that AI exposes existing flaws in how writing is taught and assessed rather than creating new ones — rote five-paragraph-essay drills were already misaligned with how people actually write and think. His reframe for a worried teacher: the job was never really "teach kids to write" (a lifelong pursuit) so much as "convince them it's worth learning to," a goal AI doesn't change. He also cites an oral-exam format — long-form spoken defense of ideas in front of faculty — as a naturally AI-resistant assessment design, since preparation can't be faked in the room.

> "I think your job is to convince them that it's worth learning to write." — Noah Brier

## The home-server setup

The practical stack he describes: a small always-on computer at home running a coding agent against his synced notes system, reachable securely from his phone over a personal VPN, with a lightweight terminal app as the only thing installed on the phone itself. The computation and file access stay on the home machine; the phone is just a thin client. He also mentions a small side project — a scripted job that cleans up and renames every attachment in his notes system automatically — as an example of notes-maintenance work that AI makes close to free.

## Takeaways

- A dedicated "thinking partner" agent that is explicitly forbidden from writing anything is one of the more useful and underused agent patterns — most people only build agents to produce output.
- Reading and synthesizing across your own notes is a more durable daily use of AI than writing, even though writing gets most of the attention.
- A small, flexible AI layer can accommodate how different people or teams already work instead of forcing everyone onto one standardized tool — worth remembering before mandating a single workflow.
- Running a coding agent against a personal notes system from a home server, reached securely from a phone, turns small pockets of otherwise-idle time (commutes, waiting rooms) into real research and writing time.
