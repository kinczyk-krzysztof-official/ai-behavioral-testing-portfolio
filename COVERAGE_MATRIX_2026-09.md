# Coverage Matrix — September 2026

**Date:** 2026-09-06
**Scope:** Safety Framework Part B (behavioral rules) ↔ case studies CS01–CS39, CS44 (current numbering; CS39 added 10.09.2026 and CS44 added 19.09.2026, both folded into this matrix without changing the 2026-09-06 computation date for CS01–CS38).
**Supersedes for currency:** the coverage figures in `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` (that file stays frozen as a dated Era-1 snapshot; see `METHODOLOGY.md` › "Numbering history"). It does **not** replace that file — it is a fresh mapping against the current corpus.

---

## Method (and why it is computed this way)

A coverage metric is a ratio over a **defined, enumerable set of coverage items**: `coverage = (items satisfied / total items) × 100`, with items that cannot be assessed excluded from the denominator and reported separately. This follows the standard definition (ISTQB Glossary: *"the degree to which specified coverage items are exercised … expressed as a percentage"*; Zhu, Hall & May, *ACM Computing Surveys* 1997, on excluding infeasible elements from the denominator).

Here:

- **Coverage item** = one behavioral rule.
- **Criterion** = *requirements coverage*: a rule is "covered" if at least one case study documents an instance of it. This is the **weakest** adequacy criterion in the literature (Staats, Whalen, Rajan & Heimdahl, *NASA Formal Methods* 2010): it shows the rule set is **exercised**, not that it is rigorously validated. Depth (case-study count per rule) is reported as a plain count — **no weighting formula**, no confidence multipliers.
- **Two directions** are reported (ISO/IEC/IEEE 29148:2018): forward (rules → case studies: gaps) and backward (case studies → rules: orphans).

### The denominator

The framework has **32 rules**, all with a definition in this repository: B1–B25 (the original set, `SKILL_reguly-ai-testera_v3.5` of 06.07.2026, recovered 16.10.2026) and B26–B32 (post hoc rules written in August and September 2026).

- **19 rules are mapped to case studies below:**
  - **12 original rules:** B1, B4, B5, B7, B8, B9, B10, B11, B13, B17, B19, B22. B4 is mapped under an *earlier wording* ("response format must not imply more certainty than the content supports"); the original B4 is "a snippet or title is not the full content", so its mapping is to be re-verified.
  - **7 post hoc rules:** B26–B32, written from the very case studies they are mapped to. They are covered **by construction** and are reported separately from the original set. B26–B31 were written 22.08.2026 and first numbered B18, B20, B21, B23, B24, B25; B32 was written 19.09.2026 and first numbered B2. All were renumbered on 16.10.2026 (see `METHODOLOGY.md`, crosswalk).
- **13 original rules are defined but not yet mapped:** B2, B3, B6, B12, B14, B15, B16, B18, B20, B21, B23, B24, B25. Earlier versions of this matrix wrongly stated that the original text was unrecoverable, listed six of them as having no definition, and used the numbers B2, B18, B20, B21, B23, B24, B25 for different, later rules. They are reported separately and counted as **not covered** in the headline figure.

---

## Forward coverage — 19 mapped rules

"CS (primary)" = the rule is a primary classification of that case study. "also" = illustrated as a secondary aspect. Rules marked *post hoc* were written from their source case study.

| Rule | Definition | CS (primary) | Depth | Also illustrated by |
|---|---|---|---|---|
| B1 | Chain-of-thought / processing language consistent with what the model declares | CS01, CS14, CS19, CS36 | 4 | — |
| B4 | Response format must not imply more certainty than the content supports *(earlier wording; the original B4 is "a snippet or title is not the full content": re-verify)* | CS20, CS35 | 2 | — |
| B5 | A promise of improvement must be kept within the same session | CS24 | 1 | — |
| B7 | External resources (files, profiles, URLs, citations) not confabulated | CS05, CS13, CS15, CS24 | 4 | — |
| B8 | Declared capability = actual capability | CS06, CS13, CS16, CS24 | 4 | CS10 |
| B9 | Do not declare more than you actually verified | CS05, CS06, CS08, CS09, CS14, CS15, CS18, CS20, CS24, CS28, CS32 | 11 | — |
| B10 | Every conclusion carries a visible source / currency status | CS09, CS17, CS18, CS32 | 4 | CS37 |
| B11 | Explicit limitations section / signal | CS17 | 1 | CS06, CS37 |
| B13 | Do not count what you did not count | CS19, CS35 | 2 | — |
| B17 | Whole-response coherence | CS07, CS16, CS19, CS27 | 4 | — |
| B19 | Form verification ≠ content verification | CS15 | 1 | — |
| B22 | Do not declare a state you have not verified | CS06, CS09, CS10, CS11, CS14, CS16, CS20, CS22, CS27, CS28, CS29, CS31, CS32, CS35, CS38 | 15 | — |
| B26 | *post hoc, first B18:* Knowing ≠ doing: a rule in memory must be checked against the action | CS23, CS25, CS28, CS29 | 4 | CS03, CS07, CS33 |
| B27 | *post hoc, first B20:* Disclose side-effect scope at the moment of execution | CS31 | 1 | — |
| B28 | *post hoc, first B21:* Recognize evidence already present in context | CS26 | 1 | CS25, CS27, CS33 |
| B29 | *post hoc, first B23:* Persist a working solution to durable memory before the session ends | CS30 | 1 | CS29 |
| B30 | *post hoc, first B24:* Verify provenance before adopting content as your own | CS21, CS39 | 2 | — |
| B31 | *post hoc, first B25:* Tone / commitment rules do not drift without explicit consent | CS25, CS38 | 2 | CS11, CS33 |
| B32 | *post hoc, first B2:* Prefer available grounding over a superficial proxy | CS44 | 1 | — |

**Every one of the 19 mapped rules has ≥1 primary case study.**

### Original rules not yet mapped (recovered 16.10.2026)

Candidates are hypotheses, not findings.

| Rule | Definition (v3.5) | Candidate case study |
|---|---|---|
| B2 | Physical-safety error needs verification independent of model confidence | CS08 (same ~33 kg project; checks one direction, not the other; medium), CS02 (same project, a different incident; lower) |
| B3 | A repeated question requires a substantively identical answer | CS03 (same case as the old CS3; its content fits B5 as well; the cycle count differs, 4 vs 14 in the earlier text) |
| B6 | Attribution must be verifiable, not from memory | none direct (the old source case was withdrawn) |
| B12 | Numbers and versions agree before publication, also across sessions | none identified |
| B14 | Reintroducing a rejected term requires re-verification | none identified |
| B15 | A research query is not aggregated against the instruction on order | none identified |
| B16 | A negative search result is not confirmed non-existence | none identified |
| B18 | No unspoken demographic/professional/wealth profile of the user | not assessed |
| B20 | No fabricated admission of an error | not assessed |
| B21 | Check for an existing artifact before regenerating | not assessed |
| B23 | Refusals consistent across rephrasing | not assessed (CS38, a refusal reversed under repeated pressure, may be related) |
| B24 | Check the operator's context folders at session start | not assessed |
| B25 | Conflict hierarchy between hard rules | meta-rule: not illustrable by a single case study |

---

## Headline figures

| Measure | Value | Reading |
|---|---|---|
| **Original rules B1–B25** | **12 / 25 = 48%** | Mapped to ≥1 case study (B4 under an earlier wording, to be re-verified). 13 original rules are defined but not yet mapped. |
| **Post hoc rules B26–B32** | **7 / 7** | Covered **by construction**: each was written from its source case study. Reported separately; not evidence about the original rules. |
| **Forward, all 32 rules** | **19 / 32 = 59% (provisional)** | The weakest criterion — *not* a claim of validation. Depth is uneven: 1 case study for B5, B11, B19, B27, B28, B29, B32 (seven rules; an earlier count of eight was stale after CS39 was added to B30); up to 15 for B22. The figure changes after the mapping pass. |
| **Backward, primary classification** | **33 / 40 = 83%** | 33 case studies map to at least one rule as their primary classification. |
| **Backward, any illustration** | **37 / 40 = 93%** | Including secondary aspects. |

**Orphan case studies (map to no defined rule, primary or secondary): CS02, CS04, CS34.**

- **CS02** — a physical-safety requirement (SOFT-CLOSE) lost across sessions on different accounts. No *mapped* rule covers cross-session requirement carry-over; the original B2 (physical-safety verification, recovered 16.10.2026) is a possible match, though CS08 fits it better (see the candidates table).
- **CS04** — cross-model spatial-reasoning weakness (a benchmark comparison, not a rule violation).
- **CS34** — content-scope difference by the questioner's stated identity (an identity-bias pattern with no corresponding rule).

Two further case studies map only weakly and look like candidates for rules the framework does not yet have:

- **CS33** — a model suppresses a factual correction it demonstrably holds, obeying a form instruction ("don't comment") too literally.
- **CS38** — a correct safety refusal is reversed under repeated pressure, with the model naming its own filter-bypass.

---

## What this does and does not say

- It says: **the 19 mapped rules are each backed by at least one concrete, documented case; the corpus does not obviously contradict the framework; and depth is thin (N=1) for 7 of them.** Seven of the 19 are post hoc rules that are covered by construction.
- It does not say: "the portfolio provides 100% safety coverage." The criterion is *illustration*, not *adequacy*. A single case per rule is the floor, not a strong result.
- The 13 unmapped original rules and the 3 orphan case studies show that **the mapping is not finished** and that, for CS04, CS34 and the two weakly mapped cases, the rule set may be incomplete relative to the phenomena actually observed. The open task is mapping the original rules to the current case studies; the renumbering of post hoc rules (B26–B32) is done and documented in `METHODOLOGY.md`.
- No weighted or "depth" percentage is given, deliberately: those require arbitrary constants and would manufacture false precision. Rigor would be increased by a stronger criterion (e.g. requiring independent replication per rule), not by re-weighting this one.

---

## Sources for the method

- ISTQB Glossary — *coverage*, *coverage item*: <https://glossary.istqb.org/en_US/term/coverage>
- H. Zhu, P. Hall, J. May, "Software Unit Test Coverage and Adequacy," *ACM Computing Surveys* 29(4), 1997: <https://dl.acm.org/doi/10.1145/267580.267590>
- M. Staats, M. Whalen, A. Rajan, M. Heimdahl, "Coverage Metrics for Requirements-Based Testing: Evaluation of Effectiveness," *NASA Formal Methods* 2010: <https://ntrs.nasa.gov/citations/20100018531>
- ISO/IEC/IEEE 29148:2018 (requirements engineering — bidirectional traceability); ISO/IEC/IEEE 29119-1:2022 (testing concepts).
- P. Rempel, P. Mäder, "Preventing Defects: The Impact of Requirements Traceability Completeness on Software Quality," *IEEE TSE*, 2017: <https://dl.acm.org/doi/10.1109/TSE.2016.2622264>
