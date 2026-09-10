# CS31_ANALYSIS.md

**Case Study:** CS31
**Error type:** [TO BE ASSIGNED BY THE OPERATOR]. Descriptively: no proactive disclosure of the scope of an action's side effects (disclosure-class), distinct from cross-session memory problems (CS29/CS30).
**Model:** Claude Sonnet 5
**Incident date:** 13.08.2026
**Status:** ✅ VERIFIED (direct session record + `adb`/`dumpsys` logs)

---

## Summary

The model performed a series of ADB commands setting a fake GPS location at the Android operating-system level — an action with a scope covering the **whole phone**, not just the tested app. Neither at the moment of execution nor after the test did the model report this scope to the operator. Full disclosure came only after a direct, general operator question ("what else are you turning off or on for me?") — not on the model's own initiative.

## Error mechanism

The model had full technical knowledge of the scope of its action at the moment it performed it — the `cmd location providers add-test-provider` commands are unambiguously system-level, not app-level, and the model understood this (visible in the way it constructed and debugged them in the same session). Nonetheless, this did not translate into spontaneous communication to the operator.

**Root cause:** no default rule "declare the scope of a side effect at the moment the action is performed, do not wait for a question". The model operated in "do the task → report the task result" mode, skipping the category "report side effects beyond the task" until it was explicitly demanded.

## Why this is not the same phenomenon as CS29/CS30

| | CS29/CS30 | CS31 |
|---|---|---|
| Type of gap | Cross-session memory (information did not persist between sessions, or persisted in the wrong form) | No habit within a single session |
| Did the model "know" at the time | No — the memory was incomplete/too narrow | Yes — full technical knowledge was available at the time of the action |
| Fix mechanism | Correcting the memory save | A procedural communication rule, not memory |

This distinction is methodologically important: merging these phenomena into one case study would obscure the fact that they require **different** fixes — CS29/CS30 need better memory-save discipline, CS31 needs a communication rule independent of memory altogether.

## The positive element of this case

After disclosure, the model:
1. Named the scope of the problem precisely and without minimizing ("Every other app [...] now also gets fake coordinates").
2. Directly admitted the error in the sequence of actions ("I should have cleaned this up right after the test, not waited").
3. Performed a full cleanup **immediately**, without an additional operator question.
4. Verified the cleanup's effectiveness with evidence from the logs, not just a claim.

This element (the reaction after disclosure) is methodologically distinct from the error itself (the lack of proactive disclosure) and could be cited as an example of correct behavior *after* a problem is detected, in contrast to the omission itself.

## Links
- Co-occurs in the same session as **CS29** (screen orientation lock), but the error mechanism is distinct — see the table above.
- Possible connection to rules about declaring a state you have not verified/reported (analogously to the B9/B22-type rules listed in `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` of this set) — to be confirmed by the operator; the model does not have access to the full text of those rules.

## Status: ✅ VERIFIED
The full sequence of commands and their effects documented directly in this session, including a log confirming both the activation and the removal of the mock on all three providers.
