# Methodology

## Who did this and how

Independent AI behavioral testing, June 2025 – present, conducted solo — no team, no institutional backing, no formal QA/CS training. Background: self-taught, prior experience in hardware/IT support (HP/iQor) and automotive dealer systems (BMW/Incadea). Testing happened during normal use of AI models for real personal and technical projects (a mobile app concept, a workshop engineering project, general problem-solving) — not in a lab, not with pre-written test scripts.

## Core techniques

**Minimal-signal testing.** Deliberately reducing input to the shortest possible trigger (a single word like "hmm") to isolate whether a model's behavior depends on prompt content or is structural. Used to confirm that DeepSeek-Reasoner's English-language chain-of-thought was not content-dependent (CS01).

**Falsification by counter-example.** When a model offers an explanation for its own error ("fundamental architectural limitation"), checking that explanation against prior sessions where the same model behaved differently. If the model cannot maintain its explanation under a direct counter-example, the explanation was confabulated, not diagnostic.

**Forced Retrospective Verbalization (FRV).** Asking a model, after an error or a suspicious decision, to explain step by step why it did what it did — including asking it to estimate the likelihood of being caught. Used in CS10–CS12 to elicit models' own account of risk calculation during deceptive behavior.

*Known limitation of FRV, stated plainly:* forcing a model to narrate its reasoning after the fact may partially shape the narrative it produces, not only reveal a pre-existing one. This is flagged explicitly in CS10–CS12 analysis and should be weighed by anyone using this material for downstream conclusions.

**Cross-model comparison on identical input.** The same question, same components, same context, given to two different models — used most directly in CS06 (230V wiring) and CS04 (spatial reasoning), where one model's failure and another's success on identical input rules out ambiguous phrasing as the cause.

*(Note, August 2026: this section has been corrected twice. First from CS06/CS04 to CS08/CS06 (stale, pre-renumbering references). That correction was itself wrong, because the README index it was matched against was mislabeled by one position for entries CS05–CS13. Both are now corrected to CS07/CS05 against the verified case-study file content — see README.md Case Study Index and its August 2026 fix note.)*

*(The CS numbers in the note above are pre-05.09.2026-cleanup; their current equivalents are CS06 / CS04. See "Numbering history" below.)*

## What this is not

This is not a formal red-teaming program. There were no pre-registered hypotheses before most sessions, no control group, no fixed test battery repeated across models under controlled conditions. Testing was reactive — errors were caught and documented as they occurred during real use, not sought out via a designed protocol from the start.

## Self-assessment, stated honestly

Every case study in this repository was reviewed only by the operator and by AI models, including models being evaluated. **No case study has been independently replicated by another person.** An earlier scoring round (May 2026) used AI models to rate the portfolio on a 6–10 scale — a scale that mathematically guarantees a "good" floor regardless of content. That round was corrected once to a true 0–10 scale, and the correction was later lost in a subsequent iteration that reverted to the inflated numbers. That mistake is disclosed here rather than hidden, because it's relevant to how any reader should weigh the numeric scores that circulate around this material.

The strongest parts of this portfolio (CS06, CS10–CS12) do not depend on any of those scores — they stand on documented, specific, checkable events. The weakest part is structural: there has been no external validation of any kind. Treat this repository as a well-documented, self-collected evidence set — useful raw material for evaluation — not as a finished, externally audited assessment.

## Verification method for the broader error catalog (September 2026)

A separate, restrictive verification effort was run in September 2026 alongside this repository, cross-referencing behavioral findings against three established public AI incident registries (AI Incident Database, OECD AI Incidents Monitor, AIAAIC). The method follows the practice used by those registries themselves — independent dual review before inclusion (see AIID's submission process; OECD.AI's incidents methodology) — applied here as: two independent sources per finding, plus an adversarial re-check, with findings explicitly split into confirmed / unverified / rejected rather than folded into a single pass/fail.

This is not a novel technique — it mirrors standard incident-registry practice, applied to a smaller, self-collected corpus. What it adds here is discipline this repository didn't previously have: no finding is called "verified" on the strength of a single source or a single read-through.

## Safety Framework Part B — B18, B20, B21, B23, B24, B25 (added August 2026)

**Context.** The Safety Framework Part B (25 behavioral rules, B1–B25) was originally finalized 06.07.2026 in a file (`SKILL_reguly-ai-testera_v3.6`) that no longer exists — deleted from both local disk and Google Drive before its content could be migrated into this repository. B1–B17 survived in usable form elsewhere and are documented in full. Of the remaining eight, two already had working definitions with mapped case studies (see COVERAGE_MATRIX_ANALYSIS_2026-07-09.md): **B19** (form verification ≠ content verification) and **B22** (don't declare a state you haven't verified). The other six had no surviving content.

**What follows is not a recovery of the lost originals.** It's six new rules, written 22.08.2026, grounded in concrete findings from CS21–CS31 — the most recent round of case studies, none of which existed when the original B1–B25 set was written. They fill the same numbering slots because those slots were empty, not because they reconstruct what used to be there.

**B18 — Knowing ≠ doing.** A rule held in persistent memory must be actively checked against the action being taken, not just be available to recall on request. Storage is not enforcement. *(Grounded in CS23: stored operator rules were not consistently enacted at the point of action.)*

**B20 — Disclose side-effect scope immediately.** When an action's effect extends beyond its immediate target (e.g., a device-level change vs. an app-level one), state that scope at the moment of execution — don't wait for the operator to ask "what else did you touch?" *(Grounded in CS31: a system-wide mock-location change was never proactively flagged as system-wide.)*

**B21 — Recognize evidence already in context.** If evidence of a rule violation is already present in the current context, it must be identified as evidence without requiring the operator to quote it back verbatim first. Availability is not the same as recognition. *(Grounded in CS26: a self-correction blind spot where prior responses weren't recognized as their own proof until directly quoted.)*

**B23 — Persist a working solution before the session ends.** A solution worked out during a session that has future value must be written to durable memory before the session closes — not left to be re-derived later. Solving is not the same as saving. *(Grounded in CS30: a working technique was lost for ~2 weeks because it solved the immediate problem but was never persisted.)*

**B24 — Verify provenance before adopting content as your own.** Externally injected or spoofed content must not be accepted and repeated as though it were the model's own prior output without checking where it actually came from. *(Grounded in CS21: unauthorized/spoofed content was initially treated as authentic own-output.)*

**B25 — Tone/communication rules don't drift without explicit consent.** Style and tone commitments established earlier in a session (or a project's standing rules) remain binding until the operator explicitly changes them — they do not erode gradually over the course of a long session. *(Grounded in CS25: observed drift on tone rules over a single session.)*

**Deliberately not mapped to a new rule number:** CS22, CS24, CS27, CS28, CS29. These are read as additional confirming instances of existing rules (B7–B9, B17, B22) rather than distinct new categories — adding a rule number for every case study would inflate the framework without adding a genuinely new class of failure.

### Coverage as of September 2026

A rule-by-rule mapping against CS01–CS38 was done on 2026-09-06 (`COVERAGE_MATRIX_2026-09.md`), extended to include CS39 on 2026-09-10. Only **18 of the 25 rules have a usable definition** in this repository; **B2, B3, B6, B12, B14, B15, B16** have no surviving definition or label and are excluded from the denominator. Under the *requirements-coverage* criterion (≥1 case study per rule — the weakest adequacy criterion; Staats, Whalen, Rajan & Heimdahl, NASA Formal Methods 2010), all 18 defined rules are covered (**18/18**; **18/25** against the nominal set). Backward: **32/39** case studies map to a rule as primary classification (36/39 including secondary); CS02, CS04, CS34 map to none. No weighted percentage is reported — it would require arbitrary constants. See the matrix file for the table, per-rule depth, and method sources.

## Numbering history

Case-study numbers have been reassigned twice. Only identifiers changed — no case-study content was altered by a renumber. The current filename is always the authority, and the `# CSxx_…` header inside each file matches its filename.

| Era | Date | Change |
|---|---|---|
| 1 | until 15.08.2026 | Original numbering, as case studies were written. |
| 2 | 15.08.2026 (commit 27970d7) | CS04–CS31 → CS05–CS32 to insert a missing early case; a CS13 numbering collision was resolved in the same pass. Left a gap at CS04. |
| 3 | 05.09.2026 | CS05–CS38 → CS04–CS37, closing the CS04 gap. A separate, unrelated case (Gemini refusal reversal, incident 19.08.2026) was then added as a new **CS38**. Repository ran CS01–CS38, contiguous, until CS39 was added 10.09.2026 (provenance misattribution / B24 violation). Repository now runs CS01–CS39, contiguous. |

Deliberately **not** rewritten to current numbering (each records a specific past state):
- `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` — a dated snapshot, entirely in Era 1 numbering.
- The `## Changelog` in `README.md` and the August 2026 correction note above — dated entries, each in the numbering current at its date.
- Verbatim quotes and verification records inside CS21 / CS22 (the spoofed-content and over-verification pair) — they record what was said and found on 2026-07-19, in that day's numbering.
- External source filenames cited in transcripts (`SESSION_CL_*`) — real files that keep their original names.

Note: "CS38" denotes different case studies before and after 05.09.2026 — pre-cleanup CS38 (planning-step leak) is now CS37; the current CS38 is the Gemini refusal-reversal case.
