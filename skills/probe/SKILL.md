---
name: probe
description: >
  Map the edge of the learner's understanding with a short graded quiz.
  Start broad, then binary-search every strand a lesson will need. Use when
  the user runs /probe or /skill:probe, or says quiz me, pretest, what do I
  already know, diagnose my understanding, probe me, or find the edge before
  teaching.
license: MIT
metadata:
  author: vasanthsreeram
  version: "1.0"
  source: "Eero Alvar — How I Use AI to Learn Things https://youtu.be/kzcI5F4tGiU"
---

# Probe

Measure first. Do not teach during a probe except a one-line correction after they answer.

**Quiz UI is mandatory.** Read [../teach/references/quiz-ui.md](../teach/references/quiz-ui.md) and call that tool. Never print A/B/C/D in the chat.

Multiple choice is the *right* instrument here — a probe sweeps many strands fast, and with
competitive distractors the alternatives themselves carry the diagnosis. This is unlike the
in-lesson gates, where open questions lead. See
[../teach/references/quiz-protocol.md](../teach/references/quiz-protocol.md).

## Tell them errors are productive

Say it before the first question:

> Wrong answers here are useful, not embarrassing. Guessing at something before you learn it
> makes the teaching land better afterwards — even when the guess is wrong. "I don't know" is
> a real answer and it saves us both time.

This is true (the pretesting effect), and it stops a learner from hedging their way into a
map full of lucky guesses labelled `known`.

## Goal

Produce `alvar/maps/<slug>.md` that labels every dependency strand:

`known` | `edge` | `unknown` | `blocked`

`blocked` = they said they don't know, or the question needs a tool you don't have.

## How to ask

- 1–3 multiple-choice questions per turn. Wait.
- Always include **D. I don't know** (or an extra "I don't know" option).
- Start wide (what kind of object is this? what does this operator measure?). Then split the strand that the answer leaves ambiguous.
- If they already listed solid ground, skip those strands.
- Invite a talk-through: a wrong reason + right letter is `edge`, not `known`.
- **Ask for a confidence tag** with each answer — `sure` / `think so` / `guess`.

One right answer. No trick options that hinge on wording. Put **I don't know** as an option. Do not mark the correct choice recommended.

**Distractors must be competitive**: each wrong option encodes a specific misconception you
can name. If you cannot state the reasoning error that produces an option, cut it — it is
filler, and filler turns the item into elimination practice. Record **which** distractor was
chosen; that is the diagnosis.

## Scoring

| result | confidence | status move |
|--------|-----------|-------------|
| correct + sound reason | sure | `known` |
| correct, thin reason | any | `edge` |
| correct | guess | `edge` — a lucky pick is not knowledge |
| wrong, near-miss | any | `edge` |
| wrong, foundation missing | any | `unknown` |
| **wrong** | **sure** | `unknown` + flag for hypercorrection when taught |
| I don't know | — | `blocked` or `unknown` |

A `known` from a probe is a *pre-existing* `known` — the learner already held it cold, which is
exactly the delayed, unprompted retrieval the in-lesson gates have to work to manufacture. That
is why a probe can grant it directly and a Gate-1 checkpoint cannot.

After each batch, update the map. Stop when the upcoming lesson's dependencies are all labeled — not when you have asked "enough questions."

## Map file

```markdown
# Map — <goal>

Updated: <ISO date>
Goal: <one sentence>
Criterion: <what they will actually have to DO — problem set, exam, build>

## Strands
| strand | status | gate | evidence |
|--------|--------|------|----------|
| … | known | probe | Q2 + sound reason, confidence: sure |

## Quiz log
- Q1 [strand] chose "<option text>" — correct|wrong|idk — conf: sure|think so|guess — <five words>
```

Log the **option text**, not the letter — letters are meaningless once the shuffle is gone,
and the chosen distractor is the part a future session cannot reconstruct.

## End

Show the table. Say which strands a teacher should start from. Do not start the lesson unless they ask.
