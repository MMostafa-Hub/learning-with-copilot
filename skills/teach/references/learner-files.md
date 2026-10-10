# Learner files

All session state lives in the **learner's working directory**, not in this skill repo.

```
alvar/
  LEARNER.md                 # how this mind wants to be taught
  maps/<slug>.md             # probe results for one goal
  sessions/<date>-<slug>.md  # plan + steps + quizzes
  visuals/<slug>-<n>.svg     # diagrams from learn-visual
```

Create `alvar/` on first use.

## LEARNER.md

If missing, run `learn-profile` or write a stub from `assets/LEARNER.md` and ask 3–5 questions to fill it. Do not invent a personality.

Read LEARNER.md at the start of every `teach` session. It controls:

- voice and density
- how they want struggle
- what they already treat as solid
- whether they want visuals, mermaid, LaTeX, or a long markdown log

## Map file

```markdown
# Map — <goal>

Updated: <ISO date>
Goal: <one sentence>
Criterion: <what they will actually have to DO — e.g. "PS2 code + exam:
compute an update by hand, choose which update applies, debug a diverging filter">

## Strands
| strand | status | gate | evidence |
|--------|--------|------|----------|
| line integrals | known | G2 | cold re-test day 2, new numbers, conf: sure |
| Stokes | edge | G1 | checkpoint passed, never re-tested cold |
| differential forms | unknown | — | said so |
| SR field mix | blocked | probe | answered "I don't know" |

Status: `known` | `edge` | `unknown` | `blocked`
Gate: `probe` | `G1` (checkpoint, ceiling `edge`) | `G2` (lock-in) | `G3` (carry-over)

**`known` requires G2 or a cold probe pass.** A node whose only evidence is `G1` is `edge`,
however clean the answer was.

## Gate-2 debt
Nodes that passed a checkpoint and still owe a cold, delayed, mixed re-test:
- Stokes — checkpoint 2026-09-07, owes G2

## Confusable pairs
Nodes that share surface features and need different procedures. These get mandatory
discrimination items at G2, presented unlabeled.
- measurement update ⟷ motion update

## Quiz log
- G1 [line integrals] open Q → "∮F·dr, parameterize then integrate" — correct, conf: sure
- G2 [line integrals] cold, mixed w/ Stokes → correct, conf: sure — promoted to known
- G2 [Stokes] chose "curl of the field over the boundary" (swapped surface/boundary)
  — WRONG, conf: sure → hypercorrection run, re-ask passed, re-queued
```

## Session file

```markdown
# Session — <goal>
Date:
Model:
Goal:

## Plan
\`\`\`mermaid
graph TD
  A[covector] --> B[1-form]
  B --> C[wedge]
\`\`\`

## Log
### Node: covector
- G0 predict:
- taught:
- visual:
- G1 checkpoint (open question):
- result: edge | retry | insert-prereq       <- G1 can never yield "known"
- G2 lock-in (cold, new numbers, mixed, ≥1 node later):
- result: known | re-queued

## Gate-2 debt at close
- <node> — passed checkpoint, owes a cold re-test next session
```

Keep these files updated as you go. They are the persistence layer (the portable stand-in for a markdown-log / Obsidian pane).
