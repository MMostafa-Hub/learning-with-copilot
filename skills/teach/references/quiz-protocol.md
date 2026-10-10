# Quiz protocol — when to test, in what form, and what a pass is worth

This file governs **when** you quiz and **what the result means**.
[quiz-ui.md](quiz-ui.md) governs **which tool** you call. Read both.

## The failure this replaces

The naive loop is: teach a step → quiz it immediately → correct answer → mark it locked → move on.

That loop cannot fail, and a test that cannot fail cannot grade. Immediately after an
explanation the answer is still in working memory: retrieval strength is at ceiling, so the
retrieval produces almost no gain in storage strength (Bjork) and almost no diagnostic signal.
Roediger & Karpicke (2006) found the crossover directly — restudy beats testing on a 5-minute
test, testing beats restudy at 2 days and a week. The delayed-JOL meta-analysis (Rhodes &
Tauber 2011, g = 0.93) makes the same point about judgments: immediate ones are contaminated
by short-term memory.

Symptom you will see in your own logs: near-perfect first-try scores on every post-teaching
quiz, followed later by reteaches of material already marked locked, or by the learner saying
"I don't actually get the math" about a node they answered correctly.

Perfect scores are not evidence of learning. They are evidence the questions were mistimed.

## The four gates

Every node passes through these. Only Gate 2 grants `known`.

| Gate | When | Format | Grants at most |
|---|---|---|---|
| **0 — Predict** | *before* teaching the node | one prediction question, real numbers, unscored | nothing (priming only) |
| **1 — Checkpoint** | after teaching, on the learner's go-ahead | open constructed response | **`edge`** |
| **2 — Lock-in** | ≥1 intervening node later, closed book, new numbers, interleaved | mixed set + discrimination item | **`known`** |
| **3 — Carry-over** | next session opener, and Anki review data | cold retrieval on prior `known` nodes | confirms, or **demotes** |

### Gate 0 — Predict (before teaching)

One cheap question with concrete numbers, asked *before* you explain anything:

> Before I show you: you multiply two Gaussians, means 4 and 16, both variance 4.
> Where does the new mean land, and is the result wider or narrower than either input?

Being wrong here is the normal case and it is *productive*. Attempting an answer before
instruction improves later learning even when the attempt fails — it primes attention,
activates the search set, and creates an error-correction signal (Kornell et al. 2009;
Richland et al. 2009; Pan & Carpenter 2023 review).

Rules:
- Never scored, never logged as a failure, never gates anything.
- Say so out loud: "this is a guess-first question, wrong is fine and useful."
- One question. Do not turn it into a probe.
- Skip only if the probe already covered this exact node cold.

### Gate 1 — Checkpoint (immediately after teaching)

Purpose: catch a misunderstanding while the explanation is still repairable. **Not** lock-in.

- Ask it **open** — no options. See "Produce before you recognize" below.
- 1–3 questions. If the learner asked for a range, run easy → hard.
- Honour the learner's gating rule if they have one (e.g. "quiz only when I say I'm ready").
  A learner-imposed delay before this gate is a *feature* — it adds lag. Do not argue with it.
- Result sets `edge` at best. Write `gate: 1` next to the status in the map.
- **Never write `known` from this gate**, no matter how clean the answer or how confident
  the learner. If they got 3/3 with no hedge, that is a Gate-1 pass and it is still `edge`.

Say the ceiling out loud so a clean pass doesn't feel dismissed:

> That's a clean checkpoint — the explanation landed. I'm holding it at `edge` until it
> survives a cold re-test later, because right now the answer is still in working memory.

### Gate 2 — Lock-in (delayed, interleaved)

Purpose: this is the real grade. A node reaches `known` here or not at all.

Conditions, all required:
- **At least one intervening node** has been taught since Gate 1. Later in the same session
  is fine; a different session is better.
- **Closed book.** No scrolling back, no re-reading the session file first.
- **New numbers and new framing.** Not the worked example. Not a rephrase of the Gate-1 stem.
- **Mixed.** Items from ≥2 nodes in the same set, presented unlabeled.
- **At least one discrimination item** once a confusable sibling exists (see below).

Interleaving is not decoration. Rohrer & Taylor's error analysis found that under blocked
practice, most test errors were *strategy-selection* errors — the right procedure applied to
the wrong problem type. If every question in a set is about the node you just taught, the
learner never has to decide which tool applies, which is the one decision the criterion task
will actually demand.

### Gate 3 — Carry-over (next session + Anki)

- Open every session after the first with 2–3 cold items on the previous session's `known`
  nodes, **before** new material. This is where `known` is re-earned.
- A miss here **demotes to `edge`** and the node re-enters teaching. Say this is expected and
  normal; it is the mechanism working, not a regression.
- If `learn-anki` has shipped a deck, read lapse data before the opener and target the
  lapsing nodes. See learn-anki's SKILL.md.

Retrieval to criterion *spaced across sessions* — successive relearning — is the design with
the strongest evidence for durable retention (Rawson & Dunlosky 2022). Notably, extra
retrievals crammed into one session washed out after three spaced sessions. So do not drill
harder in-session. Space it.

---

## Rule 1 — Produce before you recognize

**Every item starts as an open question in chat with no options.** The learner types, computes,
or explains. Only then, and only if needed, do you fall to the harness multiple-choice tool.

This does **not** conflict with quiz-ui.md's "never paste A/B/C/D in chat." That rule forbids
*pasting a multiple-choice question as markdown*. An open question has no options to paste.
The two rules are complementary: open questions go in chat, multiple-choice goes through the tool.

Why: multiple-choice is a recognition device. In university-lecture settings, short-answer
practice produced a testing effect and multiple-choice produced none — attributed to low
retrieval effort plus distractor interference (Frontiers in Psychology 2018; Endres et al.
2022). Recognition is also the specific component implicated in the inert-knowledge problem,
where a learner holds the knowledge but does not recognize that it applies.

Fall to the multiple-choice tool when:
- the learner stalls or asks for options (retrieval failed; scaffold it rather than reveal it);
- the item is genuinely about **discriminating** between two ideas, where the alternatives
  *are* the content;
- you need a fast confidence-calibrated read across many strands at once (probes).

Recall-then-recognize is the hybrid format from Smith & Karpicke (2013): at worst equal to
either format alone, slightly better in one experiment, and far more diagnostic — you learn
whether they could *produce* it, not just pick it.

## Rule 2 — Competitive distractors only

When you do use the multiple-choice tool, **every wrong option must encode a specific
misconception a real learner could hold** — ideally one this learner has already shown.

Multiple-choice testing improves retention of related, non-tested information *only* when
the alternatives are competitive, because the learner must retrieve why each wrong option is
wrong (Little & Bjork 2010; Sparck, Bjork & Bjork 2016). Filler options that are merely
wrong-sounding turn the item into elimination practice and the effect disappears.

Test for a good distractor: **can you name the reasoning error that produces it?**

- Bad: "The variance doubles." (nobody thinks this; it's noise)
- Good: "σ²′ = σ² + r²." (that's the *motion* update — the exact confusion this unit creates)
- Good: "44 and 56 → 14 and 86." (took σ² as the ruler instead of σ)

**Log which distractor was chosen, not just right/wrong.** The chosen distractor names the
misconception. That is the diagnosis; the score is only a summary.

Still applies from quiz-ui.md: one right answer, an "I don't know" option, never mark the
correct option recommended, never put it first on purpose.

## Rule 3 — Tag every answer with confidence

Ask for one word alongside every answer: **`sure` / `think so` / `guess`.**

It costs one line and it makes the map mechanical instead of vibes-based:

| Answer | Confidence | Status move |
|---|---|---|
| correct | sure, sound reason | eligible for `known` (at Gate 2 only) |
| correct | think so | `edge` |
| correct | guess | `edge` — a lucky pick is not knowledge |
| wrong | guess / think so | `edge` or `unknown` per the miss |
| **wrong** | **sure** | **`unknown`** + trigger the hypercorrection routine |

**Hypercorrection routine.** Errors committed with high confidence are corrected *better* than
low-confidence errors — the confidence/feedback mismatch drives attention and encoding
(Butterfield & Metcalfe). But the correction decays unless you test it again immediately:
a test right after the corrective feedback blocks the error from returning (Butler et al.).

So on a confident miss: give the correction → **immediately re-ask in different words** →
re-queue at Gate 2 → and flag the node for a `learn-anki` card. Do not just explain and move on.

## Rule 4 — Calibrate to roughly 70–85% correct

Across a quiz set, aim for one item in four or five to be genuinely hard enough to miss.

**A 3/3 or 6/6 is a signal about the questions, not the learner.** Say so, and raise the
difficulty of the next set rather than logging a perfect score as lock-in:

> 3/3 — but that means I pitched those too easy to tell us much. Next set goes harder.

Support: in the university-lecture study above, the short-answer testing effect appeared only
in the high-retrievability band (items answered roughly 46–81% of the time); items outside
that band produced no benefit. The "85% Rule" (Wilson et al. 2019) points the same direction
but is derived for gradient-descent learners on binary perceptual tasks — treat it as a
suggestive heuristic, not as evidence about human conceptual learning, and do not cite it
to the learner as if it were.

Below ~50% correct: stop quizzing. That is a teaching failure, not a testing opportunity.
Back up and insert a prerequisite node.

## Rule 5 — Match the criterion task

Write the criterion task into the map header, in the learner's own terms:

```
Criterion: PS2 implementation + Unit 3 exam — compute an update by hand,
choose which update applies, debug a filter that diverges.
```

**At least half of every Gate-2 set must have the same response form as that criterion.**
If the criterion is "produce a number" or "write the line of code," then items shaped like
"which statement about the Kalman gain is true?" do not count toward the half.

This is the largest single moderator in the transfer literature. Pan & Rickard's meta-analysis
(122 experiments) found transfer at d = 0.40 overall, **+0.30 when responses were congruent**
between practice and criterion, and **+0.23 with elaborated retrieval**. Agarwal (2019) is
blunter: fact-based retrieval practice produced higher-order test performance
*indistinguishable from no practice at all*, and higher-order practice did not help fact tests.
Practice the form you will be graded in.

Caveat worth holding: for procedural problem-solving specifically, retrieval practice alone
sometimes shows no benefit at all. Worked examples plus **self-explanation** carry more of the
load there (Bisra et al. 2018 meta-analysis, g = 0.55). So for a derivation-heavy node, prefer
"predict the next line before I reveal it" and "explain why this step is legal" over recall
questions about the finished result.

## Rule 6 — Interleave the moment a confusable sibling exists

The trigger is structural, not scheduled: **as soon as the DAG contains two nodes that share
surface features but need different procedures, every later set mixes them, unlabeled.**

The first question in a mixed set is always the discrimination question, asked *before* any
arithmetic:

> Here are three scenarios. For each: which update is this, and what in the wording told you?

Worked example of the trigger in a Kalman unit: the instant the motion update lands, every
subsequent set mixes measurement-update and motion-update items with the labels stripped.
They look identical (two Gaussians, combine them) and their procedures are opposites
(precisions add and variance shrinks / variances add and variance grows). Blocked practice
on those two guarantees the learner can execute both and cannot tell them apart — which is
exactly the error Rohrer & Taylor measured.

Novices sort problems by surface features; experts sort by governing principle (Chi et al.
1981). Discrimination items are how you move a learner across that line.

## Rule 7 — The failure protocol

When an answer is wrong, in this order:

1. **Hint.** Name the region of the reasoning, not the answer. Let them retry.
2. **Retry.** Second attempt on the same item.
3. **Elaborated feedback.** Not "the answer is B." Explain *why their answer was attractive* —
   name the reasoning that produced it and where it breaks. Elaborated feedback is worth
   d ≈ 0.23 on transfer; bare correct-answer feedback is not.
4. **Immediate re-ask in different words.** Same idea, different surface. Confirms the
   correction took rather than the sentence being echoed back.
5. **Re-queue at Gate 2.** The node does not advance to `known` on this pass regardless.
6. **Flag for `learn-anki`.** A missed item is a decay risk and deserves more card angles.

Never reveal the answer at step 1. Never skip step 3 to save time — step 3 is where the
learning is.

## Scoring summary

```
Gate 0   → priming only, unscored
Gate 1   → edge (ceiling)
Gate 2   → known, if: correct + confident + sound reason + delayed + new framing
Gate 3   → confirms known, or demotes to edge
any miss → edge/unknown + failure protocol + re-queue
```

`known` means: **passed cold, later, in different words, mixed with other material.**
Nothing weaker earns the label.

## What to log

In `alvar/maps/<slug>.md`, per item:

```
- N2 G2 [meas-vs-motion] mixed set, unlabeled → picked "variances add" (motion procedure)
  — WRONG, confidence: sure → hypercorrection routine run, re-ask passed, re-queue G2
```

Record: node, gate, strand, the framing, **the distractor actually chosen**, correct/wrong,
**confidence**, and what you did about it. The distractor and the confidence are the parts a
future session cannot reconstruct.

## Sources

- Roediger & Karpicke (2006), *Test-enhanced learning* — https://journals.sagepub.com/doi/10.1111/j.1467-9280.2006.01693.x
- Rhodes & Tauber (2011), delayed-JOL meta-analysis — https://pubmed.ncbi.nlm.nih.gov/21219059/
- Kang, McDermott & Roediger (2007), test format × feedback — https://www.researchgate.net/publication/224943432_Test_format_and_corrective_feedback_modify_the_effect_of_testing_on_long-term_retention
- Testing effect, format and retrievability (Frontiers 2018) — https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2018.02412/full
- Short-answer beneficial, multiple-choice not (2022) — https://www.tandfonline.com/doi/full/10.1080/20445911.2022.2085281
- Smith & Karpicke (2013), short-answer / multiple-choice / hybrid — https://www.tandfonline.com/doi/abs/10.1080/09658211.2013.831454
- Little & Bjork (2012), competitive alternatives — https://bjorklab.psych.ucla.edu/wp-content/uploads/sites/13/2016/07/Little_EBjork_RBjork_Angello_2012.pdf
- Sparck, Bjork & Bjork (2016), confidence-weighted testing — https://cognitiveresearchjournal.springeropen.com/articles/10.1186/s41235-016-0003-x
- Pan & Rickard (2018), transfer meta-analysis — https://pdf.retrievalpractice.org/transfer/Pan_Rickard_2018.pdf
- Agarwal (2019), retrieval practice and Bloom's taxonomy — https://www.researchgate.net/publication/325639446_Retrieval_Practice_Bloom's_Taxonomy_Do_Students_Need_Fact_Knowledge_Before_Higher_Order_Learning
- Rohrer, Dedrick & Stershic (2015), interleaved mathematics practice — http://uweb.cas.usf.edu/~drohrer/pdfs/Rohrer_et_al_2015JEdPsych.pdf
- Chi, Feltovich & Glaser (1981), expert/novice problem categorization — https://onlinelibrary.wiley.com/doi/10.1207/s15516709cog0502_2
- Rawson & Dunlosky (2022), successive relearning — https://journals.sagepub.com/doi/full/10.1177/09637214221100484
- Prequestioning and pretesting effects review (2023) — https://link.springer.com/article/10.1007/s10648-023-09814-5
- Butterfield & Metcalfe, hypercorrection; persistence over a week — https://link.springer.com/article/10.3758/s13423-011-0173-y
- Bisra et al. (2018), self-explanation meta-analysis — https://gwern.net/doc/psychology/spaced-repetition/2018-bisra.pdf
- Retrieval practice may not benefit math word-problem solving (2023) — https://pmc.ncbi.nlm.nih.gov/articles/PMC9987560/
- Wilson et al. (2019), Eighty Five Percent Rule (scope: gradient-descent learners) — https://www.nature.com/articles/s41467-019-12552-4
