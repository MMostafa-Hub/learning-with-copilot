# Anki operations

Mechanics for actually getting well-designed cards into Anki via the Anki MCP tools. Anki must be running with AnkiConnect available.

## Deck structure

```
<Course>::<Lesson>
```

Two levels. `create_deck` caps nesting at 2, so the course is the parent and the lesson is the child. Creating `Course::Lesson` creates the parent automatically. Put nothing directly in the parent deck — it exists to aggregate.

Name the course deck after the thing the learner actually calls it. Avoid a bare `:` inside a deck name; `::` is the separator and a stray colon reads badly next to it.

`create_deck` only makes an empty deck. It never adds cards. Adding notes is a separate, explicit step.

## Note types

| Use | Type | When |
|---|---|---|
| Formulas, definitions, ordered sequences | `Cloze` | Default choice. Highest value per unit of effort. |
| Question-to-answer reasoning, mechanism, numeric application | `Basic` | When the retrieval direction matters and a blank would give it away. |
| Term-to-definition pairs you want both ways | `Basic (and reversed card)` | Sparingly. Doubles review load and invites interference. |

Check `model_names` before assuming a type exists. `Cloze` requires `Text` and `Back Extra`; `Basic` requires `Front` and `Back`. Confirm with `model_field_names` rather than guessing.

## Cloze syntax

```
new_prior(l) = {{c1::sum over s}} of posterior(s) x P(displacement = {{c2::l - s}})
```

Each `c1`, `c2` becomes its own card from one note. Multiple deletions with the *same* index reveal together — useful when two blanks are genuinely one idea, wrong when they are two.

Keep deletions small. Blanking half a sentence produces a card that tests nothing precisely.

## Math rendering

**Anki uses `\(...\)` for inline math and `\[...\]` for display math. It does not use `$...$`.**

This matters when porting from Obsidian, where `$P(X_i|Z)$` is normal. That exact string will render as literal dollar signs in Anki. Convert:

| Obsidian | Anki |
|---|---|
| `$P(X_i \mid Z)$` | `\(P(X_i \mid Z)\)` |
| `$$ ... $$` | `\[ ... \]` |

When passing fields through JSON to the MCP tools, a single backslash in the final card is written `\\` in the JSON string. Getting this wrong renders raw markup, which is the single most common way one of these decks ships broken.

Cloze and MathJax interact badly when a deletion lands inside a math expression. Prefer wrapping the whole expression in one deletion, or splitting into a `Basic` note.

## HTML in fields

Fields accept HTML. `<br>` for line breaks, `<b>` for emphasis, `<ul><li>` for the rare genuine list. Plain newlines in a field do **not** render as line breaks.

Escape `<`, `>`, and `&` when they are literal content rather than markup.

## Tags

Tag every note so the deck stays queryable and repairable later:

```
course::<slug>        e.g. course::cs7638
lesson::<slug>        e.g. lesson::localization
node::<node-name>     e.g. node::motion-update
rung::<1-5>           which ladder rung this card is
src::<session-date>   e.g. src::2026-09-07
```

This is what makes a second pass possible. `rung::3` finds every numeric card; `node::motion-update` finds the whole nucleus around one idea when a card there goes bad.

Use `tag_management` to add or rename tags in bulk after the fact.

## Writing notes

Use `add_notes` (plural) for a batch — one call, atomic, far fewer round trips than looping `add_note`. Anki rejects duplicates on the first field by default, so a partial re-run is safe but will report skips.

Before writing, always show the learner the drafted cards. After writing, verify with `find_notes` on the deck and report the actual count rather than the intended one.

## Repair

- `find_notes` with a `deck:` or `tag:` query to locate cards.
- `notes_info` to read current field contents.
- `update_note_fields` to rewrite a bad stem in place. This preserves the review history, which `delete_notes` plus re-add would destroy. Prefer updating.
- `delete_notes` only for cards that should never have existed.

## Scheduling

Do not touch FSRS parameters or deck options as part of building a deck. Anki's defaults are well-tuned, and `optimize_fsrs_params` needs a real review history before it means anything. Revisit only after the learner has hundreds of reviews logged and reports the intervals feel wrong.

## Sync

`sync` after a batch write if the learner uses AnkiWeb. Ask first — a sync at the wrong moment can surface conflicts on their other devices.
