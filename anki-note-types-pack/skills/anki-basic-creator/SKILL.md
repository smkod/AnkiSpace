---
name: anki-basic-creator
description: >
  Creates atomic Anki cards using the custom Basic (or Basic_Custom) note type for concepts, definitions, key-value facts, and situational knowledge.
  Trigger: When creating conceptual, analytical, definitional, or key-value Anki flashcards (anything not requiring verbatim memorization).
license: Apache-2.0
metadata:
  author: BlackLion_s99
  version: "2.0"
---

# Anki Basic Creator (`Basic` / `Basic_Custom`)

Creates fast-review (<10s), atomic cards for conceptual understanding, definitions, comparisons, tradeoffs, and key-value facts.

## When to Use

- Conceptual understanding, mental models, and architectural principles
- Definitions, key-value facts (ports, HTTP codes), and cause-effect rules
- Situational or behavioral takeaways
- **Do NOT use** for verbatim commands, quotes, or verses — use `anki-cloze-creator` for literal recall.

## Field Mapping & AI Instructions

| Field | Purpose | AI Population Rule |
| :--- | :--- | :--- |
| `Front` | Question, concept prompt, or cue on card front. | Write 1 atomic prompt (<10s recall). Optionally prefix with `<t>Topic \| Subtopic</t><br>`. HTML only (`<b>`, `<code>`, `<em>`). |
| `Back` | Direct, unambiguous answer on card back. | Lead with the core answer using `<strong>` and `<code>`. Add optional nuance via `<br><em>note</em>`. HTML only. |
| `Mnemonic` | Optional memory peg, analogy, or visual cue. | Fill only when a sharp, vivid peg or short anchor phrase helps; otherwise `""`. |
| `Audio` | Optional audio (`[sound:...]`) or TTS marker on back. | Leave `""` unless attaching `[sound:...]` or running a batch TTS workflow. Never paste raw `Back` text here. |
| `Mode` | Optional footer color-dot category indicator. | One lowercase code (`c`, `p`, `b`, `g`, `lg`, `y`, `o`, `r`, `gy`) matching the deck/domain color, or `""`. |
| `Extra` | Optional context, `<img>`, or code block on back. | Wrap code in `<pre><code class="language-LANG">...</code></pre>` (HTML-escaped) or add brief context; else `""`. |

## Critical Formatting Rules

- **No Markdown**: Anki does not render Markdown. Use HTML (`<strong>`, `<b>`, `<code>`, `<em>`, `<br>`, `<ul><li>`).
- **Topic Pill**: Prefix `Front` with `<t>Domain | Subtopic</t><br>` for instant context without cluttering the question.
- **Note Callout**: `<br><em>...</em>` in `Back` automatically renders as a styled muted explanatory line.
- **Code Blocks**: Escape `<` / `>` inside `<pre><code class="language-LANG">...</code></pre>` so Highlight.js renders cleanly.
- **Note Type Name**: Check `anki_list_note_types` first; use `"Basic"` or `"Basic_Custom"` depending on the user's profile.
- **Tags**: Use lowercase tags (`Obsidian_to_Anki` is auto-hidden in the card header).

## Example

```json
{
  "modelName": "Basic",
  "fields": {
    "Front": "<t>Architecture | Idempotency</t><br>Why do payment endpoints require an <code>Idempotency-Key</code> header?",
    "Back": "To prevent <strong>duplicate charges</strong> when a client safely retries a timed-out request.<br><em>The server caches the first response keyed by client token and replays it on retries.</em>",
    "Mnemonic": "Same key, same receipt — never charge twice.",
    "Audio": "",
    "Mode": "g",
    "Extra": "<pre><code class=\"language-http\">POST /v1/charges\nIdempotency-Key: 9b1deb4d-3b7d-4bad-9bdd-2b0d7b3dcb6d</code></pre>"
  },
  "tags": ["architecture", "api"]
}
```
