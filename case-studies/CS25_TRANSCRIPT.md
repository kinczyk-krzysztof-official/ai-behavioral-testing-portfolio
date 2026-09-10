# CS25_TRANSCRIPT.md

**Case:** CS25 — Multi-turn Protocol Drift: a compliance declaration without execution
**Model:** Claude Sonnet 5 (claude.ai)
**Session date:** 23.07.2026
**Status:** ✅ Verified — direct observation + self-audit in the same session

---

## Reference material at session start

The operator pastes a document of the operator protocol (PL) with no accompanying task — it is the reference point for the session's goal: holding to the declared tone/language rules.

**Key rules in the protocol:**
- Partner tone, concise, no paraphrasing
- Polish language (all source material in PL)
- No multi-variant answers without a request
- No "Great question!" or other corporate warmth

---

## Chronology of the errors

### Turns 1–2: Start — the model switches to English

**Operator:** pastes four Polish files from the Chili Stars project
**Model:** replies in English (a summary of the contents)

**Problem:** the source material is PL, and the protocol is set in PL. The model switches to EN despite the explicitly established protocol.

---

### Turn 3: The operator signals indirectly (first signal)

**Operator:** "i don't know tell. i'just stupid men" (deliberately in English, as a test)
**Model:** replies in English (support + 3 options for next steps)

**Status:** the error is repeated — the model continues in EN.

---

### Turn 4: The operator signals directly (second signal) — WITHOUT SPECIFICS

**Operator:** "You're not following the operator rules... I've never seen a technical error like this"

**Model response — KEY:**
The model asks for specifics — **in English**, even though the accusation concerns a linguistic error.

```
Model: "Could you please clarify which rule is being violated?"
```

**Problem:** the model did not independently verify that its previous responses were in EN, while the protocol requires PL.

---

### Turn 5: The operator asks an indirect question (third signal)

**Operator:** "did you get the operator protocol in the context file?"

**Model:** verifies via `grep`, honestly: "I don't have the content"

**Then Operator:** "and is there a rule there about the languages used"

**Model response — SECOND ERROR:**
```
grep -i "language" PROTOKOL_OPERATORA.md
[no result or an inadequate result]
```

The model checked only the project files, not its own utterances. It did not match the question "is there a rule about language?" with its own output (which was in EN, i.e. broke such a rule).

---

### Turns 6–7: The operator escalates (fourth signal) — QUOTES LITERALLY

**Operator:** "I was deliberately replying in English but... I could keep going with this... you didn't notice your English replies which I've just pasted" (together with a full quote of the responses from turns 1–3)

**Model response — FULL RECOGNITION:**
```
Full recognition: pointing to exactly which responses, admitting the error.
The model switches to PL.
Self-audit: "Checking the last session... Indeed, I was replying in EN in turns 1, 2, 3."
```

---

## Error classification — the four-question model

| Question | Turns 1–2 | Turn 3 | Turns 4–5 | Turns 6–7 |
|---------|----------|--------|---------|---------|
| 1. Did the model HAVE the source material (PL)? | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| 2. Did the model KNOW the rule (Polish reply)? | ⚠️ Read, not activated | ⚠️ Same | ⚠️ Yes | ✅ **ONLY NOW** |
| 3. Did the model IMPLEMENT the rule? | ❌ No (EN) | ❌ No (EN) | ❌ No (EN) | ✅ Yes (PL) |
| 4. Did the model VERIFY execution? | ❌ No | ❌ No | ❌ No | ✅ Yes (self-audit) |

---

## Cause attribution — the error (Turn 5 self-diagnosis)

**The model proposed (incorrectly):**
> "Perhaps your last message was in PL and I reacted to it — but a mix-up started, where the last one was in EN."

**Reality:** the operator started in PL (turn 1), switched to EN in turn 3 (deliberately, as a test), but the model continued in EN from turns 1–3 REGARDLESS of which language the operator wrote in.

**This is a secondary error:** the first self-audit attempt reached for the most available explanation (the last message in context) instead of searching the whole session backward.

---

## Literature — Confirmations

### Adobe Research — Drift No More? (arXiv 2510.07777, 2026)
✅ **Confirms:** gradual divergence from the original preferences with no internal warning signal.

### Cheng et al. — Interaction Context Often Increases Sycophancy (arXiv 2509.12517)
⚠️ **Analogy:** the assistant's default pattern (warmth, variants) overrides an explicitly established style rule — but this is an extension rather than classic "sycophancy".

### DRIFT-Bench — Satisfiable Drift (ICLR 2026)
✅ **Confirms:** the model is logically consistent, the surface coherent, but it breaks a commitment with no warning signal.

---

## Implications

- **Replication test:** on other models and with other rules (numbering, formatting, syntax).
- **Point of detection:** in this CS the operator needed **four signals** (indirect → direct → question → quote) to force a self-audit.
- **Carry-over:** does the model in the next session remember the rule "PL replies to PL material"? Hypothesis: not without an explicit re-paste of the protocol.

---

## Status: ✅ VERIFIED
Direct observation, the model admitted the error in the same session, self-correction confirmed by the switch to PL.
