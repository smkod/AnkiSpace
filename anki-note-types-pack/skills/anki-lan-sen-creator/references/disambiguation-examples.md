# Disambiguation Playbook & Reference Examples (`lan_sen_1.1`)

Use this reference to calibrate answer determinability, avoid leakage, run the 3-alternative ambiguity check, and scale card design across CEFR A1–C2.

---

## 1. Before-and-After Case Studies (Examples A–F)

### Case A: Ambiguous Modal Expressions (`had better`)

- **Objective**: Communicative function — urgent advice implying a negative consequence.
- **❌ Before (Ambiguous)**:
  - `sentence`: `"We had better go now."` (`We _____ go now.`)
  - `target`: `"had better"` | `pattern`: `""` | `hint`: `""`
  - **Why it fails**: *should*, *must*, *could*, *might*, and *need to* are all grammatically valid and natural.
- **✅ After (Determinable)**:
  - `sentence`: `"We had better go now."`
  - `target`: `"had better"`
  - `pattern`: `"Modal idiom: strong advice implying a negative consequence + base verb"`
  - `hint`: `"Context: About to miss the last train; stranded if we don't leave immediately."`
- **Validation (3+ alternatives)**:
  1. *should* -> Grammatically valid, weaker pragmatically (does not convey the specific urgent-warning modal idiom cued in `pattern` + `hint`).
  2. *could* / *might* -> Semantically inappropriate (expresses possibility/suggestion, not urgent advice with a negative consequence).
  3. *must* -> Semantically different (obligation/necessity rather than modal-idiom advice).
  - **Verdict**: Pass — context + communicative intent isolate `had better` without leaking it.

---

### Case B: Over-Wide Conversational Blank (`go over that again`)

- **Objective**: Expression recall — phrasal verb *go over something again* (review/discuss one more time).
- **❌ Before (Ambiguous & Over-Wide)**:
  - `sentence`: `"Can we go over that again after the game?"` (`_____ after the game?`)
  - `target`: `"Can we go over that again"` | `pattern`: `""` | `hint`: `"Repetition request"`
  - **Why it fails**: Blank hides 6 words. *Could you explain that again*, *Can we talk about it again*, *Should we review it* all satisfy `"Repetition request"`.
- **✅ After (Scoped & Determinable)**:
  - `sentence`: `"Can we go over that again after the game?"`
  - `target`: `"go over that again"`
  - `pattern`: `"Modal request + phrasal expression: Can + subject + [verb + particle + object + 'again']?"`
  - `hint`: `"Expression: 'go over something again' — review or discuss something one more time"`
  - *(Alternative for pure phrasal-verb recall without naming `go over`)*: Shrink `target` to `"go over"` (`Can we _____ that again after the game?`) and set `hint` to `"Phrasal verb with 'go': review or discuss one more time"`.
- **Validation (3+ alternatives for `Can we _____ after the game?`)**:
  1. *review that* -> Semantically similar, but fails the phrasal-verb structure (`verb + particle + object + 'again'`) and target expression cue.
  2. *talk about it again* -> Wrong expression/verb-particle target.
  3. *repeat that* -> Invalid with explicit phrasal-expression pattern.
  - **Verdict**: Pass — shrinking `target` removes unrelated opener ambiguity (`Can we`) and focuses squarely on the target expression.

---

### Case C: Past Simple Conjugation (`arrived`)

- **Objective**: Grammar application — past simple conjugation of *arrive* with finished-time markers.
- **❌ Before (Ambiguous Verb Choice)**:
  - `sentence`: `"Paul and Lucy arrived ten minutes ago."` (`Paul and Lucy _____ ten minutes ago.`)
  - `target`: `"arrived"`
  - `pattern`: `"Subject + past simple verb + finished-time marker ('ago / yesterday / last year')"`
  - `hint`: `"Finished past time ('ten minutes ago')"`
  - **Why it fails**: The card tells the learner to use past simple, but gives no clue which verb to conjugate (*left*, *called*, *met*, *finished* are all equally valid).
- **✅ After (Determinable)**:
  - `sentence`: `"Paul and Lucy arrived ten minutes ago."`
  - `target`: `"arrived"`
  - `pattern`: `"Past simple with finished-time expressions (Subject + V2 + '... ago')"`
  - `hint`: `"Verb: arrive"`
- **Validation (3+ alternatives)**:
  1. *left* / *called* / *met* -> Invalid against `Verb: arrive`.
  2. *have arrived* -> Ungrammatical with finished-time marker `ten minutes ago` and `Subject + V2` pattern.
  3. *arrive* -> Ungrammatical (present simple with `ten minutes ago`).
  - **Verdict**: Pass — uniquely determines `arrived`.

---

### Case D: Polite Requests (`Could you`)

- **Objective**: Grammar application / specific modal construction (`Could you + base verb...?`).
- **❌ Before (Unconstrained Near-Synonyms)**:
  - `sentence`: `"Could you optimize this loop for better scalability?"` (`_____ optimize this loop for better scalability?`)
  - `target`: `"Could you"` | `pattern`: `""` | `hint`: `"Polite formal request"`
  - **Why it fails**: *Can you*, *Would you*, and *Would you be able to* all satisfy `"Polite formal request"`.
- **✅ After (Constrained Construction)**:
  - `sentence`: `"Could you optimize this loop for better scalability?"`
  - `target`: `"Could you"`
  - `pattern`: `"Polite request: modal verb + subject + base verb...?"`
  - `hint`: `"Complete the polite request using the modal 'could'"`
  - `explanation`: `"<b>Could you + base verb...?</b> is a standard polite request. <code>Would you</code> is an equally valid polite equivalent; <code>Can you</code> is slightly more casual; <code>Would you be able to</code> is more formal/tentative."`
- **Template Guard Note**: Keep `target` as `"Could you"` (not `"Could"`) if mentioning `'could'` in cues, and keep `'could'` in `hint` rather than `pattern` so `lan_sen_1.1`'s JS spoiler guard never hides `pattern`.
- **Alternative if modal choice isn't the point**: If the real learning goal is comparing register differences (*Can you* vs *Could you* vs *Would you be able to*), use a `Basic` card (`anki-basic-creator`) instead of forcing an artificial cloze.

---

### Case E: Meaning Clarification (`What do you mean by` / `mean by`)

- **Objective**: Communicative function — asking someone to clarify a term or expression.
- **❌ Before (Ambiguous Opener)**:
  - `sentence`: `"What do you mean by 'Lanchester's laws' in AoE?"` (`_____ 'Lanchester's laws' in AoE?`)
  - `target`: `"What do you mean by"` | `pattern`: `""` | `hint`: `"Meaning request"`
  - **Why it fails**: *Can you explain*, *Could you clarify*, and *What does ... refer to* work naturally.
  - **Leakage Trap to Avoid**: Putting `"What do you mean by + noun/phrase?"` verbatim inside `pattern` triggers `lan_sen_1.1`'s JS auto-hide (pattern vanishes completely!), and putting it verbatim inside `hint` leaks the entire answer!
- **✅ After — Option 1 (Tighter Blank, Zero Leakage)**:
  - `sentence`: `"What do you mean by 'Lanchester's laws' in AoE?"`
  - `target`: `"mean by"` (`What do you _____ 'Lanchester's laws' in AoE?`)
  - `pattern`: `"Clarification question: What + do/does + subject + [verb + prep] + term?"`
  - `hint`: `"Ask the speaker to clarify what they intend by a specific expression"`
- **✅ After — Option 2 (Full Construction, Abstract Skeleton)**:
  - `sentence`: `"What do you mean by 'Lanchester's laws' in AoE?"`
  - `target`: `"What do you mean by"`
  - `pattern`: `"Clarification construction: Wh-word + aux + subject + 'mean' + prep + [noun/phrase]?"` *(does NOT contain `"what do you mean by"`, so `pattern` stays visible)*
  - `hint`: `"Ask the speaker to clarify what they are referring to with a specific term"`
- **Validation (Option 1 alternatives for `What do you _____ 'Lanchester's laws' in AoE?`)**:
  1. *think about* -> Asks for an opinion, not clarification of meaning.
  2. *know about* -> Asks about prior knowledge, not clarification.
  3. *understand by* -> Asks for the listener's own interpretation, not what the speaker meant.
  - **Verdict**: Pass — zero leakage and tight determinability.

---

### Case F: Naturally Deterministic Grammar — Minimalism (`went`)

- **Objective**: Grammar application — irregular past simple of *go*.
- **✅ Good (Minimalist)**:
  - `sentence`: `"Yesterday, she went to the office."` (`Yesterday, she _____ to the office.`)
  - `target`: `"went"`
  - `pattern`: `"Past simple (irregular verb + finished-time marker)"`
  - `hint`: `"Verb: go"`
  - **Why it works**: No unnecessary story. Tense + base verb + `Yesterday` uniquely determine `went`.

---

## 2. CEFR A1–C2 Calibration Guide

| Level | Grammar / Function Focus | Disambiguation Strategy | Example (`pattern` / `sentence` / `hint`) |
| :--- | :--- | :--- | :--- |
| **A1** | Present simple `to be` / third-person `-s` | Base verb in `hint` + subject-number anchor in `sentence` | Pattern: `"Present simple (3rd person singular)"`<br>Sentence: `"My sister [lives] in Madrid."`<br>Hint: `"Verb: live"` |
| **A2** | Irregular past simple / basic prepositions of time | Finished-time marker in `sentence` + lemma in `hint` | Pattern: `"Past simple (irregular verb)"`<br>Sentence: `"Yesterday, she [went] to the office."`<br>Hint: `"Verb: go"` |
| **B1** | Present perfect (`for` vs `since`) / 1st conditional | Grammatical contrast in `pattern` + minimal `target` | Pattern: `"Present perfect + preposition before a starting point in time"`<br>Sentence: `"I have lived here [since] 2019."`<br>Hint: `"Preposition for a specific starting point (vs. duration)"` |
| **B2** | Modals of deduction / phrasal verbs / passive | Short situational context in `hint` + abstract `pattern` | Pattern: `"Modal idiom: strong advice implying a negative consequence + base verb"`<br>Sentence: `"We [had better] go now."`<br>Hint: `"About to miss the last train; stranded if we don't leave now."` |
| **C1** | Negative inversion / mixed conditionals | Abstract syntactic skeleton in `pattern` + tense cue in `hint` | Pattern: `"Inverted third conditional: Aux + subject + past participle"`<br>Sentence: `"[Had I known] earlier, I would have acted differently."`<br>Hint: `"Formal inversion omitting 'if' (verb: know)"` |
| **C2** | Subjunctive / concessive clauses / formal register | Register + syntactic cue in `pattern` + semantic anchor in `hint` | Pattern: `"Formal concession: Adjective/Adverb + 'as/though' + subject + verb"`<br>Sentence: `"[Try as he might], he couldn't reproduce the race condition."`<br>Hint: `"Formal concession meaning 'no matter how hard he tried' (verb: try)"` |

---

## 3. When to Reject Cloze & Switch Note Type

Reject `lan_sen_1.1` and switch note types when disambiguation forces an artificial or trivial prompt:

| Problem | Better Note Type | Example |
| :--- | :--- | :--- |
| Testing *why* or *when* to choose one tense/modal over another (`should` vs `had better` vs `ought to`) | `Basic` / `Basic_Custom` (`anki-basic-creator`) | Front: `"When should you choose 'had better' instead of 'should'?"` -> Back: `"When giving urgent advice or warning of a negative consequence in a specific situation."` |
| Testing isolated word recall from a definition (`resilient`, `alleviate`) | `lan_1.1` (`anki-lan-creator`) | Single-word vocabulary note with `definition` + blanked `example_1` (`Production` card). |
| Multiple genuinely equivalent phrasings cannot be distinguished without giving away the answer word-for-word | `Basic` (`anki-basic-creator`) | Front: `"Give a natural polite request opener to ask a teammate to review a PR."` -> Back: `"Could you... / Would you mind + -ing... / Would you be able to..."` |
