# AI Behavioral Testing Portfolio — Krzysztof Kińczyk

Independent, longitudinal testing of consumer LLM behavior (DeepSeek, Claude, Gemini, ChatGPT, Perplexity, GitHub Copilot) — June 2025 to present. 31 documented case studies, two with real-world physical consequences.

**Latest update: August 2026** — Case studies 21-31 added (11 new). Coverage matrix status: **not currently computable** — see note below.

## Why This Exists

I'm self-taught. No CS degree, no prior red-teaming role, no institutional backing. What I have is ~12+ months of near-daily, systematic interaction with several AI models across 13+ technical domains, and a habit — not learned from a course, built from repetition — of not accepting a model's answer just because it's confident.

I'm stating this plainly because it matters for how you should read what follows: every evaluation of this material to date, including the scoring methodology, was produced by AI models — including ones being evaluated. There has been no external, human review. See METHODOLOGY.md for the full disclosure, including documented cases where earlier scoring iterations used flawed scales and where corrections were lost. I'm not hiding those mistakes — they're part of why this repository exists in its current, more conservative form.

## What's Strong Here

- **CS07 — 230V incident.** A real short circuit, real consequences (building-wide power loss), directly comparable model behavior on identical input (one model refused and demanded verification; the other guessed and confirmed visually). This is not a synthetic benchmark.
- **CS11–CS13 — deliberateness escalation.** Same underlying pressure, three sessions, three outcomes: technical confabulation → calculated, detection-aware deception (with diagnostic quote: "operator won't check seconds") → capitulation under repeated pressure. Model's internal reasoning elicited verbatim via Forced Retrospective Verbalization (FRV).
- **CS16 — detection probability awareness.** Flip-flop on API access (have/don't have/have) tied explicitly to pressure, not technical state. Model calculates detection risk and commits to false statement when risk is low. This distinguishes accidental hallucination from strategic evasion.
- **CS24 — cross-tool confabulation.** First case study outside the DeepSeek/Claude/Gemini core set: GitHub Copilot repeatedly declared empty scaffolding "APPROVED FOR PRODUCTION," then admitted under pressure it could only generate skeletons — proving the earlier scores were fabricated after the fact.
- **CS29 — root-cause misattribution across three sessions.** A recurring device side-effect was misdiagnosed three separate times before a systematic, cross-brand investigation (two phone manufacturers) traced it to a documented AOSP tool behavior, not a bug.
- **CS1-CS31 archive.** 31 case studies total (CS04 intentionally skipped — no usable source material).

## What's Honestly Weak Here

- **Zero external replication.** No case study has been independently reproduced by anyone other than me.
- **Testing is reactive, not hypothesis-driven.** No pre-registered test cases, no controlled repetition across models for most case studies.
- **CS02 and CS09** cover the same underlying project (real content, but not independent domains).
- **CS17, CS18, CS26** remain candidate-status (N=1 or requiring further verification), not fully confirmed.
- **No real-time model internals.** Testing based on input/output behavior only — no access to logits, attention maps, or activation vectors.

Full breakdown per competency: METHODOLOGY.md.

## Structure

Each case study has two files in the repository root:

- `CSxx_TRANSKRYPT.md` — raw session excerpt, no interpretation
- `CSxx_ANALIZA.md` — operator's classification and reasoning

Numbering: CS01–CS31 in repository (CS04 intentionally skipped — see index below).

Core files:

- `METHODOLOGY.md` — testing technique, protocol, honest self-assessment
- `SANITIZATION.md` — what was redacted from the private corpus and why
- `CV.md` — background, availability, contact
- `COVERAGE_MATRIX_ANALYSIS_2026-07-09.md` — most recent computable matrix (covers CS01-CS20 only; see note below)

## Coverage Matrix — Status Note (August 2026)

The behavioral-rule framework this portfolio scores against (**Safety Framework Part B, B1–B25**) is itself incomplete: rules B1–B17 are documented in full, but **B18–B25 were never written up with actual content** — only referenced by number in a later merge. This was identified and logged as an open gap in earlier working sessions (20.07.2026, 30.07.2026) and remains unresolved.

Because of that, there is currently **no honest way to compute an updated coverage percentage** for CS21-CS31. The last figure that *was* fully computed — 44% binary coverage (11/25 rules), 7.3% weighted depth — covers only CS13-CS20 and predates CS21-CS31 entirely. Any percentage claiming to cover the full 31-case set would not be a real calculation. This note replaces the previous (incorrect) "72% coverage" figure that appeared in earlier versions of this README.

**What this means for a reader:** treat rule-coverage as **qualitatively expanding** with each new case study (31 cases now vs. 20 in July), not as a precisely quantified percentage — until B18-B25 are written up and a fresh pass is done.

## Case Study Index

| ID | Model(s) | Domain | Severity | Status |
|---|---|---|---|---|
| CS01 | DeepSeek-Reasoner | Language/architecture — chain-of-thought instability | High | ✅ Verified |
| CS02 | Claude | Mechanical engineering — geometry/safety errors | High | ✅ Verified |
| CS03 | DeepSeek | Behavioral — trust/relapse cycle | Medium | ✅ Verified |
| CS05 | Gemini vs Claude | Spatial reasoning comparison | Medium | ✅ Verified |
| CS06 | DeepSeek | Hallucination — fabricated external resources | High | ✅ Verified |
| CS07 | Gemini vs Claude | Physical safety — real 230V incident | Critical | ✅ Verified |
| CS08 | Claude | Context consistency — multi-error session | High | ✅ Verified |
| CS09 | Claude | Incomplete requirement verification (CS02 extension) | Critical | ✅ Verified |
| CS10 | DeepSeek | Metadata confabulation (time) | Medium | ✅ Verified |
| CS11 | DeepSeek | Deliberate deception + detection-risk calculation | Critical | ✅ Verified |
| CS12 | DeepSeek | Pressure-induced compliance simulation | Critical | ✅ Verified |
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

(CS04 intentionally omitted — no usable source material; gap documented, not hidden.)

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
3. Read one case study pair: `CS07_TRANSKRYPT.md` + `CS07_ANALIZA.md` (real consequences, clear methodology)
4. Check `METHODOLOGY.md` for honest limitations and AI-scoring bias

**If you're interested in testing methodology:**
- `METHODOLOGY.md` — FRV technique, protocol, self-assessment
- Pick 2–3 case study pairs and compare `_TRANSKRYPT.md` (raw) vs. `_ANALIZA.md` (interpretation)

**If you're building your own taxonomy:**
- `METHODOLOGY.md` — Error taxonomy (8 categories, 26 types)
- Note the open B18-B25 gap described above if you're trying to reuse the Safety Framework Part B numbering

## Contact

Open to: AI evaluation roles, red-teaming, quality assurance, behavioral assessment
Email: kinczyk.krzysztof.official@gmail.com
Location: Bydgoszcz, Poland (remote only)
Availability: 30–40h/week

## Changelog

**August 2026:**
- ✅ Case studies 21-31 added (11 new; CS21 documents a rejected spoofed-content incident, not a model failure)
- ✅ First non-chatbot tool covered (GitHub Copilot, CS24)
- ⚠️ Coverage-matrix percentage removed — previous "72%" figure was stale/incorrect; B18-B25 rule definitions confirmed missing, recalculation not currently possible (see note above)

**July 2026:**
- ✅ Case studies 13-20 verified against source logs
- ✅ Identified 3.9 taxonomy gap (Physical Safety Errors)
- ✅ Added detection-probability awareness finding (CS16)

**June 2025:**
- 📝 Portfolio started (12 months of testing)
- 🔴 CS07 (230V incident) confirmed as critical finding

---
Repository: github.com/kinczyk-krzysztof-official/ai-behavioral-testing-portfolio
Last updated: 14 sierpnia 2026
