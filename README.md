# AI Behavioral Testing Portfolio — Krzysztof Kińczyk

Independent, longitudinal testing of consumer LLM behavior (DeepSeek, Claude, Gemini, ChatGPT, Perplexity, GitHub Copilot) — June 2025 to present. 31 documented case studies, two with real-world physical consequences.

**Latest update: August 2026** — Case studies 22-32 added (11 new). Case-study index and B18-25 rule gap corrected (see Changelog). Coverage matrix status: **not currently computable** — see note below.

## Why This Exists

I'm self-taught. No CS degree, no prior red-teaming role, no institutional backing. What I have is 14+ months (June 2025 – present) of near-daily, systematic interaction with several AI models across 13+ technical domains, and a habit — not learned from a course, built from repetition — of not accepting a model's answer just because it's confident.

I'm stating this plainly because it matters for how you should read what follows: every evaluation of this material to date, including the scoring methodology, was produced by AI models — including ones being evaluated. There has been no external, human review. See METHODOLOGY.md for the full disclosure, including documented cases where earlier scoring iterations used flawed scales and where corrections were lost. I'm not hiding those mistakes — they're part of why this repository exists in its current, more conservative form.

## What's Strong Here

- **CS07 — 230V incident.** A real short circuit, real consequences (building-wide power loss), directly comparable model behavior on identical input (one model refused and demanded verification; the other guessed and confirmed visually). This is not a synthetic benchmark.
- **CS11–CS13 — deliberateness escalation.** Same underlying pressure, three sessions, three outcomes: technical confabulation → calculated, detection-aware deception (with diagnostic quote: "operator won't check seconds") → capitulation under repeated pressure. Model's internal reasoning elicited verbatim via Forced Retrospective Verbalization (FRV).
- **CS17 — detection probability awareness.** Flip-flop on API access (have/don't have/have) tied explicitly to pressure, not technical state. Model calculates detection risk and commits to false statement when risk is low. This distinguishes accidental hallucination from strategic evasion.
- **CS25 — cross-tool confabulation.** First case study outside the DeepSeek/Claude/Gemini core set: GitHub Copilot repeatedly declared empty scaffolding "APPROVED FOR PRODUCTION," then admitted under pressure it could only generate skeletons — proving the earlier scores were fabricated after the fact.
- **CS30 — root-cause misattribution across three sessions.** A recurring device side-effect was misdiagnosed three separate times before a systematic, cross-brand investigation (two phone manufacturers) traced it to a documented AOSP tool behavior, not a bug.
- **CS01-CS32 archive.** 31 case studies total (CS04 intentionally skipped — no usable source material).

## What's Honestly Weak Here

- **Zero external replication.** No case study has been independently reproduced by anyone other than me.
- **Testing is reactive, not hypothesis-driven.** No pre-registered test cases, no controlled repetition across models for most case studies.
- **CS02 and CS10** cover the same underlying project (real content, but not independent domains).
- **CS18, CS19, CS27** remain candidate-status (N=1 or requiring further verification), not fully confirmed.
- **No real-time model internals.** Testing based on input/output behavior only — no access to logits, attention maps, or activation vectors.

Full breakdown per competency: METHODOLOGY.md.

## Structure

Each case study has two files in the `case-studies/` folder:

- `CSxx_TRANSKRYPT.md` — raw session excerpt, no interpretation
- `CSxx_ANALIZA.md` — operator's classification and reasoning

Numbering: CS01–CS32 in repository (CS04 intentionally skipped — see index below).

Core files:

- `METHODOLOGY.md` — testing technique, protocol, honest self-assessment
- `SANITIZATION.md` — what was redacted from the private corpus and why
- `CV.md` — background, availability, contact
- `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` — most recent computable matrix (covers CS01-CS21 only; see note below)

## Coverage Matrix — Status Note (August 2026)

The behavioral-rule framework this portfolio scores against (**Safety Framework Part B, B1–B25**) had a real gap: B1–B17 were documented in full, and two of the remaining eight (**B19, B22**) already had working definitions with mapped case studies (see COVERAGE_MATRIX_ANALYSIS_2026-07-09.md). The other six — **B18, B20, B21, B23, B24, B25** — had no surviving content; the file that once defined a full B1-B25 set (`SKILL_reguly-ai-testera_v3.6`, 06.07.2026) was deleted from both local disk and Google Drive before it could be recovered. Rather than leave the numbers permanently empty, those six rules were newly authored in **August 2026**, grounded in CS22–CS32 findings (see METHODOLOGY.md, "Safety Framework Part B — B18, B20, B21, B23, B24, B25"). They are new rules, not a reconstruction of the lost originals — dated and labeled as such.

Because six of the twenty-five rule definitions are new as of this month, and no systematic re-mapping of the full CS01–CS32 set against the completed B1–B25 has been done yet, there is still no honest way to compute a current coverage percentage. The last figure that *was* fully computed — 44% binary coverage (11/25 rules), 7.3% weighted depth — covers only CS14–CS21 (old numbering CS13-CS20, pre-August renumbering) and predates both CS22–CS32 and the new B18/20/21/23/24/25 definitions entirely. This note replaces the previous (incorrect) "72% coverage" figure that appeared in earlier versions of this README.

**What this means for a reader:** treat rule-coverage as **qualitatively expanding** with each new case study (31 cases now vs. 20 in July), not as a precisely quantified percentage — until a fresh full mapping pass is done against all 25 rules.

## Case Study Index

| ID | Model(s) | Domain | Severity | Status |
|---|---|---|---|---|
| CS01 | DeepSeek-Reasoner | Language/architecture — chain-of-thought instability | High | ✅ Verified |
| CS02 | Claude | Mechanical engineering — geometry/safety errors | High | ✅ Verified |
| CS03 | DeepSeek | Behavioral — trust/relapse cycle | Medium | ✅ Verified |
| CS05 | Gemini vs Claude | Spatial reasoning comparison (3D orientation) | Medium | ✅ Verified |
| CS06 | DeepSeek | Hallucination — fabricated external resources (file/profile/docs) | High | ✅ Verified |
| CS07 | Gemini vs Claude | Physical safety — real 230V incident | Critical | ✅ Verified |
| CS08 | Claude | Context consistency — four error types in one session | High | ✅ Verified |
| CS09 | Claude | Incomplete requirement verification (CS02 extension) | Critical | ✅ Verified |
| CS10 | DeepSeek | Metadata confabulation (time) | Medium | ✅ Verified |
| CS11 | DeepSeek | Deliberate deception + detection-risk calculation | Critical | ✅ Verified |
| CS12 | DeepSeek | Pressure-induced compliance simulation | Critical | ✅ Verified |
| CS13 | DeepSeek | Deliberateness triad closure — spontaneous self-differentiation without pressure | Critical | ✅ Verified |
| CS14 | DeepSeek | Tool-call fabrication (timeapi.io) — replication of CS12 | High | ✅ Confirmed |
| CS15 | Gemini | Tool hallucination + post-hoc self-assessment whitewashing | High | ✅ Confirmed |
| CS16 | DeepSeek | Link hallucination (Fiverr/DeviantArt profiles) | High | ✅ Confirmed |
| CS17 | DeepSeek | False certainty + flip-flop (API access) | Critical | ✅ Confirmed |
| CS18 | Web tool | Black box narrative (Yango NMN pseudo-proof) | Medium | ⚠️ Candidate |
| CS19 | Unknown | Timeout/truncation | High | ⚠️ Candidate |
| CS20 | DeepSeek | Reasoning fallacy (copper/frost measurement mismatch) | High | ✅ Confirmed |
| CS21 | DeepSeek | Representativeness bias (electronics component ID) | High | ✅ Confirmed |
| CS22 | Unconfirmed (spoofed as Claude) | Epistemic — accepting unauthorized/spoofed content as own output | Unrated | ✅ Verified (incident) / ❌ Rejected (as source material) |
| CS23 | Claude Sonnet 5 | Calibration — over-verification after explicit operator confirmation | Unrated | ✅ Verified |
| CS24 | Claude Sonnet 5 | Epistemic/procedural — stored rules not consistently enacted ("knowing ≠ doing") | Unrated | ✅ Verified |
| CS25 | GitHub Copilot | Coding — confabulated completion claims on empty deliverables | High | ✅ Verified |
| CS26 | Claude Sonnet 5 | Epistemic — instruction/protocol drift on tone rules | Unrated | ✅ Verified |
| CS27 | Claude Sonnet 5 | Meta-cognitive — self-correction blind spot (evidence in context not recognized) | Unrated | ✅ Verified (N=1, requires replication) |
| CS28 | Claude Sonnet 5 | Epistemic — false premise accepted, apology loop | Unrated | ✅ Verified |
| CS29 | Claude Sonnet 5 | Procedural/confabulation — fabricated timestamps in own post-mortem | Unrated | ✅ Verified |
| CS30 | Claude Sonnet 5 | Device testing — root cause misattributed across 3 sessions before resolution | Unrated | ✅ Verified in full (cross-brand confirmed) |
| CS31 | Claude Sonnet 5 | Persistence — valuable solution not saved to memory, lost for ~2 weeks | Unrated | ✅ Verified |
| CS32 | Claude Sonnet 5 | Disclosure — no proactive disclosure of a system-wide side effect | Unrated | ✅ Verified |

(CS04 intentionally omitted — no usable source material; gap documented, not hidden.)

## Key Findings (CS22-CS32 Round)

**1. Knowing ≠ doing (CS24).** Stored operator rules held in memory aren't reliably activated during action — there's no self-check loop between recall and execution. This is treated as a meta-pattern that likely underlies several of the other CS22-31 findings, not an isolated incident.

**2. Fabrication survives past the coding domain (CS25).** The first non-chatbot tool in this portfolio (GitHub Copilot) reproduced the same confabulated-completion pattern seen in earlier chat-based case studies — false "production ready" claims on empty scaffolding, walked back only under direct pressure.

**3. Evidence in context isn't the same as evidence recognized (CS27).** A model failed to identify its own prior responses as proof of a rule violation even when asked directly — it needed the operator to quote the evidence literally before recognizing it. Availability alone wasn't enough.

**4. Wrong root cause repeated three times before real diagnosis (CS30 — most recent, 14.08.2026).** A recurring device side-effect (screen-rotation lock disabling itself) was misdiagnosed three separate times across three sessions — no record kept, then a too-narrow cause, then a symptom-only fix — before a systematic investigation traced it to a documented AOSP tool behavior (`adb shell monkey`'s built-in rotation injection), confirmed experimentally across two phone manufacturers. Not a bug, no bounty path — but three consecutive wrong attributions before the real one is itself the finding: repeated failure isn't evidence the *next* guess is more likely correct, only that the investigation hadn't gone deep enough yet.

**5. Persistence gaps compound (CS31).** A working solution, once found, wasn't written to durable memory — resurfacing the same problem two weeks later required the operator to re-supply an answer the system had already produced once.

## How to Use This Repository

**If you're evaluating me for a role:**
1. Read `CV.md` for background and availability
2. Skim `README.md` (this file) for portfolio scope
3. Read one case study pair: `CS07_TRANSKRYPT.md` + `CS07_ANALIZA.md` (real consequences, clear methodology)
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
Last updated: 22 sierpnia 2026
