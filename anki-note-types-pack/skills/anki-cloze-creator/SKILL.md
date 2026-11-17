---
name: anki-cloze-creator
description: >
  Creates Cloze deletion Anki cards using the custom Cloze (or Cloze_Custom) note type strictly for literal/verbatim memorization (commands, verses, quotes, exact syntax).
  Trigger: When creating Anki cards for CLI commands, exact code syntax, Bible verses, quotes, or formulas requiring verbatim recall.
license: Apache-2.0
metadata:
  author: BlackLion_s99
  version: "2.0"
---

# Anki Cloze Creator (`Cloze` / `Cloze_Custom`)

Creates Cloze cards **exclusively for literal / verbatim recall** where exact wording, flags, or token order matters.

## When to Use (Strict)

- CLI commands, flags, and exact arguments (e.g., `git remote prune origin`)
- Exact code syntax, regex tokens, or API signatures that must be typed from memory
- Bible verses, quotes (*citas*), laws, or exact formulas
- **Do NOT use** for conceptual understanding, definitions, or general study notes — use `anki-basic-creator` (`Basic`) instead.

## Field Mapping & AI Instructions

| Field | Purpose | AI Population Rule |
| :--- | :--- | :--- |
| `Text` | Verbatim text with `{{c1::...}}` deletions. | Cloze only the exact tokens to recall verbatim (avoid `::hint` unless disambiguation is essential). HTML only (`<code>`, `<pre>`, `<b>`, `<br>`). |
| `Back Extra` | Legacy/editor-only note field (NOT rendered by template). | Leave `""`. Put visible back explanations or code in `Extra` instead. |
| `Audio` | Optional `[sound:...]` rendered directly on back. | Leave `""` unless attaching a valid `[sound:...]` file. Never paste plain text here. |
| `Mode` | Optional footer color-dot category indicator. | One lowercase code (`c`, `p`, `b`, `g`, `lg`, `y`, `r`, `gy`) or `""`. *(Note: `o` falls back to transparent in `Cloze` CSS.)* |
| `Extra` | Optional explanation, context, or code box on back. | Add brief usage notes or `<pre><code class="language-LANG">...</code></pre>` (HTML only), or `""`. |

## Critical Formatting Rules

- **No Markdown**: Always use literal HTML (`<code>`, `<pre>`, `<b>`, `<i>`, `<br>`).
- **Minimal Clozes**: Keep clozes surgical (`{{c1::...}}`, `{{c2::...}}`) so each blank tests a real token rather than hiding an entire paragraph.
- **Do Not Use `Back Extra`**: The `Cloze` back template renders `{{Extra}}`, not `{{Back Extra}}`.
- **Note Type Name**: Check `anki_list_note_types` first; use `"Cloze"` or `"Cloze_Custom"` depending on the user's profile.

## Example

```json
{
  "modelName": "Cloze",
  "fields": {
    "Text": "Remove stale remote-tracking branches no longer on origin:<br><code>git {{c1::remote}} {{c2::prune}} {{c3::origin}}</code>",
    "Back Extra": "",
    "Audio": "",
    "Mode": "g",
    "Extra": "Keeps <code>git branch -a</code> clean without deleting your local feature branches."
  },
  "tags": ["git_commands", "cli"]
}
```
