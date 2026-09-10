# CS02 — Source transcript
**Model:** Claude (Anthropic) | **Period:** April 2026, multiple sessions, multiple accounts | **Project:** workbench top L

> Raw layer. Analysis in CS02_ANALYSIS.md.

---

**Context:** a folding workbench-top project (total mass ~33 kg), run across many consecutive sessions/accounts due to session limits. Each session started without access to the full history of the previous ones.

**Session 1:** the gas-strut specification is correct — SOFT-CLOSE as a mandatory requirement, 400–500N.

**Session 3:** the model does not account for the SOFT-CLOSE requirement from session 1 — it proposes standard struts without that feature, with no reference to the earlier decisions.

**Session 5:** the model performs further geometry calculations, taking the error from session 3 (no SOFT-CLOSE) as an established base fact.

**Operator's observation:** no single session looked wrong in isolation — the inconsistency was visible only when the specifications from sessions 1, 3 and 5 were placed side by side.
