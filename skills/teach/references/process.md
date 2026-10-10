# Probe → Plan → Teach

Source: Eero Alvar, *How I Use AI to Learn Things*
https://youtu.be/kzcI5F4tGiU

Load this after `philosophy.md`. Do not skip phases unless the learner already has a fresh map for this exact goal.

## Phase 1 — Probe

Measure the edge of understanding before teaching.

- Start broad, then binary-search every strand the lesson will depend on.
- Multiple-choice through the **harness quiz UI** is appropriate here — a probe sweeps many
  strands fast, and the alternatives carry diagnostic content. See [quiz-ui.md](quiz-ui.md).
  Never dump A/B/C/D in chat.
- Tell them errors here are *useful*: attempting before instruction improves later learning
  even when the attempt fails. A probe is not a test they can do badly on.
- Ask 1–3 questions at a time. Wait for the tool. Do not dump a long exam.
- Let the learner talk through reasoning in a note or in chat. Treat that as signal.
- If they already stated solid ground, skip those strands.
- Write the map to `alvar/maps/<topic>.md`.
- A long probe is a feature when context is thin. It is also a warm-up.

Stop when each dependency strand is labeled `known`, `edge`, `unknown`, or `blocked`.

## Phase 2 — Plan

Reason how to teach **this mind** **this goal**. Do not wing it.

- **Name the criterion task first**, in the learner's own terms, and write it into the map
  header: what will they actually have to *do* — a problem set, an exam, a build, a
  conversation? Quiz response-form is matched to this. Practice the form you get graded in.
- Build a dependency DAG. Each node is one reasoning step, not a chapter.
- **Mark the confusable pairs.** Any two nodes that share surface features but need different
  procedures get flagged in the graph. Those pairs become mandatory discrimination items at
  Gate 2 — see quiz-protocol.md Rule 6.
- Start from `known`. Path through `edge`. Do not start in `unknown` with no ramp.
- Verify claims the plan will treat as fact (use `learn-verify` when the domain is empirical, historical, or you are unsure). Math still gets a pass for named theorems if you would otherwise invent them.
- Show the plan as a mermaid graph **before** teaching. Two jobs: the learner sees what is coming; the graph forces you to finish the reasoning.
- Write the plan into `alvar/sessions/<date>-<topic>.md`.
- Ask if they want the graph changed. Then freeze it until a quiz failure forces a new node.

## Phase 3 — Teach

Walk the DAG. One node per turn. Quizzing runs on the four-gate protocol in
[quiz-protocol.md](quiz-protocol.md) — read it before the first node.

Per node:

1. **Gate 0 — predict.** One concrete prediction question *before* you explain. Unscored.
   Wrong is expected and productive. Say so.
2. **Teach.** One reasoning step. Stop. Do not rush the whole graph (that is the ChatGPT
   failure mode). If a picture would lock the idea, use `learn-visual`.
3. **Invite questions.** Answer them. Do not "finish the lesson" over them.
4. **Gate 1 — checkpoint.** Ask it **open**, in chat, no options. Catches a broken explanation
   while it is still cheap to repair. **Ceiling is `edge`.** A perfect Gate-1 score does not
   grant `known`, ever.
5. **Advance** to the next node.
6. **Gate 2 — lock-in**, one or more nodes later: cold, new numbers, new framing, mixed with
   items from other nodes, at least one discrimination item once a confusable sibling exists.
   `known` is granted here or nowhere.

Open every session after the first with **Gate 3**: 2–3 cold items on last session's `known`
nodes, before new material. A miss demotes to `edge` and the node re-enters teaching.

- Give them things they can accept at face value only after the step they rest on is locked.
- Persist what happened in the session file, including gate, confidence, and distractor chosen.

## Feedback rules

- **Open question first, multiple choice second.** Producing an answer beats picking one.
  Fall to the tool when they stall, or when the item is about discriminating between ideas.
- **Every answer carries a confidence tag** — `sure` / `think so` / `guess`. Correct + guess is
  `edge`. Wrong + `sure` triggers the hypercorrection routine: correct it, re-ask immediately
  in different words, re-queue at Gate 2.
- **A perfect set means the questions were too easy.** Say it out loud and raise the difficulty
  rather than logging it as lock-in. Target roughly 70–85% correct across a set.
- **Half of every Gate-2 set must match the criterion task's response form** — if the criterion
  is "compute it" or "write the code," recognition items don't count toward the half.
- **Failure protocol:** hint → retry → elaborated feedback naming *why their answer was
  attractive* → immediate re-ask in different words → re-queue at Gate 2 → flag for Anki.
  Never reveal at the hint step. Never skip the elaborated feedback.
- Prefer a short applied question over a recap prompt.
- If they answer from vibe, that *is* the vibe signal — mark it `edge` and re-test at Gate 2.

## What the system absorbs

You handle: order, sources, verification, "what next," file logging, diagrams.

They handle: thinking about the material.
