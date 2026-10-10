# Quiz UI — use the harness tool, never markdown MCQs

This file covers **tool mechanics**. For *when* to quiz, what format to lead with, and what a
pass is worth, read [quiz-protocol.md](quiz-protocol.md) — it is the governing document.

Do **not** print A/B/C/D in the chat transcript. Every *multiple-choice* question must go
through the interactive question tool this agent already has. Wait for the tool result before
scoring.

## This rule does not ban open questions

"Never A/B/C/D in chat" forbids **pasting a multiple-choice question as markdown**. It does
not forbid asking a question in chat — an open constructed-response question has no options
to paste.

Per quiz-protocol.md Rule 1, open questions are the **default** and go in chat. This tool is
for the cases where multiple choice is the right instrument:

- the learner stalled on the open version and needs the answer space scaffolded
- the item is about **discriminating** between ideas, where the alternatives *are* the content
- a probe sweeping many strands quickly

So: **open question in chat first, tool second.** Never a pasted MCQ, ever.

If more than one of these tools exists, pick the first match in the table.

| If you have this tool | Harness | Call it |
|-----------------------|---------|---------|
| `ask_user_question` | **Grok Build** or **Codex** | `ask_user_question` |
| `AskUserQuestion` | **Claude Code** | `AskUserQuestion` |
| `question` | **OpenCode** | `question` |
| `quiz` | **Pi** (quiz extension) | `quiz` |
| `ask_user` / `askUserQuestion` / `ask_user_question` | **Pi** (ask-user extension) | that tool |

No match → say which tool is missing and stop. Do not fall back to pasted multiple choice.

## Shared quiz shape

- 1–3 questions per call. Wait.
- One right answer. `multi_select` / `multiSelect` / `multiple` = false.
- Options: 3 content choices + **I don't know**.
- Do **not** mark the correct option `(Recommended)` or put it first on purpose. That leaks the answer. Shuffle or keep a fixed A/B/C order that is not “right answer first.”
- Free-text / Other is for talk-through. Treat a typed reason as signal when scoring.
- Header / strand tag: short (≤12 chars if the tool requires it), e.g. `synbio`, `promoter`, `dogma`.

## Distractors must be competitive

Every wrong option must encode **a specific misconception a real learner could hold** —
ideally one this learner has already shown. Multiple-choice testing only produces a retention
benefit when the alternatives compete, because that is what forces the learner to retrieve
why each wrong option is wrong (Little & Bjork; Sparck, Bjork & Bjork 2016). Filler options
turn the item into elimination practice and the effect vanishes.

Test: **can you name the reasoning error that produces this option?** If not, cut it.

| Verdict | Option | Why |
|---|---|---|
| ✗ | "The variance doubles" | nobody thinks this — noise |
| ✓ | "σ²′ = σ² + r²" | that's the *motion* update; the exact confusion this unit builds |
| ✓ | "44 and 56 → 14 and 86" | took σ² as the ruler instead of σ |

Write each option's `description` to say **what the choice means**, never whether it is right.

**Log the distractor actually chosen, not just right/wrong.** The chosen option names the
misconception; the score is only a summary.

## Ask for confidence

Per quiz-protocol.md Rule 3, every answer carries one word: `sure` / `think so` / `guess`.

Cheapest way with a constrained tool: ask for it in the chat turn that accompanies the call
("tag each answer sure / think so / guess"), or read it off the Other/free-text slot. A
correct answer tagged `guess` is `edge`, not `known`. A wrong answer tagged `sure` triggers
the hypercorrection routine.

## Grok — `ask_user_question`

```
ask_user_question
  questions:
    - question: "<stem>"
      options:
        - label: "<choice>"
          description: "<what this choice means, not whether it is right>"
        - label: "I don't know"
          description: "Skip this strand; do not guess."
      multi_select: false
```

Grok always adds Other. That is the talk-through slot.

## Claude Code — `AskUserQuestion`

```
AskUserQuestion
  questions:
    - question: "<stem>"
      header: "<strand>"
      options:
        - label: "<choice>"
          description: "<what this choice means>"
        - label: "I don't know"
          description: "Skip this strand; do not guess."
      multiSelect: false
```

## Codex — `ask_user_question`

Same job as Grok: tabbed questionnaire, constrained answers. One right option + I don't know. Do not use `request_user_input` for graded quizzes.

## OpenCode — `question`

```
question
  questions:
    - header: "<strand>"
      text: "<stem>"
      options:
        - label: "<choice>"
          description: "<what this choice means>"
        - label: "I don't know"
          description: "Skip this strand; do not guess."
```

## Pi

1. If `quiz` exists (graded quiz extension, as in Eero Alvar’s demo), use it.
2. Else `ask_user` / `askUserQuestion` / `ask_user_question`.
3. Else tell the user to install a quiz or ask-user extension (`pi install npm:pi-ask-user` or their preferred quiz package). Still do not paste MCQs.

## Scoring after the tool returns

Map the selected label to A/B/C/D only in the **map file**, not in the next chat turn as a new quiz. Then update `alvar/maps/<slug>.md` and continue.

Record the **gate** (0/1/2/3), the **distractor chosen**, and the **confidence tag** alongside
the result. Status ceilings are set by the gate, not by the score — see quiz-protocol.md.
A perfect set at Gate 1 is still `edge`.
