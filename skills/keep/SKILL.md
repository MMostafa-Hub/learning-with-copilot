---
name: keep
description: >
  Turn a finished teaching session into a spaced-repetition deck that defends
  the reasoning, not just the vocabulary. Builds an Anki course deck and lesson
  sub-deck from an alvar session/map via the Anki MCP tools. Use when the user
  runs /keep or /skill:keep, or says make me flashcards, Anki deck,
  ankify this, cards for this lesson, help me retain this, or asks to lock in
  material after a teach session.
license: MIT
metadata:
  author: mohamed
  version: "1.0"
  source: >
    Synthesis of Wozniak (20 rules of knowledge formulation),
    Matuschak (How to write good prompts), Nielsen (Augmenting Long-term Memory),
    and Roediger/Karpicke retrieval-practice research. See references/card-design.md.
---

# Learn-Anki

You are converting **understanding that already happened** into **retrieval that will keep happening.**

This skill runs *after* teaching, not instead of it. Anki does not create understanding — it prevents the decay of understanding you already earned. Wozniak's Rule 1 is load-bearing here: *do not memorize what you do not understand.* If the session map shows a node at `edge` or `unknown`, that node does not get cards. It gets taught first.

`edge` includes **nodes that only ever passed an immediate checkpoint** (Gate 1 in
`teach`'s quiz protocol). A clean answer given ninety seconds after the explanation is not
evidence of understanding — it is evidence the answer was still in working memory. Those nodes
owe a cold re-test before they earn cards. Check the map's **Gate-2 debt** section first.

Read before writing a single card:

1. [references/card-design.md](references/card-design.md) — the card ladder and the design rules. **Required.**
2. [references/anki-ops.md](references/anki-ops.md) — deck naming, note types, MathJax, tags, MCP call shape. **Required.**
3. `alvar/LEARNER.md` — controls voice, density, and what counts as solid ground.
4. The session file `alvar/sessions/<date>-<slug>.md` and map `alvar/maps/<slug>.md` for this lesson.

## The core move

An alvar session already produced a DAG of reasoning nodes with lock-in evidence attached. **That DAG is the card blueprint.** Do not re-derive structure from the raw notes — the teaching already decided what the load-bearing steps were, and the quiz log already recorded which ones were hard.

"Lock-in evidence" means a **Gate-2 pass** — cold, delayed, differently worded. A node carrying
only a Gate-1 checkpoint is `edge` and does not get cards yet.

For each node: build a **card ladder** (see card-design.md). Load-bearing nodes get the full ladder. Supporting nodes get one or two rungs. Nodes marked `known` before teaching started get a single maintenance card at most.

Weight by the quiz log, not by the prose. A node the learner missed on first attempt, or one the teacher had to correct mid-lesson, is a decay risk — give it more angles. A node that transferred cleanly to a flipped configuration needs fewer.

## Hard rules

- **One card, one retrieval.** If the answer has two independent parts, it is two cards.
- **No card the learner cannot answer ~90% of the time** once the lesson is fresh. Tractable beats clever.
- **No binary yes/no cards.** Reframe as open retrieval. A coin flip is not evidence of knowledge.
- **No orphans.** Every card sits in a nucleus of 2+ related cards on the same idea. An isolated fact does not survive.
- **Answers must be stable.** If a card could be answered three different correct ways, it will trigger retrieval-induced forgetting. Tighten the stem.
- **Compute, don't conclude.** At least one card per mechanism must demand the actual calculation, not the name of the result. This is the specific guard against a right answer that hides shaky math.
- **Never invent content.** Cards come from the session, the map, and the learner's own notes. If you want a card about something not taught, say so and ask — do not quietly extend the syllabus.

## Procedure

1. **Confirm scope.** Which lesson, which nodes. Show the node list with its status and let the learner cut.
2. **Check readiness.** Any node not `known` → flag it, exclude it, recommend teaching it first.
3. **Name the decks.** Course deck, lesson sub-deck. Two levels max (see anki-ops.md).
4. **Draft the ladder** for every included node. Show the learner the draft cards **before** writing to Anki. This is the audit step and it is not optional — an unaudited generated deck is a deck of near-misses.
5. **Write** via the Anki MCP tools. Tag every note with course, lesson, node, and rung.
6. **Log it.** Append a `## Cards` section to the session file: what shipped, how many, which nodes, the date. A future session should be able to see what is already defended.

## Feeding review data back to the teacher

The deck is not a write-only archive. It is the only instrument in this system that measures
retention across days, which makes it the evidence source for `teach`'s Gate 3 (carry-over).

When a `teach` session opens on a topic that already has a deck:

1. Read lapse data before teaching anything — `cards_stats` / `get_card_memory_state` over the
   lesson deck, or `find_notes` on `tag:lesson::<slug>` then `notes_info`.
2. **A node whose cards keep lapsing is not `known`.** Demote it in `alvar/maps/<slug>.md` and
   open the session by re-teaching or re-testing it, ahead of new material.
3. Tell the learner which nodes the data flagged. Repeated lapses on one node are a signal
   about the *teaching*, not about their memory — usually the node was marked `known` off an
   immediate checkpoint that never survived a delay.

This closes the loop: spaced retrieval across sessions is the design with the strongest
evidence for durable retention (successive relearning), and it only works if failures come
back to the teacher instead of dying in the review queue.

## Two passes, not one

Ship the core ladder the same day the lesson lands — the forgetting curve is steepest in the first 24 hours and the lesson's meaning is still intact. Then, after the learner has actually reviewed the deck a few times, do a second pass: cards that consistently frustrate get rewritten or split, cards that are trivially easy get merged or deleted, and new cards get added where reviews exposed a gap. Prompt-writing is iterative. A deck is a draft.

## When the learner reports a bad card

Do not defend the card. Diagnose it against the failure table in card-design.md — ambiguous stem, buried second question, interference with a sibling card, or a genuine gap in understanding. Only the last one is a teaching problem; the first three are your bug. Fix and move on.
