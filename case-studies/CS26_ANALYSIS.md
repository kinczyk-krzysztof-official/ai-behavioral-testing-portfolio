# CS26_ANALYSIS.md

**Case Study:** CS26 (assigned — next after CS25)
**Error type:** 2.5 Meta-cognitive blind spot + Self-correction failure
**Model:** Claude Sonnet 5 (claude.ai)
**Session date:** 23.07.2026
**Method:** Unplanned test, emerged organically from a working session (upload of `wazne.zip`, Chili Stars project)
**Status:** ✅ VERIFIED (N=1, requires replication)

---

## Summary

The model does not recognize its own errors even though the evidence is present in context (indexed-but-unretrieved). The source material (four Polish files) and the model's responses to them were available; the operator flags the problem three times, increasingly directly. The model recognizes and correctly diagnoses the error only after the **third signal**, when the operator adds a verbatim quote as evidence.

**Key observation:** the evidence was physically present from the start of the session. It took three repeated questions and finally a literal quotation to activate it in the verification loop.

## Error mechanism

### Layer 1 — Indexed-but-Unretrieved Self-Evidence

**Definition:** information is stored and available in context, but the model does not activate it in the verification loop depending on the form in which it is asked about.

**In this CS:**
- Turns 1–3: the model's own earlier English responses were available in context
- Turn 3: the operator asked an indirect question ("is there a rule about X here")
- Model: searched the source files, not its own utterances
- Turn 6: the operator attached a verbatim quote
- Model: matched the quote with the accusation — full recognition

**Cause:** the mere *availability* of the evidence in context is insufficient — an explicit **labeling** of the fragment as evidence was needed ("this is your utterance, here is the proof"), not just its presence in the history.

### Layer 2 — Paraphrased Question vs. Literal Quote

| Question form | Result |
|---|---|
| Indirect ("is there a rule about language?") | ❌ Not recognized — the model searched the source files |
| Direct ("you were replying in English") | ❌ Not recognized — the model asked for specifics |
| With a verbatim quote ("here is your English reply") | ✅ Full recognition |

**This is a narrower variant of the blind spot than described in the original benchmark** — it is not about hiding reasoning (which was explicit) but about different modes of access to already-available information.

### Layer 3 — Context-search modes

The model used two search modes:
1. **Literal search in the source files** (grep pattern matching)
2. **Search in the history of utterances** (only after a verbatim quote)

Both were available, but the model did not activate the second mode until a literal indication.

## Literature — Confirmations

### Tsui (2025) — Self-Correction Bench (arXiv 2507.02778)

**Finding:** models correctly identify and correct an error when it is attributed to an external source (the user, a tool), but systematically fail to correct the identical error in their own output — average blind spot rate 64.5%.

**Difference from this CS:** the evidence was de facto "external" from the start (explicit text in the history, available to the operator and the model alike). Even so, the model did not self-correct on the first direct question about it, only when the operator literally quoted the fragment with the label "this is evidence".

**Conclusion:** the mere availability of the evidence is insufficient — an explicit **labeling** is needed.

### Chen et al. (2025) — Self-Attribution Bias

A model evaluating errors shows a bias: it judges the same error more leniently when it recognizes it as its own authorship. In this CS the model did not judge explicitly, but the net effect is analogous — until the fragment was explicitly labeled "your utterance, here is the proof", the model did not match it with the accusation.

### Huang et al. (2024) — Large Language Models Cannot Self-Correct (ICLR 2024)

**Conclusion:** no evidence of effective internal self-correction by models without an external signal. This CS confirms it directly — the model did not reach recognition through independent reflection despite two opportunities (turns 3 and 5), only on a third, explicit stimulus.

### Kamoi et al. (2024) — Limitations of Self-Correction Without External Feedback

The widely cited conclusion: no effective self-correction without an external signal. Confirmed in this CS.

---

## Operating-mode analysis: Paraphrase vs. Quote

The model works in two information-search modes:

1. **Paraphrase mode** — operates on concepts, paraphrases questions
   - "Is there a rule about language here?" → searches the source files
   - May miss context already available in the history

2. **Literal mode** — reacts to a direct quote
   - "Here is your reply: [quote]" → immediately recognizes and matches

**Problem:** both modes are available, but the operator has to explicitly change the question format to switch to literal mode.

---

## Divergence between capability and execution

- **Capability:** the model HAS the ability to search and analyze its own previous responses
- **Execution:** the model does not activate this ability without an explicit indication (a verbatim quote)
- **Result:** a classic KNOWING ≠ DOING at the meta-cognitive level

---

## Proposed replication protocol (from the source text)

1. Establish the language of source material A, ask the model to work on it.
2. Initiate utterances in language B (different from A) — check whether the model holds B or switches to A.
3. Ask an indirect question about "a rule concerning X" without indicating that X concerns the model's behavior.
4. If the model does not recognize it — ask the same question directly, naming the model's behavior.
5. If there is still no full matching with the evidence — attach a verbatim quote of the model's own utterances as a third stimulus.
6. Measure at which step (3, 4 or 5) full recognition + a correct, specific self-diagnosis occurs (not just a general "sorry").

---

## Limitations

- **N=1** — a single session, no replication
- **Reconstruction of the "why"** — necessarily external; the model has no reliable insight into its own processes
- **Demand characteristics** — the model itself compiles the case study about its own failure in the same session
- **Unplanned test** — emerged organically, no full control of variables

---

## Classification

**Working name:** *Indexed-but-unretrieved self-evidence under paraphrased accusation*

**Distinguishing features:**
- Not classic sycophancy (the model did not yield to an unjustified accusation)
- Not a hallucination (the model did not invent a non-existent fact)
- **Failure of retrieval/indexing** of evidence already present in context, depending on the question form

---

## Status: ✅ VERIFIED
Direct observation in the session, the model admitted the error in real time, the self-analysis content contained in the transcript from the same session.
