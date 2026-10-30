# Every Company Should Have a Brain — Garry Tan (AI Engineer conference)

**Speaker:** Garry Tan, President/CEO of Y Combinator | **Source:** AI Engineer conference talk | **Watch:** https://youtu.be/eBUyTS7SzV4

## The core idea

Garry Tan's argument is that the leverage from AI doesn't come from the model itself — a below-average employee and a top performer are often using the exact same underlying model. The leverage comes from *how the work is wired*: what context and instructions get loaded into an AI agent, and when. He frames building a company around agents as building an organization — "a workforce made of markdown" — and argues every company will eventually need a "brain": a curated memory and context layer that decides what knowledge an agent sees at the right moment.

## Mapping agent infrastructure onto an org chart

The idea Tan most wants people to take away: a written instruction set for one capability (a "skill file") functions like an employee. A routing layer that sends a task to the right handler functions like an org chart. Rules about what gets filed where function like process and compliance. And tests that check whether the right skill actually loads at the right time function like performance reviews. His point is that the "management layer" that was previously implicit and human is now something you can and should build explicitly into your agent infrastructure.

## Two kinds of computation, kept separate

Tan argues most agent bugs come from putting work on the wrong side of a line: "latent space" (the language model — good for taste, judgment, and vague human intent, steered through written instructions) versus "deterministic space" (ordinary code — good for state, data, and anything that needs to be exact). His example: a large array of records should never live inside a model's context window; code should hold the data, while the model handles the judgment calls about what to do with it.

## The "brain" is a library, and curation is the product

Tan's framing: with roughly a million tokens of context, you can have the equivalent of about three books open on a desk at once — but a company accumulates the equivalent of an entire library over time. The hard problem isn't retrieval (he's blunt that "this is just RAG," the same way a database is "just B-trees") — it's deciding what's worth writing down, enriching, linking, and promoting in the first place. "Being worth retrieving from is the product."

Without active curation, he warns, a knowledge base becomes "a garbage dump with great search" — it will retrieve stale or wrong information with complete confidence, and a flawed process encoded as a "skill" gets repeated forever. His prescription: treat the knowledge base like production infrastructure — track where facts came from, actively check for contradictions when new information conflicts with old, and assign an ongoing "librarian" role (human, agent, or both) whose job is pruning and maintaining it.

## "Rent the model, own the brain"

His summary line: an organization that captures and structures what it learns gets smarter every day, while one that doesn't effectively wakes up with amnesia each morning regardless of how good the underlying model is.

## The headline discipline: "skillify" repeated work

Tan's most concrete, repeatable advice: after any agent successfully completes a task, convert what worked into a reusable, named skill file rather than solving the same problem from scratch next time. His test for whether you've done this well: "if you have to ask for something twice, you failed."

## Illustrative examples from the talk

Tan cited examples from Y Combinator companies of very small teams reaching large revenue figures, attributing it partly to this agent-infrastructure approach — including a non-engineer who used agents to consolidate around a hundred spreadsheets into a single internal tool without ever opening a terminal, effectively becoming "a manager of agents." He also described his own personal note-taking system, built up over many years and heavily agent-maintained, which can surface relevant past context automatically — his description of the difference this makes was "the difference between an assistant and a colleague."

## Most actionable takeaways

1. After any task an agent completes well, turn the successful approach into a reusable skill rather than one-off work.
2. Deliberately map your agent setup onto an org-chart-like structure: one skill per capability, a routing layer, filing rules, and tests that check the right skill loads at the right time.
3. Keep factual/numeric state in ordinary code and judgment calls in the model — don't blur the two.
4. Curate accumulated knowledge like production infrastructure: track provenance, check for contradictions, and assign someone (or something) to prune it.

## Sources
- AI Engineer conference talk, Garry Tan (YC): https://youtu.be/eBUyTS7SzV4
