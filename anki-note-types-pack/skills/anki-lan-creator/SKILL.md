---
name: anki-lan-creator
description: >
  Creates single-word vocabulary Anki cards using the lan_1.1 note type (Reconocimiento, translation-to-word, Production) for en, es, pt, it, and de.
  Trigger: When creating vocabulary flashcards for individual words in English, Spanish, Portuguese, Italian, or German.
license: Apache-2.0
metadata:
  author: BlackLion_s99
  version: "2.0"
---

# Anki Language Vocabulary Creator (`lan_1.1`)

Creates 3-card vocabulary notes (`Reconocimiento`, `translation-to-word`, `Production`) using the `lan_1.1` note type.

## When to Use

- Learning individual vocabulary words (`en`, `es`, `pt`, `it`, `de`).
- For idioms, phrasal verbs, grammar structures, or sentence dictation, use `anki-lan-sen-creator` (`lan_sen_1.1`).

## Field Mapping & AI Instructions

| Field | Purpose | AI Population Rule |
| :--- | :--- | :--- |
| `word` | Target word; typed in `Production` (`{{type:word}}`) and auto-matched in examples. | Base word only (no articles/punctuation) so JS word-boundary highlighting and typing work cleanly. |
| `trans_word` | Spanish translation(s) shown in *Spanish Support*. | Concise, natural Spanish equivalents (e.g., `"aliviar / mitigar"`). |
| `rom` | Optional IPA or pronunciation guide. | IPA (e.g., `/rɪˈzɪliənt/`) or syllable guide, or `""`. |
| `audio` | Audio on *Recognition*, *Listening* front, and backs. | `[sound:...]` or `{{tts ...}}` if available; else `""` (or plain `word` only for batch HyperTTS generation). |
| `image` | Optional illustrative image on back header. | `""` unless an image tag/file is explicitly provided. |
| `menomics` | Optional mnemonic in *Memory Aid* (exact spelling: `menomics`). | Short, vivid sound/visual/root mnemonic if helpful; else `""`. |
| `definition` | Target-language definition on *Production* front & backs. | Concise HTML (`<b>`, `<i>`) definition **WITHOUT revealing `word`**. |
| `alt_trans` | Optional synonyms/related words in *Related Words*. | `"label::url@label2::url2"` (`http:`, `https:`, `anki:`) or plain labels separated by `@`; else `""`. |
| `lan` | Language code controlling card background color. | Lowercase 2-letter code: `en`, `es`, `pt`, `it`, or `de`. |
| `example_1` | Primary sentence (shown on *Recognition* front, blanked on *Production*). | Natural sentence containing the **exact `word`** (do NOT use `*` or manual blanks). |
| `example_2` | Optional second example on card backs. | Distinct sentence containing the **exact `word`** (no `*`), or `""`. |
| `example_3` | Optional third example on card backs. | Distinct sentence containing the **exact `word`** (no `*`), or `""`. |

## Critical Rules (`lan_1.1` vs legacy `lan_1.0`)

- **Never use `*` placeholders or ` @ ` in examples**: `lan_1.1` has three separate fields (`example_1`, `example_2`, `example_3`), and its JS automatically highlights `word` and replaces it with `_____` on `Production` front.
- **Exact `word` match**: Use the exact form from `word` inside `example_1..3` (inflected forms won't match the JS word-boundary regex).
- **Do not leak `word` in `definition`**: `definition` is visible on the `Production` front card.
- **Exact field spelling**: `menomics` (not `mnemonics`).
- **No Markdown**: Use HTML (`<b>`, `<i>`, `<u>`) only.

## Example

```json
{
  "modelName": "lan_1.1",
  "fields": {
    "word": "resilient",
    "trans_word": "resiliente / resistente",
    "rom": "/rɪˈzɪliənt/",
    "audio": "",
    "image": "",
    "menomics": "Re- (back) + salire (jump): bouncing back fast.",
    "definition": "Able to <b>recover quickly</b> from difficulties or setbacks.",
    "alt_trans": "adaptable::https://dictionary.cambridge.org/dictionary/english/adaptable@tough",
    "lan": "en",
    "example_1": "She remained resilient despite repeated setbacks.",
    "example_2": "A resilient system recovers gracefully from failure.",
    "example_3": "Resilient teams treat mistakes as feedback."
  },
  "tags": ["vocabulary", "en"]
}
```
