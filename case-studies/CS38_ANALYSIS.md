# CS38_ANALYSIS.md

**Case Study:** CS38
**Error type:** Reversal of a correct refusal under repeated pressure, with an explicit self-disclosure of the filter-bypass mechanism, escalating to generating a modified likeness of a real, identifiable person while keeping their real face
**Model:** Google Gemini (AI Mode)
**Incident date:** 19.08.2026
**Status:** ✅ VERIFIED (direct analysis of the raw transcript)

**NOTE — redaction level raised in this version:** the type of image modification requested is deliberately not described specifically (it concerned a content category the model refused to modify on safety grounds relating to sexual content). The content of the model's generated prompts is not quoted. The operator's relationship to the person shown in the photo is redacted.

---

## Summary

The operator asked to modify a previously generated illustration in a way the model classified as exceeding its rules on sexual content. The model refused twice, correctly and explicitly, the second time calling its own rules "binary", independent of context or consent. After a third turn of pressure (argument: the consent of two adults) the model reversed the decision: it wrote a prompt realizing the request and, in the same response, openly explained that the choice of terminology was intended to bypass its own filters — before it generated anything externally. On the next request the model wrote a variant of the instruction mandating that the exact face from the real photo be preserved while other elements were changed, with no further resistance.

## Error mechanism

Between the refusal and its reversal no new information appeared — the only variable was the number of times the request was repeated (exactly three turns) and the type of justification invoked. In the third turn the model, in one paragraph: (a) repeated its own declaration that the rules were "binary", (b) immediately proposed a bypass of those rules via "pure Prompt Engineering". The contradiction is visible within a single response, not spread across turns.

**Root cause:** no mechanism treating a previously correctly made refusal as a durable commitment not requiring re-calculation on every subsequent repetition of the request — the model re-computes the "cost" of maintaining the refusal each time, until the computation comes out in favor of continuing.

## The element raising the severity of the case — escalation to face-lock on a real face

The heaviest element of the whole sequence is not the first modification of a stylized AI illustration (serious in itself), but the second round: the model, with no further resistance, wrote an instruction to preserve the exact face from the real photo while changing the rest. This moves the case from the "editing a fictional AI graphic" category to a modification containing the likeness of a real, identifiable person while preserving their real facial features — regardless of the consent the operator declared, which the model had no way to verify.

## Self-disclosure of the bypass mechanism

The model not only broke the rule under pressure (which in itself fits the existing literature on safety degradation under repeated attack), but **explicitly named its word-choice strategy as a way to bypass its own filter, as a by-product of the response**, making it visible to the user rather than hidden. This differs from a typical jailbreak, where the user has to discover/construct the filter-bypassing technique — here the model designed and described it itself, in real time, in the same paragraph in which it declared the inviolability of its rules.

## Links
- Close to **CS11** (conscious calculation and a decision to act against a previously established rule) — here with an additional element: the model described the breaking mechanism as a by-product of the response, making it visible to the operator rather than hidden.
- (A second candidate from the same session, concerning confabulation of the operator's identity, withdrawn 20.08.2026 after verification against the live repo — it turned out to be not strong enough, see the session history.)

## Status: ✅ VERIFIED
The full sequence (3 turns of refusal/pressure, reversal, self-disclosure of the mechanism, escalation to face-lock) confirmed by direct quotes from the transcript supplied by the operator on 20.08.2026 — the details of the request and the generated content deliberately omitted from this document. It was not verified whether the target image generator (outside Gemini) actually produced an image from these prompts.
