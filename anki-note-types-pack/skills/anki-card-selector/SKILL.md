---
name: anki-card-selector
description: >
  Routes user learning material to the right Anki note type and specialized skill (Basic, Cloze, lan_1.1, or lan_sen_1.1) enforcing strict Basic-vs-Cloze rules.
  Trigger: When the user asks to create, convert, or structure Anki flashcards or study notes.
license: Apache-2.0
metadata:
  author: BlackLion_s99
  version: "2.0"
---

# Anki Card Selector

Routes any learning input to the right Anki note type and creator skill (`anki-basic-creator`, `anki-cloze-creator`, `anki-lan-creator`, or `anki-lan-sen-creator`).

## Critical Rules

1. **Atomic Principle**: Test exactly ONE recall target per card. Split multi-point ideas into separate cards.
2. **Basic vs. Cloze Boundary (Strict)**:
   - Use **`Basic`** (`Basic` or `Basic_Custom`) for **all conceptual, analytical, definitional, situational, and key-value knowledge**.
   - Use **`Cloze`** (`Cloze` or `Cloze_Custom`) **ONLY for literal / verbatim memorization**: CLI commands and flags, exact code syntax, Bible verses, exact quotes (*citas*), or formulas that must be recalled word-for-word.
   - **Never** use `Cloze` for general concepts or "conceptual Dual-Gain" sentences — convert those into crisp `Basic` questions.
3. **Check Installed Note Type Names First**: Run `anki_list_note_types` before creating notes. If the user imported `anki-note-types-pack.apkg` without renaming, `Basic` and `Cloze` appear as `Basic_Custom` and `Cloze_Custom`.
4. **Anki Integration Channel**:
   - Single notes or small batches: `anki` MCP (`anki_create_note`, `anki_batch_create_notes`).
   - Bulk operations, moving cards while preserving review history (`changeDeck`), or reading `modelFieldDescriptions`: AnkiConnect directly (`http://127.0.0.1:8765`).

## Decision Tree

| Content Type | Model | Skill to Load | Example |
| :--- | :--- | :--- | :--- |
| Concepts, definitions, tradeoffs, key-value facts, architecture, situational rules | `Basic` / `Basic_Custom` | `anki-basic-creator` | "What problem does idempotency solve in payment APIs?" |
| Literal recall only: CLI commands, exact syntax, Bible verses, quotes, formulas | `Cloze` / `Cloze_Custom` | `anki-cloze-creator` | `git {{c1::remote}} {{c2::prune}} {{c3::origin}}` |
| Single vocabulary word in a target language (`en`, `es`, `pt`, `it`, `de`) | `lan_1.1` | `anki-lan-creator` | Word: `resilient` / `alleviate` |
| Contextual phrase, idiom, phrasal verb, grammar pattern, or dictation | `lan_sen_1.1` | `anki-lan-sen-creator` | `"Had I known earlier..."` (target: `Had I known`) |

## Action Protocol

1. Inspect decks and note types (`anki_list_decks`, `anki_list_note_types`).
2. Select the matching creator skill from the table above and follow its exact field contract.
3. Briefly state your model choice and rationale before/when creating cards (e.g., "`Basic` because this tests a conceptual tradeoff, not literal syntax" or "`Cloze` because this command must be recalled verbatim").
4. Always send **HTML** (never Markdown) in Anki fields, and supply every required field explicitly.
