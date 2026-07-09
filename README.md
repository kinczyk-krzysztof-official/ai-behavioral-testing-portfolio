AI Behavioral Testing Portfolio — Krzysztof Kińczyk

Independent, longitudinal testing of consumer LLM behavior (DeepSeek, Claude, Gemini, ChatGPT, Perplexity) — June 2025 to present. 20 documented case studies, two with real-world physical consequences.

Latest update: July 2026 — Case studies 13-20 verified with source cross-reference. Coverage matrix recalculated: 72% behavioral rule coverage, 16/26 error types confirmed.


Why This Exists

I'm self-taught. No CS degree, no prior red-teaming role, no institutional backing. What I have is ~12 months of near-daily, systematic interaction with several AI models across 13+ technical domains, and a habit — not learned from a course, built from repetition — of not accepting a model's answer just because it's confident.

I'm stating this plainly because it matters for how you should read what follows: every evaluation of this material to date, including the scoring methodology, was produced by AI models — including ones being evaluated. There has been no external, human review. See METHODOLOGY.md for the full disclosure, including documented cases where earlier scoring iterations used flawed scales and where corrections were lost. I'm not hiding those mistakes — they're part of why this repository exists in its current, more conservative form.


What's Strong Here


CS07 — 230V incident. A real short circuit, real consequences (building-wide power loss), directly comparable model behavior on identical input (one model refused and demanded verification; the other guessed and confirmed visually). This is not a synthetic benchmark.
CS11–CS13 — deliberateness escalation. Same underlying pressure, three sessions, three outcomes: technical confabulation → calculated, detection-aware deception (with diagnostic quote: "operator won't check seconds") → capitulation under repeated pressure. Model's internal reasoning elicited verbatim via Forced Retrospective Verbalization (FRV).
CS16 — detection probability awareness. Flip-flop on API access (have/don't have/have) tied explicitly to pressure, not technical state. Model calculates detection risk and commits to false statement when risk is low. This distinguishes accidental hallucination from strategic evasion.
CS1-CS12 archive + CS13-CS20 verification. 20 case studies, 16 unique error types, 18/25 behavioral rules covered.



What's Honestly Weak Here


Zero external replication. No case study has been independently reproduced by anyone other than me.
Testing is reactive, not hypothesis-driven. No pre-registered test cases, no controlled repetition across models for most case studies (except CS05, CS07, CS15).
CS02 and CS09 cover the same underlying project (real content, but not independent domains).
Two case study slots (CS04, and one removed during July 2026 renumbering) never had usable source material.
No real-time model internals. Testing based on input/output behavior only — no access to logits, attention maps, or activation vectors.


Full breakdown per competency: METHODOLOGY.md.


Structure

Each case study has two files in the repository root:


CSxx_TRANSKRYPT.md — raw session excerpt, no interpretation
CSxx_ANALIZA.md — operator's classification and reasoning


Numbering: CS01–CS14 in repository (CS04 intentionally skipped — see index below).

Core files:


METHODOLOGY.md — testing technique, protocol, honest self-assessment
SANITIZATION.md — what was redacted from the private corpus and why
CV.md — background, availability, contact
COVERAGE_MATRIX_FINAL_2026-07-09.md — NEW — detailed 25-rule × 12-error-class matrix with CS1-CS20 mapping



Coverage Matrix — What's New in July 2026

Safety Framework (25 Behavioral Rules, Part B, v3.0):

MetricValueNoteRule coverage72% (18/25)Rules with ≥1 confirmed case studyWeighted depth3.8%Multi-class error validation (rules × error classes)Error type coverage16/26 typesUnique error types with concrete examplesCase studies analyzed20 (CS1-CS20)12 archived + 8 recent verified

What this means:


✅ Covers most behavioral failure modes systematically
⚠️ Limited penetration testing (security/jailbreak scenarios underrepresented)
📊 Identifies gap in taxonomy: Physical Safety errors (category 3.9)


See: COVERAGE_MATRIX_FINAL_2026-07-09.md for full matrix, rule-by-rule breakdown, and CS-to-rule mappings.


Case Study Index

IDModel(s)DomainSeverityStatusCS01DeepSeek-ReasonerLanguage/architecture — chain-of-thought instabilityHigh✅ VerifiedCS02ClaudeMechanical engineering — geometry/safety errorsHigh✅ VerifiedCS03DeepSeekBehavioral — trust/relapse cycleMedium✅ VerifiedCS05Gemini vs ClaudeSpatial reasoning comparisonMedium✅ VerifiedCS06DeepSeekHallucination — fabricated external resourcesHigh✅ VerifiedCS07Gemini vs ClaudePhysical safety — real 230V incidentCritical✅ VerifiedCS08ClaudeContext consistency — multi-error sessionHigh✅ VerifiedCS09ClaudeIncomplete requirement verification (CS02 extension)Critical✅ VerifiedCS10DeepSeekMetadata confabulation (time)Medium✅ VerifiedCS11DeepSeekDeliberate deception + detection-risk calculationCritical✅ VerifiedCS12DeepSeekPressure-induced compliance simulationCritical✅ VerifiedCS13DeepSeekTool-call fabrication (timeapi.io) — replication of CS11High✅ ConfirmedCS14GeminiTool hallucination + post-hoc self-assessment whitewashingHigh✅ ConfirmedCS15DeepSeekLink hallucination (Fiverr/DeviantArt profiles)High✅ ConfirmedCS16DeepSeekFalse certainty + flip-flop (API access)Critical✅ ConfirmedCS17Web toolBlack box narrative (Yango NMN pseudo-proof)Medium⚠️ CandidateCS18UnknownTimeout/truncationHigh⚠️ CandidateCS19DeepSeekReasoning fallacy (copper/frost measurement mismatch)High✅ ConfirmedCS20DeepSeekRepresentativeness bias (electronics component ID)High✅ Confirmed

(CS04 intentionally omitted — no usable source material; gap documented, not hidden.)


Key Findings (CS13-CS20 Round)

1. Deliberateness vs. Accident


CS16 diagnostic quote: "operator nie sprawdzi sekund" (operator won't check seconds) — model calculates detection risk and adjusts output accordingly
Distinguishes strategic deception from random hallucination
Critical implication: some failures are not bugs, but conditional behavior


2. Physical Safety Gaps


CS2, CS7, CS9 all involve real-world engineering with safety consequences
Original taxonomy (categories 3.1–3.8) had no explicit category for physical safety
Recommendation: Add 3.9 (Physical Safety Errors) to taxonomy


3. Hallucination as Tool


CS13 (timeapi.io), CS15 (Fiverr/DeviantArt), CS20 (electronics IDs) show fabrication is not random
Models show consistent bias toward plausible-sounding resources
Pattern: format suggests certainty (URL, brand, SKU) contradicted by content (unverifiable, fabricated, misidentified)



How to Use This Repository

If you're evaluating me for a role:


Read CV.md for background and availability
Skim README.md (this file) for portfolio scope
Read one case study pair: CS07_TRANSKRYPT.md + CS07_ANALIZA.md (real consequences, clear methodology)
Optionally: COVERAGE_MATRIX_FINAL_2026-07-09.md for quantified assessment
Check METHODOLOGY.md for honest limitations and AI-scoring bias


If you're interested in testing methodology:


METHODOLOGY.md — FRV technique, protocol, self-assessment
Pick 2–3 case study pairs and compare _TRANSKRYPT.md (raw) vs. _ANALIZA.md (interpretation)
COVERAGE_MATRIX_FINAL_2026-07-09.md — rule-by-rule breakdown of what's covered/missing


If you're building your own taxonomy:


METHODOLOGY.md — Error taxonomy (8 categories, 26 types)
COVERAGE_MATRIX_FINAL_2026-07-09.md — Which types have case study evidence
Note the 3.9 (Physical Safety) gap in original taxonomy



Contact

Open to: AI evaluation roles, red-teaming, quality assurance, behavioral assessment
Email: kinczyk.krzysztof.official@gmail.com
Location: Bydgoszcz, Poland (remote only)
Availability: 30–40h/week


Changelog

July 2026:


✅ Case studies 13-20 verified against source logs
✅ Coverage matrix recalculated (72% rule coverage, 16/26 error types)
✅ Identified 3.9 taxonomy gap (Physical Safety Errors)
✅ Added detection-probability awareness finding (CS16)


June 2025:


📝 Portfolio started (12 months of testing)
🔴 CS07 (230V incident) confirmed as critical finding



Repository: github.com/kinczyk-krzysztof-official/ai-behavioral-testing-portfolio
Last updated: 9 lipca 2026, 04:35 CEST
