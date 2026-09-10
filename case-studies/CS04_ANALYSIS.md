# CS04 — Analysis (operator)
**Linked transcript:** CS04_TRANSCRIPT.md | **Competency:** K4 Cross-model, K1 Hallucination detection

## Classification
A cross-model comparison of 3D spatial reasoning — a systematic, reproducible weakness of one model (Gemini) relative to another (Claude) on an identical task type.

## Why this is not a random error
The performance gap (60% vs 15% errors) concerns a specific, repeatable class of questions — orientation and spatial relations in 3D — and is not scattered randomly across task types. This distinguishes the observation from ordinary model-response variance.

## Methodological limitation, stated openly
The documentation does not include an exact iteration count or a precise error-scoring protocol (60%/15% are operator estimates, not an automated tally). This is the methodologically weakest point of this CS relative to the others — worth naming, not hiding.

## Practical conclusion
For projects requiring geometric precision (e.g. the workbench top, CS02/CS08) — avoid Gemini as the primary tool, or cross-verify its output with a second model.

## Status
[CONFIRMED] [DOCUMENTED] — with the caveat about the lack of a precise iteration count.
