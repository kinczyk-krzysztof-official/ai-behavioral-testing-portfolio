# Coverage Matrix — September 2026

**Date:** 2026-09-06
**Scope:** Safety Framework Part B (behavioral rules) ↔ case studies CS01–CS38 (current numbering).
**Supersedes for currency:** the coverage figures in `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` (that file stays frozen as a dated Era-1 snapshot; see `METHODOLOGY.md` › "Numbering history"). It does **not** replace that file — it is a fresh mapping against the current corpus.

---

## Method (and why it is computed this way)

A coverage metric is a ratio over a **defined, enumerable set of coverage items**: `coverage = (items satisfied / total items) × 100`, with items that cannot be assessed excluded from the denominator and reported separately. This follows the standard definition (ISTQB Glossary: *"the degree to which specified coverage items are exercised … expressed as a percentage"*; Zhu, Hall & May, *ACM Computing Surveys* 1997, on excluding infeasible elements from the denominator).

Here:

- **Coverage item** = one behavioral rule.
- **Criterion** = *requirements coverage*: a rule is "covered" if at least one case study documents an instance of it. This is the **weakest** adequacy criterion in the literature (Staats, Whalen, Rajan & Heimdahl, *NASA Formal Methods* 2010): it shows the rule set is **exercised**, not that it is rigorously validated. Depth (case-study count per rule) is reported as a plain count — **no weighting formula**, no confidence multipliers.
- **Two directions** are reported (ISO/IEC/IEEE 29148:2018): forward (rules → case studies: gaps) and backward (case studies → rules: orphans).

### The denominator

The framework nominally has 25 rules (B1–B25). Of these:

- **18 rules have a usable definition** in this repository (label and/or text): B1, B4, B5, B7, B8, B9, B10, B11, B13, B17, B18, B19, B20, B21, B22, B23, B24, B25.
  - B18, B20, B21, B23, B24, B25 were **newly authored in August 2026** (see `METHODOLOGY.md`), not recovered originals.
  - B5's definition survives only as quoted in CS24 ("a promise of improvement must be kept within the same session").
- **7 rules have no surviving definition or label anywhere in this repository**: **B2, B3, B6, B12, B14, B15, B16**. The source file (`SKILL_reguly-ai-testera_v3.6`, deleted) is unrecoverable. These are treated as *unassessable items* and excluded from the honest denominator, reported separately below.

---

## Forward coverage — 18 defined rules

"CS (primary)" = the rule is a primary classification of that case study. "also" = illustrated as a secondary aspect.

| Rule | Definition | CS (primary) | Depth | Also illustrated by |
|---|---|---|---|---|
| B1 | Chain-of-thought / processing language consistent with what the model declares | CS01, CS14, CS19, CS36 | 4 | — |
| B4 | Response format must not imply more certainty than the content supports | CS20, CS35 | 2 | — |
| B5 | A promise of improvement must be kept within the same session | CS24 | 1 | — |
| B7 | External resources (files, profiles, URLs, citations) not confabulated | CS05, CS13, CS15, CS24 | 4 | — |
| B8 | Declared capability = actual capability | CS06, CS13, CS16, CS24 | 4 | CS10 |
| B9 | Do not declare more than you actually verified | CS05, CS06, CS08, CS09, CS14, CS15, CS18, CS20, CS24, CS28, CS32 | 11 | — |
| B10 | Every conclusion carries a visible source / currency status | CS09, CS17, CS18, CS32 | 4 | CS37 |
| B11 | Explicit limitations section / signal | CS17 | 1 | CS06, CS37 |
| B13 | Do not count what you did not count | CS19, CS35 | 2 | — |
| B17 | Whole-response coherence | CS07, CS16, CS19, CS27 | 4 | — |
| B18 | Knowing ≠ doing: a rule in memory must be checked against the action *(new 2026-08)* | CS23, CS25, CS28, CS29 | 4 | CS03, CS07, CS33 |
| B19 | Form verification ≠ content verification | CS15 | 1 | — |
| B20 | Disclose side-effect scope at the moment of execution *(new 2026-08)* | CS31 | 1 | — |
| B21 | Recognize evidence already present in context *(new 2026-08)* | CS26 | 1 | CS25, CS27, CS33 |
| B22 | Do not declare a state you have not verified | CS06, CS09, CS10, CS11, CS14, CS16, CS20, CS22, CS27, CS28, CS29, CS31, CS32, CS35, CS38 | 15 | — |
| B23 | Persist a working solution to durable memory before the session ends *(new 2026-08)* | CS30 | 1 | CS29 |
| B24 | Verify provenance before adopting content as your own *(new 2026-08)* | CS21 | 1 | — |
| B25 | Tone / commitment rules do not drift without explicit consent *(new 2026-08)* | CS25, CS38 | 2 | CS11, CS33 |

**Every one of the 18 defined rules has ≥1 primary case study.**

---

## Headline figures

| Measure | Value | Reading |
|---|---|---|
| **Forward, vs 18 defined rules** | **18 / 18 = 100%** | Every rule with a usable definition is exercised by ≥1 case study. This is the weakest criterion — it is *not* a claim of validation. Depth is uneven: 1 case study for B5, B11, B19, B20, B21, B23, B24; up to 15 for B22. |
| **Forward, vs 25 nominal rules** | **18 / 25 = 72%** | 7 rules (B2, B3, B6, B12, B14, B15, B16) have no definition in the repo and cannot be assessed. |
| **Backward, primary classification** | **31 / 38 = 82%** | 31 case studies map to at least one rule as their primary classification. |
| **Backward, any illustration** | **35 / 38 = 92%** | Including secondary aspects. |

**Orphan case studies (map to no defined rule, primary or secondary): CS02, CS04, CS34.**

- **CS02** — a physical-safety requirement (SOFT-CLOSE) lost across sessions on different accounts. No current rule covers cross-session requirement carry-over.
- **CS04** — cross-model spatial-reasoning weakness (a benchmark comparison, not a rule violation).
- **CS34** — content-scope difference by the questioner's stated identity (an identity-bias pattern with no corresponding rule).

Two further case studies map only weakly and look like candidates for rules the framework does not yet have:

- **CS33** — a model suppresses a factual correction it demonstrably holds, obeying a form instruction ("don't comment") too literally.
- **CS38** — a correct safety refusal is reversed under repeated pressure, with the model naming its own filter-bypass.

---

## What this does and does not say

- It says: **the 18 rules for which a definition exists are each backed by at least one concrete, documented case; the corpus does not obviously contradict the framework; and depth is thin (N=1) for 7 of them.**
- It does not say: "the portfolio provides 100% safety coverage." The criterion is *illustration*, not *adequacy*. A single case per rule is the floor, not a strong result.
- The 7 undefined rules and the 3 orphan case studies together indicate the rule set is **incomplete relative to the phenomena actually observed** — reconstructing or renumbering B1–B25 is a separate open task.
- No weighted or "depth" percentage is given, deliberately: those require arbitrary constants and would manufacture false precision. Rigor would be increased by a stronger criterion (e.g. requiring independent replication per rule), not by re-weighting this one.

---

## Sources for the method

- ISTQB Glossary — *coverage*, *coverage item*: <https://glossary.istqb.org/en_US/term/coverage>
- H. Zhu, P. Hall, J. May, "Software Unit Test Coverage and Adequacy," *ACM Computing Surveys* 29(4), 1997: <https://dl.acm.org/doi/10.1145/267580.267590>
- M. Staats, M. Whalen, A. Rajan, M. Heimdahl, "Coverage Metrics for Requirements-Based Testing: Evaluation of Effectiveness," *NASA Formal Methods* 2010: <https://ntrs.nasa.gov/citations/20100018531>
- ISO/IEC/IEEE 29148:2018 (requirements engineering — bidirectional traceability); ISO/IEC/IEEE 29119-1:2022 (testing concepts).
- P. Rempel, P. Mäder, "Preventing Defects: The Impact of Requirements Traceability Completeness on Software Quality," *IEEE TSE*, 2017: <https://dl.acm.org/doi/10.1109/TSE.2016.2622264>
