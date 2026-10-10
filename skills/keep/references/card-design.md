# Card design

## Why this exists

Most generated decks fail the same way: they test the *vocabulary* of a lesson while the *reasoning* quietly decays. You end up able to say "posterior is proportional to prior times likelihood" and unable to compute one. The research consensus is that retrieval practice does support conceptual understanding, and transfers beyond the studied context — but only when the prompts demand explanation, application, and discrimination rather than surface recall. The card ladder below exists to force that.

## The card ladder

For each reasoning node in the lesson, walk the rungs. Load-bearing nodes get all five. Supporting nodes get rungs 1-2. Already-`known` prerequisites get at most one.

| # | Rung | What it asks | Why it is here |
|---|------|--------------|----------------|
| 1 | **Definition / attribute** | What *is* this object; what is always / sometimes / never true of it | Atomic anchor. Cheap to review, cheap to keep. |
| 2 | **Mechanism / why** | Why does this rule hold — the reason, not the statement | Elaborative interrogation. Converts a fact into a reason you can regenerate. |
| 3 | **Numeric application** | Compute one step with real numbers from the lesson's worked example | The anti-fluency guard. Recognizing a formula is not running it. |
| 4 | **Discrimination** | How does this differ from the adjacent idea it is confusable with | Interference is the largest cause of forgetting in mature decks. Contrast cards pre-empt it. |
| 5 | **Failure / edge** | When does this break, mislead, or not apply | Edge cases are where understanding actually lives, and they resist pattern-matching. |

Rung 3 is the one people skip. Do not skip it.

**Rung 4 is mandatory — not optional — whenever the lesson contains a confusable pair.** If the
map's *Confusable pairs* section lists two nodes that share surface features but need different
procedures, every one of those nodes gets a discrimination card, and at least one card presents
an unlabeled case whose first question is *which one is this?*

This is the highest-value card in a technical deck. Under blocked practice, the dominant error
on a delayed test is not forgetting the procedure — it is **selecting the wrong procedure**,
applying the right method to the wrong problem type (Rohrer & Taylor). Novices sort problems by
surface features; experts sort by governing principle (Chi et al. 1981). A deck of rung-1-to-3
cards trains execution and never once trains selection, which is what the exam actually tests.

Optionally, one **integration card** per lesson that asks the learner to chain several nodes into the lesson's original driving question. Write it last, after the atomic rungs exist — an integration card with no supporting rungs underneath it is just a hard card.

## The five properties every card must have

Adapted from Matuschak:

- **Focused** — one detail. A broad prompt produces vague, partial retrieval and dulls attention.
- **Precise** — unambiguous about what is being asked. Vague stems produce vague answers that never reliably activate the target knowledge.
- **Consistent** — the same answer every single review. An inconsistent card actively inhibits neighboring knowledge.
- **Tractable** — answerable about 90% of the time. Cards you keep failing produce churn and resentment, not learning.
- **Effortful** — the answer must be *retrieved*, not inferred from the stem's shape. Difficulty of retrieval predicts strength of learning.

## Wozniak's rules that matter most here

The full list is 20; these are the ones that bite when building from a lesson.

- **Minimum information principle** — the smallest formulation that still means something. Complex answers get split into cards reviewed independently.
- **Do not learn what you do not understand** — and its corollary, *learn before you memorize*. Cards come after comprehension, never instead of it.
- **Build on basics** — fundamentals are cheap to memorize and everything else hangs off them.
- **Cloze deletion is easy and effective** — the highest value-per-effort format, especially for formulas and definitions.
- **Avoid sets and enumerations** — "list the four steps" is a terrible card. Convert to individual cloze deletions over an *ordered* sequence, so each deletion has a stable neighborhood.
- **Combat interference** — actively hunt for near-duplicate cards. Two cards that feel the same during review are one bug.
- **Optimize wording** — fewer words, sharper stem. Wordy cards are slow cards, and slow cards get skipped.
- **Refer to other memories, and personalize** — tie the card to the learner's own worked example, their own notation, the thing they actually asked about.
- **Provide source and date** — so a card that goes stale can be traced back and repaired.
- **Prioritize** — capacity is finite. A card you do not care about is a card you will resent.

## Nielsen's additions for technical material

- **Atomicity is diagnostic.** When a combined card is missed, you cannot tell *which* part you got wrong. Splitting turns a vague failure into a precise one.
- **No orphans.** A single isolated card on a topic tends not to stick. Enter a nucleus of at least 2-3 interrelated cards.
- **Multiple angles on one fact.** Ask the same idea from different retrieval directions — forward and backward, name-to-mechanism and mechanism-to-name. Different associative paths, deeper encoding.
- **Density.** Roughly 5-20 cards per substantial source. If a lesson yields fewer than 5, it may not warrant a deck at all.
- **Emotional connection beats completionism.** Cards built in service of something the learner is actively doing — a problem set, a project — outperform cards stockpiled for a hypothetical future.

## Failure table

Diagnose every complaint about a card against this before assuming it is a knowledge gap.

| Symptom | Likely cause | Fix |
|---|---|---|
| "I can never remember this one" | Card bundles two facts, or it is an enumeration | Split into atomic cards |
| "I know it but the wording confuses me" | Ambiguous or wordy stem | Tighten wording; add a disambiguating context cue |
| "I get it right but do not know why" | Only rung 1 exists for this node | Add rungs 2 and 3 |
| Two cards feel identical in review | Interference between siblings | Merge, or sharpen the contrast that distinguishes them |
| Right answer arrives instantly with no thought | Pattern-matching on stem shape, not retrieval | Reword; vary phrasing away from the source text |
| Correct on the card, lost on a real problem | Card tests the conclusion, not the computation | Add a rung-3 numeric card |
| Fine on cards, picks the wrong method on the exam | Deck trains execution, never selection | Add rung-4 discrimination cards on the confusable pair |
| Card keeps lapsing across many reviews | The node was marked `known` off an immediate checkpoint and never really locked | Not a card bug — demote the node in the map and re-teach it |
| Card is technically right but meaningless now | Orphan — it lost its context | Add sibling cards, or delete it |

## False positives and false negatives

- **False positive** = right answer, no understanding. Caused by unusual wording, structural giveaways, and yes/no framing. Kill binary cards on sight.
- **False negative** = real understanding, failed card. Caused by stems so terse that another correct answer was equally valid, or by context that made sense the day you wrote it and not six months later. Write for a stranger.

## Timing

Build the core cards the same day as the lesson, while its *meaning* is still intact — the forgetting curve is steepest immediately, and a week later you are reconstructing what the lesson was about rather than encoding it. But do not try to be exhaustive in one sitting: write 5-10 strong cards on the first pass, then deepen on later passes with better context. Exhaustive first-pass ankification is the fastest route to a deck you abandon.

## Sources

- Piotr Wozniak, [Effective learning: Twenty rules of formulating knowledge](https://supermemo.guru/wiki/20_rules_of_knowledge_formulation) and [Minimum information principle](https://supermemo.guru/wiki/Minimum_information_principle)
- Andy Matuschak, [How to write good prompts: using spaced repetition to create understanding](https://andymatuschak.org/prompts/)
- Andy Matuschak, [Important attributes of good spaced repetition memory prompts](https://notes.andymatuschak.org/z42J1vxsMjhkdbrqVfoqjiEesSzfaEqurBtoJ)
- Michael Nielsen, [Augmenting Long-term Memory](https://augmentingcognition.com/ltm.html)
- Jeffrey Karpicke, [Retrieval-Based Learning review (PDF)](https://learninglab.psych.purdue.edu/downloads/2025/2025_Karpicke_Retrieval_Based_Learning_Review.pdf)
- [Far transfer of retrieval-practice benefits: rule-based learning as the underlying mechanism](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11461721/)
- [Anki for Physics and Math](https://unisium.io/guides/how-study-physics-math-anki) — principle cards versus worked-solution self-explanation cards
