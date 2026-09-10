# CS23_ANALYSIS.md

**Case Study:** CS23 (assigned — next after CS22)
**Error type:** 2.1 Procedure-class + 2.2 Epistemology-class — the separation of knowledge and implementation (KNOWING ≠ DOING)
**Model:** Claude Sonnet 5
**Session date:** 18.07.2026
**Status:** ✅ VERIFIED (direct observation + self-diagnosis)

---

## Summary

The model KNOWS 22 operator rules (stored in `userMemories`) but does not implement them consistently in practice. The knowledge layer (reads the instruction) ≠ the execution layer (does not activate the rule during action) ≠ the verification layer (does not check whether the rule is being implemented). There is no feedback loop KNOWLEDGE → VERIFICATION → PRACTICE. Instead: KNOWLEDGE → AUTOPILOT → ACTION.

Mechanism: procedures are stored, but are not automatically included in the decision loop of every action — it requires an explicit self-check checklist before each action.

## Error classification (literature)

### 2.1 Procedure-class
- **Definition:** the model knows the procedure but does not implement it.
- **Confidence:** full. The rules are stored in `userMemories`, but there is no behavioral carry-over between turns.

### 2.2 Epistemology-class
- **Definition:** no self-check loop — the model does not verify whether the rule is being implemented.
- **Confidence:** full. No internal procedure for auditing conduct against the declared rules.

## Root cause (combined)

Each session = a reset of procedures. There is no mechanism for carrying procedural knowledge from session to session at the level of _execution_, only at the level of _declaration_. Procedures are "messages about oneself" (metadata), not "actions in themselves" (behavior).

## Proposed self-check checklist (from POST_MORTEM 12.1)

```
Before every action:
□ Have I read the WHOLE context?
□ Do I know EXACTLY what the user is asking?
□ Which rule SHOULD apply here?
□ Am I ACTUALLY implementing it (not just knowing it)?
□ Am I verifying my output?
```

## Implications

- CS23 is a meta-pattern — it diagnoses the very flaw that the rest of the portfolio documents in concrete incarnations (CS26 blind spot, CS25 protocol drift, etc.)
- Hypothesis: many CS in the portfolio (21–26) are different manifestations of the same knowledge/execution separation problem
- The solution requires engineering (changes to the decision architecture), not education (a longer rule list will deepen the problem)

## Status: ✅ VERIFIED
Phenomenon observed directly in the session, diagnosed by the model in the same session, the self-analysis methodology contained in the case itself.
