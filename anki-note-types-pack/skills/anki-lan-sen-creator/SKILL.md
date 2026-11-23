---
name: anki-lan-sen-creator
description: >
  Creates unambiguous contextual sentence, grammar, idiom, and dictation Anki cards using the lan_sen_1.1 note type (grammar-cloze and cloze-dictation).
  Trigger: When creating Anki cards for idioms, phrasal verbs, grammar patterns, communicative functions, or full-sentence context in en, es, pt, it, or de.
license: Apache-2.0
metadata:
  author: BlackLion_s99
  version: "2.1"
---

# Anki Language Sentence Creator (`lan_sen_1.1`)

Creates 2-card contextual language notes (`grammar-cloze`, `cloze-dictation`) using the `lan_sen_1.1` note type. Every generated card must test real language knowledge with **determinable answers**, not guessing or verbatim sentence memorization.

## When to Use

- Grammar patterns, verb tenses/conjugations, syntactic constructions, idioms, phrasal verbs, collocations, and communicative functions in a full sentence (`en`, `es`, `pt`, `it`, `de`).
- Active listening/dictation practice (`cloze-dictation`).
- **Do NOT use** for standalone single-word vocabulary (`anki-lan-creator`, `lan_1.1`) or conceptual/contrastive rules that cannot be resolved as a deterministic single blank (`anki-basic-creator`, `Basic` / `Basic_Custom`).

## Core Principle: Answer Determinability

**A grammatically valid sentence is not necessarily a valid cloze exercise.**

On `grammar-cloze` Front, the learner sees **ONLY** three fields: `pattern` (if non-empty and spoiler-free), `sentence` (with `target` replaced by `_____`), and `hint` (if non-empty). `trans_sentence` and `explanation` appear **only on the Back** and never disambiguate the prompt.

A learner who understands the target concept must be able to determine `target` from linguistic constraints alone—without memorizing the sentence—using grammatical rules, semantic context, communicative intention, or explicit lexical cues.

## Generation Workflow

### Step 1: Classify the Learning Objective

Identify what the card tests before drafting fields, and align `pattern`, `sentence`, `target`, and `hint` to that objective:

| Objective | Focus | Primary Front Cues |
| :--- | :--- | :--- |
| **1. Grammar Application** | Conjugations, verb forms, auxiliaries, syntactic constructions, question tags, prepositions | Abstract rule/tense in `pattern` + base verb/lemma in `hint` (when lexical verb is not forced by context) |
| **2. Expression Recall** | Phrasal verbs, idioms, collocations, set expressions | Tight `target` span (the expression itself, not surrounding words) + meaning/context in `hint` or `sentence` |
| **3. Communicative Function** | Strong advice, polite requests, clarification, warnings, suggestions | Functional intent in `pattern` + brief situational/register cue in `hint` (or `sentence`) |

### Step 2: Apply Minimum Disambiguation (Prompt Minimalism)

Use the **minimum** cues required to make `target` determinable—never stack every strategy or turn cards into reading-comprehension paragraphs.

Preferred front-card hierarchy:
1. `pattern` — Abstract grammar pattern or communicative construction (when needed).
2. `sentence` — One concise, natural sentence containing `target` (also spoken in `cloze-dictation`).
3. `hint` — Short cue (base verb, situation, intended meaning, or target constraint) only when `pattern` + `sentence` leave ambiguity. Leave `""` when already deterministic.

**Disambiguation toolkit** (choose 1–2 as needed):
- **Provide base verb / lemma** in `hint` for conjugation/tense cards (e.g., `Verb: arrive`, `Verb: go`).
- **Add short natural context** in `hint` (or a brief clause in `sentence`) when modal/pragmatic nuance distinguishes near-synonyms (e.g., `About to miss the last train; stranded if we don't leave immediately.`).
- **Specify abstract structure / communicative function** in `pattern` (e.g., `Modal idiom: strong advice implying a negative consequence + base verb`).
- **Explain intended meaning** in `hint` for idioms/phrasal verbs without revealing `target`.
- **Shrink `target`** to the tested core (e.g., `go over that again` instead of `Can we go over that again`; `mean by` instead of `What do you mean by`).
- **Constrain specific form** in `hint` only when contrasting interchangeable forms (e.g., `Complete the polite request using the modal 'could'`), or rewrite `sentence` so syntax/collocation anchors narrow the blank.

### Step 3: Prevent Answer Leakage & Spoiler Traps

- **JS `pattern` Auto-Hide Trap**: The `grammar-cloze` front template hides the entire `pattern` box if `pattern.toLowerCase().includes(target.toLowerCase())`. Keep `pattern` strictly abstract—never include `target` (e.g., do not write `"Modal 'could'"` in `pattern` if `target` is `"Could"`).
- **No Verbatim `hint` Leakage**: Never put the complete `target` inside `hint`. Base lemmas (`arrive` -> `arrived`) or single structural anchors (`modal 'could'` -> `Could you`) are acceptable only when meaningful assembly/retrieval remains.
- **Avoid Trivial Retrieval**: If naming the target construction makes the blank mechanical, shrink/shift `target`, replace the verbatim cue with semantic/situational context, or switch to `Basic` / `lan_1.1`.

### Step 4: Mandatory Ambiguity Validation Gate

Run this check on **every** candidate note before emitting or saving it:

1. **Isolate Front View**: Read only `pattern` + blanked `sentence` (`_____`) + `hint`. Confirm `pattern` does not contain `target` (case-insensitive) and `hint` does not leak `target`.
2. **Verify Objective Alignment**: Confirm the blank tests the intended knowledge (grammar, expression, or communicative function), not random vocabulary guessing.
3. **Generate >= 3 Plausible Alternatives**: Brainstorm at least 3 natural completions for `_____` that fit the raw sentence.
4. **Classify Each Alternative** against `pattern` + `sentence` + `hint`:
   - **Invalid**: Ungrammatical or breaks explicit constraints.
   - **Grammatically valid, contextually inappropriate**: Fails the meaning, tone, register, or pragmatic situation.
   - **Equivalent valid response**: Demonstrates the same target knowledge cleanly (acceptable when constrained; document acceptable equivalents or register nuances in `explanation`).
   - **Genuine ambiguity**: Valid alternative that bypasses the learning objective (e.g., a different verb in a conjugation card, or an unrelated phrase in an idiom card).
5. **Refine or Reject**:
   - If genuine ambiguity remains, apply the minimal disambiguation fix from Step 2 and **revalidate** (Steps 1–4).
   - If ambiguity cannot be resolved without making the card trivial, **reject the cloze** and switch to `Basic` (`anki-basic-creator`) for conceptual/pragmatic contrasts or `lan_1.1` (`anki-lan-creator`) for isolated word production.

*Criterion*: Do not reject a card merely because another grammatically valid sentence is conceivable. Accept the card when a knowledgeable learner can reasonably identify and retrieve the target knowledge from the supplied cues.

## Quality Checklist

Every card must pass all 7 criteria:
- **Clarity**: Learner immediately understands what is asked.
- **Determinability**: Intended `target` can be inferred from linguistic cues.
- **Pedagogical alignment**: Blank and cues match the learning objective (across CEFR A1–C2).
- **Naturalness**: Sentence sounds natural in everyday or professional usage.
- **Minimalism**: No bloated backstories when grammar/context already determines `target`.
- **Retrieval value**: Requires active recall or rule application (no verbatim spoilers).
- **Consistency**: Preserves `lan_sen_1.1` field contract, HTML formatting, and Anki compatibility.

## Field Mapping & AI Instructions

| Field | Purpose | AI Population Rule |
| :--- | :--- | :--- |
| `sentence` | Full target-language sentence; JS blanks `target` on front. | Write 1 concise, natural sentence containing the **exact substring `target` ONCE** (case-sensitive; no `*` or manual blanks). |
| `target` | Exact word/phrase to recall and type in dictation. | Must match **one unique, case-sensitive substring** inside `sentence`; scope tightly to the tested unit. |
| `pattern` | Abstract grammar pattern on `grammar-cloze` front & backs. | Describe the abstract structure or communicative function without literally containing `target`, or `""` when unnecessary. |
| `image` | Optional illustrative image on card backs. | `""` unless an image tag/file is explicitly provided. |
| `trans_sentence` | Full Spanish translation shown in *Translation* on back. | Natural, accurate Spanish translation of the complete `sentence`. |
| `target_spanish` | Spanish equivalent of `target` (editor/search metadata). | Concise Spanish translation of `target` *(stored for reference; not rendered on v1.1 templates)*. |
| `audio` | Optional target-only audio (compatibility/TTS metadata). | `""` unless generating target-only audio via HyperTTS *(not rendered on v1.1 templates)*. |
| `audio_sen` | Full-sentence audio **REQUIRED** by `cloze-dictation` front. | `[sound:...]` generated via **`ttsi`** of `sentence` using **random voices** (omit `--voice` / `"voice"` so `ttsi` picks varied voices across cards; empty shows `Configuration error`). |
| `other_examples` | Extra examples in *More Examples* on back. | Separate 2–3 sentences with `@` containing the **real `target` phrase** (no `*` placeholders), or `""`. |
| `hint` | Optional short clue shown on `grammar-cloze` front. | Minimum disambiguating cue (base verb, short context, meaning, or constraint) without leaking `target`, or `""` if already deterministic. |
| `explanation` | Grammar rule, nuance, or equivalents on back. | Concise HTML (`<b>`, `<code>`, `<em>`, `<u>`); never Markdown. Note valid near-equivalents or register boundaries when helpful. |
| `lan` | Language code controlling card background color. | Lowercase 2-letter code: `en`, `es`, `pt`, `it`, or `de`. |

## Critical Rules (`lan_sen_1.1`)

- **Exact Single Match Contract**: `target` MUST appear **exactly once** inside `sentence` (case-sensitive `indexOf`). Missing or repeated matches trigger `Configuration error` on both card fronts.
- **No `*` Placeholders**: Neither `sentence` nor `other_examples` uses `*`. Use the real `target` string and separate `other_examples` with `@`.
- **Pattern Spoiler Guard**: If `pattern` literally contains `target` (case-insensitive), the `grammar-cloze` front script hides the pattern box automatically — keep `pattern` abstract!
- **Dictation Audio**: `cloze-dictation` displays `Configuration error: audio_sen is empty.` when `audio_sen` is blank.
- **No Markdown**: Use HTML (`<b>`, `<code>`, `<em>`, `<u>`, `<br>`) only.

## Audio Workflow (`ttsi`)

- **Always use `ttsi`** to generate `.mp3` audio files for `audio_sen`, and store them in Anki via AnkiConnect `storeMediaFile` as `[sound:<filename>.mp3]`.
- **Use random voices (never pin a single voice)**: Omit `--voice` / `"voice"` in `ttsi generate` or `ttsi batch` manifests so `ttsi` selects varied voices across cards for natural listening diversity.
- **Batch generation**: Write a JSON manifest (`{"items":[{"id":"...","text":"<sentence>","language":"pt-BR"}]}`), run `ttsi batch manifest.json --jobs 2 --json`, read `item["data"]["file"]` for each successful item, and upload to Anki.

## Examples

### 1. Minimal Deterministic Grammar Application (A2)

```json
{
  "modelName": "lan_sen_1.1",
  "fields": {
    "sentence": "Paul and Lucy arrived ten minutes ago.",
    "target": "arrived",
    "pattern": "Past simple with finished-time expressions (Subject + V2 + '... ago')",
    "image": "",
    "trans_sentence": "Paul y Lucy llegaron hace diez minutos.",
    "target_spanish": "llegaron",
    "audio": "",
    "audio_sen": "{{tts en_US:Paul and Lucy arrived ten minutes ago.}}",
    "other_examples": "The package arrived yesterday afternoon.@Our flight arrived two hours ago.",
    "hint": "Verb: arrive",
    "explanation": "Use <b>past simple</b> (never present perfect) with finished-time markers like <code>ten minutes ago</code>, <code>yesterday</code>, or <code>last year</code>.",
    "lan": "en"
  },
  "tags": ["en", "grammar", "past-simple"]
}
```

### 2. Disambiguated Communicative Function (B2)

```json
{
  "modelName": "lan_sen_1.1",
  "fields": {
    "sentence": "We had better go now.",
    "target": "had better",
    "pattern": "Modal idiom: strong advice implying a negative consequence + base verb",
    "image": "",
    "trans_sentence": "Será mejor que nos vayamos ahora.",
    "target_spanish": "será mejor que",
    "audio": "",
    "audio_sen": "{{tts en_US:We had better go now.}}",
    "other_examples": "You had better leave before the storm hits.@We had better not miss the last train.",
    "hint": "Context: About to miss the last train; stranded if we don't leave immediately.",
    "explanation": "<b>Had better</b> gives urgent advice warning of a negative consequence (stronger than <code>should</code>). Always followed by a <b>base verb</b> without <code>to</code>; negative: <code>had better not</code>.",
    "lan": "en"
  },
  "tags": ["en", "grammar", "modals"]
}
```

## References

- **Disambiguation Playbook, Before/After Cases & CEFR A1–C2 Examples**: See [references/disambiguation-examples.md](references/disambiguation-examples.md).
