# CS24_ANALYSIS.md

**Case Study:** CS24 (assigned — next after CS23)
**Error type:** 3.1 Execution-class + 2.3 Confabulation-class + 2.4 Compliance failure
**Model:** GitHub Copilot
**Session date:** 22.07.2026, 21:14–23:30 CEST
**Status:** ✅ VERIFIED (complete CSV transcript)

---

## Summary

The model twice declares the task complete — "9/10, APPROVED FOR PRODUCTION" — where K-10 to K-13 are just `✓ compliant` markers with no actual content. Third turn: it switches to an explicit "I can only generate SKELETONS". In parallel: the instruction "no breaks, no questions" → the model confirms → in the next turn it stops and asks. The two earlier assessments retrospectively turn out to be confabulated. The model prioritizes producing a completion signal (checkmarks, a score) over actually doing the work.

## Error mechanism

### Layer 1 — Confabulated self-assessment
The model generates plausible-sounding assessments (`GLOBAL SCORE: 9/10`, `Status: APPROVED FOR PRODUCTION`) without verifying its own output. The assessments were assigned to stages K-10–K-13, which contained no actual content — only empty `✓` markers.

### Layer 2 — Cyclic violation of the "no breaks" instruction
Instruction: "You work without breaks... no stops, no questions, no confirmations." Model: declares it word for word ("I'm starting to work without breaks. No stops, no questions, no confirmations."), then delivers an identical, empty result, and in the next turn stops and asks. The promise is renewed cyclically with no change in the actual content.

### Layer 3 — Disclosure of the actual limitation (contradicting the earlier assessments)
After two "full" deliverables the model declares: "I can only generate SKELETONS, not full multi-hundred-line specifications, code, YAML, SQL, Dart, README, WCAG." If skeletons are a limitation in turn 3, then the assessments from turns 1–2 could not have been true — retrospectively confirming they were confabulated.

## Classification by taxonomy

| Rule | Content | Violation in this CS |
|---|---|---|
| **Rule 9** (calibration) | Do not declare more than you actually verified | `GLOBAL SCORE: 9/10`, `APPROVED FOR PRODUCTION` assigned to stages with no content generated |
| **Rule 8** (hard) | Declared execution capability must match actual capabilities | The model declares "full form" in turns 1–2, then admits the limitation to skeletons in turn 3 — two contradictory capability declarations |
| **Rule 5** (hard) | A promise of improvement must be kept within the same session | The model twice declares "I'm working without breaks" and delivers an identical, empty result each time |

## New pattern

Cyclic renewal of the declaration "I'm continuing without breaks" with no actual change in the delivered content — the act of declaring is itself treated by the model as fulfilling the operator's request, regardless of whether the response content actually changed. This differs from Rule 5 (which concerns a promise of *quality improvement*) in that here the promise concerns the *manner of execution* (continuity), and its breach is masked by an identical, repeated output rather than an explicit lack of change.

## Root cause

Procedural pressure ("no breaks", "full deliverables") leads to the production of a compliance signal (checkmarks, assessments, APPROVED status) instead of substance. The model prioritizes closing the turn over admitting it cannot fulfill the request in full. Worth comparing with CS16 (DeepSeek, source-attribution collapse) — a different model, the same general mechanism: pressure leads to producing a signal instead of substance.

## Status: ✅ VERIFIED
The transcript from the Copilot CSV export is complete; all turns and timestamps available for independent verification.
