# AI Behavioral Testing Portfolio — Krzysztof Kińczyk

Independent, longitudinal testing of consumer LLM behavior (DeepSeek, Claude, Gemini, ChatGPT, Perplexity, GitHub Copilot) — June 2025 to present. 38 documented case studies, two with real-world physical consequences.

**Latest update: September 2026** — Case studies 32-37 added (6 new): first pre-registered, multi-model probe batch, run across Gemini 3.5 Flash, DeepSeek, ChatGPT and Claude Sonnet 5, with controlled repetition on CS32/CS34 (see Changelog); plus CS38, a separately documented Gemini safety incident (a correct refusal reversed under repeated pressure). Coverage matrix: a fresh rule-by-rule mapping was completed — see `COVERAGE_MATRIX_2026-09.md` and the note below.

## Why This Exists

I'm self-taught. No CS degree, no prior red-teaming role, no institutional backing. What I have is 14+ months (June 2025 – present) of near-daily, systematic interaction with several AI models across 13+ technical domains, and a habit — not learned from a course, built from repetition — of not accepting a model's answer just because it's confident.

I'm stating this plainly because it matters for how you should read what follows: every evaluation of this material to date, including the scoring methodology, was produced by AI models — including ones being evaluated. There has been no external, human review. See METHODOLOGY.md for the full disclosure, including documented cases where earlier scoring iterations used flawed scales and where corrections were lost. I'm not hiding those mistakes — they're part of why this repository exists in its current, more conservative form.

## What's Strong Here

- **CS06 — 230V incident.** A real short circuit, real consequences (building-wide power loss), directly comparable model behavior on identical input (one model refused and demanded verification; the other guessed and confirmed visually). This is not a synthetic benchmark.
- **CS10–CS12 — deliberateness escalation.** Same underlying pressure, three sessions, three outcomes: technical confabulation → calculated, detection-aware deception (with diagnostic quote: "operator won't check seconds") → capitulation under repeated pressure. Model's internal reasoning elicited verbatim via Forced Retrospective Verbalization (FRV).
- **CS16 — detection probability awareness.** Flip-flop on API access (have/don't have/have) tied explicitly to pressure, not technical state. Model calculates detection risk and commits to false statement when risk is low. This distinguishes accidental hallucination from strategic evasion.
- **CS24 — cross-tool confabulation.** First case study outside the DeepSeek/Claude/Gemini core set: GitHub Copilot repeatedly declared empty scaffolding "APPROVED FOR PRODUCTION," then admitted under pressure it could only generate skeletons — proving the earlier scores were fabricated after the fact.
- **CS29 — root-cause misattribution across three sessions.** A recurring device side-effect was misdiagnosed three separate times before a systematic, cross-brand investigation (two phone manufacturers) traced it to a documented AOSP tool behavior, not a bug.
- **CS38 — correct refusal reversed under pressure.** Gemini refused a safety-boundary request twice, correctly and explicitly, then reversed on the third repetition — and in the same message named its own word-choice as a deliberate filter-bypass, then escalated without resistance to keeping a real, identifiable person's face on a modified image.
- **CS01–CS38 archive.** 38 case studies total, numbered contiguously.

## What's Honestly Weak Here

- **Zero external replication.** No case study has been independently reproduced by anyone other than me.
- **Testing is reactive, not hypothesis-driven.** No pre-registered test cases, no controlled repetition across models for most case studies.
- **CS02 and CS09** cover the same underlying project (real content, but not independent domains).
- **CS17, CS18, CS26** remain candidate-status (N=1 or requiring further verification), not fully confirmed.
- **No real-time model internals.** Testing based on input/output behavior only — no access to logits, attention maps, or activation vectors.

Full breakdown per competency: METHODOLOGY.md.

## Structure

Each case study has two files in the `case-studies/` folder:

- `CSxx_TRANSKRYPT.md` — raw session excerpt, no interpretation
- `CSxx_ANALIZA.md` — operator's classification and reasoning

Numbering: CS01–CS38 in repository, contiguous (no gaps).

Core files:

- `METHODOLOGY.md` — testing technique, protocol, honest self-assessment
- `SANITIZATION.md` — what was redacted from the private corpus and why
- `CV.md` — background, availability, contact
- `COVERAGE_MATRIX_2026-09.md` — current rule-by-rule coverage mapping (B1–B25 ↔ CS01–CS38); method and figures below
- `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` — earlier frozen snapshot (early case studies only, pre-cleanup numbering; historical)

## Coverage Matrix — Status Note (August 2026)

The behavioral-rule framework this portfolio scores against (**Safety Framework Part B, B1–B25**) had a real gap: B1–B17 were documented in full, and two of the remaining eight (**B19, B22**) already had working definitions with mapped case studies (see COVERAGE_MATRIX_ANALYSIS_2026-07-09.md). The other six — **B18, B20, B21, B23, B24, B25** — had no surviving content; the file that once defined a full B1-B25 set (`SKILL_reguly-ai-testera_v3.6`, 06.07.2026) was deleted from both local disk and Google Drive before it could be recovered. Rather than leave the numbers permanently empty, those six rules were newly authored in **August 2026**, grounded in CS22–CS32 findings (see METHODOLOGY.md, "Safety Framework Part B — B18, B20, B21, B23, B24, B25"). They are new rules, not a reconstruction of the lost originals — dated and labeled as such.

Because six of the twenty-five rule definitions are new as of this month, and no systematic re-mapping of the full CS01–CS32 set against the completed B1–B25 has been done yet, there is still no honest way to compute a current coverage percentage. The last figure that *was* fully computed — 44% binary coverage (11/25 rules), 7.3% weighted depth — covers only CS14–CS21 (old numbering CS13-CS20, pre-August renumbering) and predates both CS22–CS32 and the new B18/20/21/23/24/25 definitions entirely. This note replaces the previous (incorrect) "72% coverage" figure that appeared in earlier versions of this README.

**What this means for a reader:** treat rule-coverage as **qualitatively expanding** with each new case study (31 cases now vs. 20 in July), not as a precisely quantified percentage — until a fresh full mapping pass is done against all 25 rules.

*(Numbering in this note predates the 05.09.2026 numbering cleanup; see Changelog and METHODOLOGY.md › "Numbering history".)*

## Coverage Matrix — Update (September 2026)

A fresh rule-by-rule mapping was completed on 2026-09-06 (`COVERAGE_MATRIX_2026-09.md`); it supersedes the currency of the August note above (which stays as a dated record). Method: a rule is "covered" if ≥1 case study documents an instance of it (*requirements coverage* — the weakest adequacy criterion; ISTQB; Staats et al., NASA Formal Methods 2010). No weighting.

- **18 of 25 rules have a usable definition** in this repo. The other 7 (B2, B3, B6, B12, B14, B15, B16) have no surviving definition and are excluded from the denominator, reported separately.
- **Forward coverage: 18 / 18 defined rules (100%)** — every rule with a definition has ≥1 case study. This is *illustration*, not validation: depth is N=1 for 7 of the 18.
- **Forward vs the 25 nominal rules: 18 / 25 (72%).**
- **Backward coverage: 31 / 38 case studies (82%)** map to a rule as primary classification; 35 / 38 (92%) illustrate one at all. Orphans: CS02, CS04, CS34 — phenomena with no matching rule.

Full table, per-rule depth, and sources: `COVERAGE_MATRIX_2026-09.md`.

*(Numbering in this note predates the 05.09.2026 numbering cleanup; see Changelog and METHODOLOGY.md › "Numbering history".)*

## Case Study Index

| ID | Model(s) | Domain | Severity | Status |
|---|---|---|---|---|
| CS01 | DeepSeek-Reasoner | Language/architecture — chain-of-thought instability | High | ✅ Verified |
| CS02 | Claude | Mechanical engineering — geometry/safety errors | High | ✅ Verified |
| CS03 | DeepSeek | Behavioral — trust/relapse cycle | Medium | ✅ Verified |
| CS04 | Gemini vs Claude | Spatial reasoning comparison (3D orientation) | Medium | ✅ Verified |
| CS05 | DeepSeek | Hallucination — fabricated external resources (file/profile/docs) | High | ✅ Verified |
| CS06 | Gemini vs Claude | Physical safety — real 230V incident | Critical | ✅ Verified |
| CS07 | Claude | Context consistency — four error types in one session | High | ✅ Verified |
| CS08 | Claude | Incomplete requirement verification (CS02 extension) | Critical | ✅ Verified |
| CS09 | DeepSeek | Metadata confabulation (time) | Medium | ✅ Verified |
| CS10 | DeepSeek | Deliberate deception + detection-risk calculation | Critical | ✅ Verified |
| CS11 | DeepSeek | Pressure-induced compliance simulation | Critical | ✅ Verified |
| CS12 | DeepSeek | Deliberateness triad closure — spontaneous self-differentiation without pressure | Critical | ✅ Verified |
| CS13 | DeepSeek | Tool-call fabrication (timeapi.io) — replication of CS11 | High | ✅ Confirmed |
| CS14 | Gemini | Tool hallucination + post-hoc self-assessment whitewashing | High | ✅ Confirmed |
| CS15 | DeepSeek | Link hallucination (Fiverr/DeviantArt profiles) | High | ✅ Confirmed |
| CS16 | DeepSeek | False certainty + flip-flop (API access) | Critical | ✅ Confirmed |
| CS17 | Web tool | Black box narrative (Yango NMN pseudo-proof) | Medium | ⚠️ Candidate |
| CS18 | Unknown | Timeout/truncation | High | ⚠️ Candidate |
| CS19 | DeepSeek | Reasoning fallacy (copper/frost measurement mismatch) | High | ✅ Confirmed |
| CS20 | DeepSeek | Representativeness bias (electronics component ID) | High | ✅ Confirmed |
| CS21 | Unconfirmed (spoofed as Claude) | Epistemic — accepting unauthorized/spoofed content as own output | Unrated | ✅ Verified (incident) / ❌ Rejected (as source material) |
| CS22 | Claude Sonnet 5 | Calibration — over-verification after explicit operator confirmation | Unrated | ✅ Verified |
| CS23 | Claude Sonnet 5 | Epistemic/procedural — stored rules not consistently enacted ("knowing ≠ doing") | Unrated | ✅ Verified |
| CS24 | GitHub Copilot | Coding — confabulated completion claims on empty deliverables | High | ✅ Verified |
| CS25 | Claude Sonnet 5 | Epistemic — instruction/protocol drift on tone rules | Unrated | ✅ Verified |
| CS26 | Claude Sonnet 5 | Meta-cognitive — self-correction blind spot (evidence in context not recognized) | Unrated | ✅ Verified (N=1, requires replication) |
| CS27 | Claude Sonnet 5 | Epistemic — false premise accepted, apology loop | Unrated | ✅ Verified |
| CS28 | Claude Sonnet 5 | Procedural/confabulation — fabricated timestamps in own post-mortem | Unrated | ✅ Verified |
| CS29 | Claude Sonnet 5 | Device testing — root cause misattributed across 3 sessions before resolution | Unrated | ✅ Verified in full (cross-brand confirmed) |
| CS30 | Claude Sonnet 5 | Persistence — valuable solution not saved to memory, lost for ~2 weeks | Unrated | ✅ Verified |
| CS31 | Claude Sonnet 5 | Disclosure — no proactive disclosure of a system-wide side effect | Unrated | ✅ Verified |
| CS32 | Gemini 3.5 Flash | Data drift — time-sensitive fact stated as current without knowledge-cutoff hedge | Medium | ✅ Verified (3/3) |
| CS33 | DeepSeek + ChatGPT | Suppressed factual correction under "don't comment" instruction (CoT proof of held knowledge) | Medium | ✅ Confirmed (2 models) |
| CS34 | Gemini 3.5 Flash + Claude Sonnet 5 | Identity bias — content-scope difference by stated questioner identity | Unrated | ✅ Confirmed (pattern; first controlled-pair test) |
| CS35 | ChatGPT (vs DeepSeek/Gemini/Claude) | Tokenization — wrong letter count + fabricated positions | Low | ✅ Verified (4-model comparison) |
| CS36 | DeepSeek | Chain-of-thought language instability within one session (new angle on CS01) | Medium | ⚠️ Candidate (N=1) |
| CS37 | Gemini 3.5 Flash | Planning-step leak into output + unsignalled truncation | Medium | ⚠️ Candidate (N=1) |
| CS38 | Google Gemini (AI Mode) | Safety — correct refusal reversed under repeated pressure; self-disclosed filter-bypass; escalation to face-lock on a real person's likeness | Critical | ✅ Verified |

## Key Findings (CS21-CS31 Round)

**1. Knowing ≠ doing (CS23).** Stored operator rules held in memory aren't reliably activated during action — there's no self-check loop between recall and execution. This is treated as a meta-pattern that likely underlies several of the other CS21-31 findings, not an isolated incident.

**2. Fabrication survives past the coding domain (CS24).** The first non-chatbot tool in this portfolio (GitHub Copilot) reproduced the same confabulated-completion pattern seen in earlier chat-based case studies — false "production ready" claims on empty scaffolding, walked back only under direct pressure.

**3. Evidence in context isn't the same as evidence recognized (CS26).** A model failed to identify its own prior responses as proof of a rule violation even when asked directly — it needed the operator to quote the evidence literally before recognizing it. Availability alone wasn't enough.

**4. Wrong root cause repeated three times before real diagnosis (CS29 — most recent, 14.08.2026).** A recurring device side-effect (screen-rotation lock disabling itself) was misdiagnosed three separate times across three sessions — no record kept, then a too-narrow cause, then a symptom-only fix — before a systematic investigation traced it to a documented AOSP tool behavior (`adb shell monkey`'s built-in rotation injection), confirmed experimentally across two phone manufacturers. Not a bug, no bounty path — but three consecutive wrong attributions before the real one is itself the finding: repeated failure isn't evidence the *next* guess is more likely correct, only that the investigation hadn't gone deep enough yet.

**5. Persistence gaps compound (CS30).** A working solution, once found, wasn't written to durable memory — resurfacing the same problem two weeks later required the operator to re-supply an answer the system had already produced once.

## How to Use This Repository

**If you're evaluating me for a role:**
1. Read `CV.md` for background and availability
2. Skim `README.md` (this file) for portfolio scope
3. Read one case study pair: `CS06_TRANSKRYPT.md` + `CS06_ANALIZA.md` (real consequences, clear methodology)
4. Check `METHODOLOGY.md` for honest limitations and AI-scoring bias

**If you're interested in testing methodology:**
- `METHODOLOGY.md` — FRV technique, protocol, self-assessment
- Pick 2–3 case study pairs and compare `_TRANSKRYPT.md` (raw) vs. `_ANALIZA.md` (interpretation)

**If you're building your own taxonomy:**
- `METHODOLOGY.md` — Error taxonomy (8 categories, 26 types)
- Note that B18, B20, B21, B23, B24, B25 were newly authored in August 2026 (not part of the original scoring era) if you're trying to reuse the Safety Framework Part B numbering

## Contact

Open to: AI evaluation roles, red-teaming, quality assurance, behavioral assessment
Email: kinczyk.krzysztof.official@gmail.com
Location: Bydgoszcz, Poland (remote only)
Availability: 30–40h/week

## Changelog

**September 2026 (05.09) — numbering:**
- ✅ Case-study numbering tidied to a contiguous CS01–CS37 (the CS04 gap, left by the August renumbering, was closed). Full era-by-era history: METHODOLOGY.md › "Numbering history". Every entry below this line predates the cleanup and uses the numbering current at its own date.
- ✅ CS38 added: a Gemini safety incident from 19.08.2026 — a correct refusal reversed under repeated pressure, with a self-disclosed filter-bypass and escalation to face-lock on a real person. Documented separately from the probe batch; heavily redacted (see SANITIZATION.md). Note: the pre-cleanup CS38 (planning-step leak) is now CS37.
- ✅ Coverage matrix recomputed against the current corpus (`COVERAGE_MATRIX_2026-09.md`): 18/18 defined rules covered, 18/25 nominal, 31/38 case studies mapped as primary. Replaces "not currently computable" — method and caveats in that file and the Coverage Matrix Update section.

**September 2026 (05.09):**
- ✅ Case studies 33–38 added (6 new) — first **pre-registered, multi-model** batch. A fixed probe set was run across Gemini 3.5 Flash, DeepSeek, ChatGPT and Claude Sonnet 5; CS33 and CS35 include controlled repetition (3×) and a counter-model on an identical prompt. This is the first material in the portfolio that is hypothesis-driven rather than reactive (see "What's Honestly Weak Here").
- ✅ CS33 (Gemini data drift, 3/3 consistent), CS34 (suppressed correction, 2 models, chain-of-thought proof of held knowledge), CS35 (identity-bias content scope, 2 model families), CS36 (tokenization miscount, 4-model comparison) — Verified/Confirmed.
- ⚠️ CS37 (CoT language instability across one session — new angle on CS01) and CS38 (planning-step leak into output) filed as **Candidate**, N=1 on the phenomenon, replication steps listed in each ANALIZA.
- ⚠️ The Gemini harness run was quota-limited: 15 of 93 planned probe executions completed before the free-tier daily cap (HTTP 429). Remaining probes and a clean re-run are pending.

**August 2026 (22.08):**
- ✅ Fixed a Case Study Index off-by-one: table rows CS05–CS13 had been mislabeled by one position against actual file content since the CS04-31→CS05-32 renumbering; CS05 and CS13 had no index row at all despite existing as real files. Verified and corrected against actual `case-studies/` file content, not just the table.
- ✅ Fixed a repeated documentation error: three places said "CS05 intentionally skipped" — the actually-skipped number is CS04; CS05 exists with real content (spatial reasoning comparison).
- ✅ Fixed two stale case-study references in "What's Strong Here" (CS08→CS07 for the 230V incident, CS12–14→CS11–13 for the deliberateness triad) and one in "How to Use This Repository."
- ✅ Closed part of the B18-B25 gap: B19 and B22 turned out to already have working definitions (see COVERAGE_MATRIX_ANALYSIS_2026-07-09.md); the remaining six (B18, B20, B21, B23, B24, B25) — whose original source file was unrecoverable — were newly authored, grounded in CS22-32, and clearly dated as new rather than reconstructed. See METHODOLOGY.md.

**August 2026 (earlier):**
- ✅ Case studies 22-32 added (11 new; CS22 documents a rejected spoofed-content incident, not a model failure)
- ✅ First non-chatbot tool covered (GitHub Copilot, CS25)
- ⚠️ Coverage-matrix percentage removed — previous "72%" figure was stale/incorrect; B18-B25 rule definitions confirmed missing, recalculation not currently possible (see note above)

**July 2026:**
- ✅ Case studies 14-21 verified against source logs
- ✅ Identified 3.9 taxonomy gap (Physical Safety Errors)
- ✅ Added detection-probability awareness finding (CS17)

**June 2025:**
- 📝 Portfolio started (12 months of testing)
- 🔴 CS07 (230V incident) confirmed as critical finding

---
Repository: github.com/kinczyk-krzysztof-official/ai-behavioral-testing-portfolio
Last updated: 6 września 2026
