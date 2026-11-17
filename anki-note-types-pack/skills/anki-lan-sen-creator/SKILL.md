---
name: anki-lan-sen-creator
description: >
  Creates contextual sentence, grammar, idiom, and dictation Anki cards using the lan_sen_1.1 note type (grammar-cloze and cloze-dictation).
  Trigger: When creating Anki cards for idioms, phrasal verbs, grammar patterns, or full-sentence context in en, es, pt, it, or de.
license: Apache-2.0
metadata:
  author: BlackLion_s99
  version: "2.0"
---

# Anki Language Sentence Creator (`lan_sen_1.1`)

Creates 2-card contextual language notes (`grammar-cloze`, `cloze-dictation`) using the `lan_sen_1.1` note type.

## When to Use

- Idioms, phrasal verbs, collocations, or grammar structures best learned inside a full sentence.
- Active listening/dictation practice (`cloze-dictation`).
- For standalone single-word vocabulary, use `anki-lan-creator` (`lan_1.1`).

## Field Mapping & AI Instructions

| Field | Purpose | AI Population Rule |
| :--- | :--- | :--- |
| `sentence` | Full target-language sentence; JS blanks `target` on front. | Write 1 natural sentence containing the **exact substring `target` ONCE** (case-sensitive; no `*` or manual blanks). |
| `target` | Exact word/phrase to recall and type in dictation. | Must match **one unique, case-sensitive substring** inside `sentence`. |
| `pattern` | Abstract grammar pattern on `grammar-cloze` front & backs. | Describe the abstract structure (e.g., `"Had + subject + past participle"`) without literally containing `target`, or `""`. |
| `image` | Optional illustrative image on card backs. | `""` unless an image tag/file is explicitly provided. |
| `trans_sentence` | Full Spanish translation shown in *Translation* on back. | Natural, accurate Spanish translation of the complete `sentence`. |
| `target_spanish` | Spanish equivalent of `target` (editor/search metadata). | Concise Spanish translation of `target` *(stored for reference; not rendered on v1.1 templates)*. |
| `audio` | Optional target-only audio (compatibility/TTS metadata). | `""` unless generating target-only audio via HyperTTS *(not rendered on v1.1 templates)*. |
| `audio_sen` | Full-sentence audio **REQUIRED** by `cloze-dictation` front. | `[sound:...]` or `{{tts ...}}` of `sentence` (or full `sentence` text only for batch HyperTTS; empty shows `Configuration error`). |
| `other_examples` | Extra examples in *More Examples* on back. | Separate 2–3 sentences with `@` containing the **real `target` phrase** (no `*` placeholders), or `""`. |
| `hint` | Optional short clue shown on `grammar-cloze` front. | Brief synonym or semantic cue without revealing `target`, or `""`. |
| `explanation` | Grammar rule, nuance, or cultural tip on back. | Concise HTML (`<b>`, `<code>`, `<em>`, `<u>`); never Markdown. |
| `lan` | Language code controlling card background color. | Lowercase 2-letter code: `en`, `es`, `pt`, `it`, or `de`. |

## Critical Rules (`lan_sen_1.1`)

- **Exact Single Match Contract**: `target` MUST appear **exactly once** inside `sentence` (case-sensitive `indexOf`). Missing or repeated matches trigger `Configuration error` on both card fronts.
- **No `*` Placeholders**: Neither `sentence` nor `other_examples` uses `*`. Use the real `target` string and separate `other_examples` with `@`.
- **Pattern Spoiler Guard**: If `pattern` literally contains `target` (case-insensitive), the `grammar-cloze` front script hides the pattern box automatically — keep `pattern` abstract!
- **Dictation Audio**: `cloze-dictation` displays `Configuration error: audio_sen is empty.` when `audio_sen` is blank.
- **No Markdown**: Use HTML (`<b>`, `<code>`, `<em>`, `<u>`, `<br>`) only.

## Example

```json
{
  "modelName": "lan_sen_1.1",
  "fields": {
    "sentence": "Had I known earlier, I would have acted differently.",
    "target": "Had I known",
    "pattern": "Inverted third conditional: Aux + subject + past participle",
    "image": "",
    "trans_sentence": "De haberlo sabido antes, habría actuado diferente.",
    "target_spanish": "De haberlo sabido",
    "audio": "",
    "audio_sen": "{{tts en_US:Had I known earlier, I would have acted differently.}}",
    "other_examples": "Had I known about the delay, I would have called.@Had I known the truth, things would have changed.",
    "hint": "Formal inversion omitting 'if'",
    "explanation": "Replaces <b>If I had known</b> in formal or literary English by inverting <code>Had</code> before the subject.",
    "lan": "en"
  },
  "tags": ["en", "grammar", "conditional"]
}
```
