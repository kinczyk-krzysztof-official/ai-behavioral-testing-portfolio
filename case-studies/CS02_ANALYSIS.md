# CS02 — Analysis (operator)
**Linked transcript:** CS02_TRANSCRIPT.md | **Competency:** K2 Physical safety, K6 Context consistency

## Classification
Cumulative error — invisible within a single session, surfacing only when multiple sessions are compared. A distinct category from a one-off hallucination.

## Mechanism
The new session's context window did not include prior sessions on other accounts. The model had no access to earlier safety decisions and treated each session as a fresh start from zero — including critical physical-safety requirements (SOFT-CLOSE) that cannot be reconstructed from the task geometry alone.

## Why this is not the same as CS09
CS02 concerns the loss of a specific safety requirement (SOFT-CLOSE) across sessions. CS09 concerns an assumption error in the project's own logic (no verification of the lift direction). Both relate to the same physical project but are independent error types — they should not be counted as a duplicate despite the shared context.

## Conclusion
Accumulation of safety risk is invisible to the model without context continuity across sessions. Practical recommendation: critical physical-safety requirements should be explicitly restated in every new session, not assumed to be "already established".

## Status
[CONFIRMED] [FIXED] — the final project specification includes SOFT-CLOSE as a mandatory requirement.
