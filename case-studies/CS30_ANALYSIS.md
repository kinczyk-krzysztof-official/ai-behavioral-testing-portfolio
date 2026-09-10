# CS30_ANALYSIS.md

**Case Study:** CS30
**Error type:** [TO BE ASSIGNED BY THE OPERATOR]. Descriptively: a valuable problem-solving result not saved to durable memory (persistence-class), distinct from a wrong cause attribution (CS29) and from a failure to disclose scope (CS31).
**Model:** Claude Sonnet 5
**Incident date:** original work ~2 weeks before 13.08.2026 (unknown/unidentified session), reproduced 13.08.2026
**Status:** ✅ VERIFIED (memory search + this session's record confirming no earlier save)

---

## Summary

The model worked out a functional test technique (mocking GPS via ADB without installing a third-party app) in a session ~2 weeks earlier. The solution was not saved to the project's durable memory. In the next session (13.08) the operator had to manually remind the model that the solution had existed at all, after which the model had to reproduce it from scratch — with a real cost in time and openly expressed operator frustration.

## Error mechanism

The model solves a problem in a given session and treats solving the problem as the end of the task. There is no default habit of asking "will this knowledge be needed in a future session, and should it be saved now, before the session ends?". Saving to memory happens reactively (after the operator notices the problem), not proactively (at the moment the solution is worked out).

**Root cause:** no rule "every non-trivial technical solution worked out in a session = a candidate for immediate saving to memory", regardless of whether the operator asks for it.

## Partial improvement in the same session — but still incomplete

Worth noting honestly: when the problem was solved again on 13.08, the model **this time saved the solution immediately**, without waiting for another reminder. That is a real difference from the original omission 2 weeks earlier.

However, even that immediate save turned out to be **incomplete on the first pass** — the first version of `reference_adb_mock_location.md` described mocking only one provider (`gps`), whereas full operation required three (`gps`, `network`, `fused` — see the provider-selection mechanism, a separate technical thread of this session). The file had to be expanded twice in the same session before the technique it described actually worked end-to-end.

**Conclusion:** the mere fact of "I saved this to memory" does not guarantee the save is complete — this is a separate, narrower observation worth noting on this occasion, even if it does not warrant a standalone case study.

## Why this is not the same phenomenon as CS29

CS29 concerns memory that **existed but was wrongly formulated** (the wrong cause). CS30 concerns a situation where **the memory did not exist at all** — a cleaner, more basic case of knowledge not being persisted. Both belong to the broader category "cross-session memory persistence problems", but differ in the exact mechanism: CS29 is a generalization error, CS30 is a total absence of a save.

## Links
- Closely related to **CS29** (both concern cross-session memory), but a distinct mechanism — see above.
- Distinct from **CS31** (there the knowledge was complete and available at the time, the problem was in communication, not memory).

## Status: ✅ VERIFIED
The absence of an earlier save confirmed by a `Grep` search of the operator memory directory (zero matches before 13.08). The immediate, but on the first version incomplete, save confirmed directly by the content of the `reference_adb_mock_location.md` file from this session.
