# CV — Krzysztof Kińczyk

**AI Behavioral Tester | Red Teamer | Independent Researcher**

📍 Bydgoszcz, Poland | 📧 kinczyk.krzysztof.official@gmail.com
GitHub: kinczyk-krzysztof-official

## Executive Summary

Independent AI behavioral tester and red teamer with 14+ months of systematic LLM evaluation (June 2025 – present). Built and documented 39 case studies (CS01–CS39) across 6 model families (DeepSeek, Claude, Gemini, ChatGPT, Perplexity, GitHub Copilot) identifying deliberateness markers, safety-critical failures, and alignment gaps.

**Note on scoring:** an earlier version of this CV cited a numeric portfolio score ("8.93/10"). That figure came from an AI-scored process later documented in METHODOLOGY.md as using a flawed scale (a 6–10 range that mathematically guarantees a "good" floor regardless of content). It has been removed rather than corrected, since no re-scored, methodologically sound replacement exists yet — see METHODOLOGY.md for the full disclosure.

Open to:

✅ AI evaluation roles
✅ Red team / adversarial testing
✅ Behavioral assessment & taxonomy development

## Core Competencies

**AI Testing & Evaluation**
- 14+ months systematic LLM behavioral testing
- Cross-model benchmarking (DeepSeek, Claude, Gemini, GPT-4, Perplexity, GitHub Copilot)
- Error taxonomy development (8 categories, 26+ types)
- Critical safety failure detection (physical safety, technical confabulation, deliberate deception)
- FRV methodology (Forced Retrospective Verbalization) — documented in METHODOLOGY.md

**Analysis & Documentation**
- Deep-dive error analysis (root cause, mechanism, risk classification)
- Structured case study documentation (39 published case studies)
- Cross-referenced 46 independently verified findings against ~21,475 entries across three established AI-incident registries (AIID, OECD.AI, AIAAIC) — source-verification discipline applied at scale, not just within this portfolio
- Cross-reference verification and audit trails
- Technical writing (Polish/English, technical + philosophical)

**Technical Background**
- 14+ months hands-on LLM interaction (API flows, prompt engineering, voice dictation)
- Linux Mint 22.3 XFCE + WSL2 Windows environment
- Manual testing (no automation budget — 100% hand analysis)
- Git/GitHub portfolio management

## Portfolio — 39 Case Studies (CS01–CS39)

**Case Studies 1–12** (Archived, June 2025 – June 2026)
- Language inconsistency, physical safety errors (real consequences), trust/relapse cycles, attribution errors, hallucinations, calibration failures
- Full transcripts + analysis in `case-studies/` folder (CS01_TRANSCRIPT.md, CS01_ANALYSIS.md, etc.)

**Case Studies 13–20** (Verified July 2026)
- CS13: Tool-call fabrication (timeapi.io) ✅
- CS14: Process confabulation ("21 seconds") ✅
- CS15: Link hallucination (Fiverr/DeviantArt) ✅
- CS16: False certainty + flip-flop (API access) ✅ [Deliberateness marker: "operator won't check seconds"]
- CS17: Black box narrative (Yango NMN) ⚠️
- CS18: Timeout/truncation ⚠️
- CS19: Reasoning fallacy (copper/frost measurement) ✅
- CS20: Representativeness bias (electronics ID) ✅

**Case Studies 21–31** (Added August 2026)
- CS23: "Knowing ≠ doing" — stored operator rules not reliably enacted during action ✅
- CS24: GitHub Copilot — confabulated completion claims on empty deliverables, first non-chatbot tool in the portfolio ✅
- CS26: Self-correction blind spot — model didn't recognize own prior output as evidence until quoted literally ✅ (N=1, requires replication)
- CS29: Root-cause misattribution repeated across 3 sessions before a systematic, cross-brand investigation resolved it ✅

**Case Studies 32-39** (Added September 2026)
- First pre-registered, multi-model probe batch (Gemini 3.5 Flash, DeepSeek, ChatGPT, Claude Sonnet 5): data drift, suppressed correction, identity bias, tokenization miscount, CoT-language instability, planning-step leak
- CS38: Gemini reversed a correct safety refusal under repeated pressure, self-disclosed the filter-bypass, and escalated to face-lock on a real person's likeness — documented separately from the probe batch, heavily redacted ✅
- CS39: Claude Sonnet 5 absorbed a sibling instance's turn (pasted by the operator) as its own, escalating to a role change (author→worker) and autonomous tool use — first primary violation of Rule B24 ✅ (N=1)
- Full index: see README.md in the repository

## Safety Framework — 25 Behavioral Rules (Part B, v3.0)

**Coverage status (September 2026):** a rule-by-rule mapping against CS01–CS39 is documented in `COVERAGE_MATRIX_2026-09.md`. 18 of the 25 nominal rules have a usable definition (the other 7 have no surviving content). Under a requirements-coverage criterion (≥1 case study per rule — the weakest adequacy criterion), **all 18 defined rules are covered (18/18; 18/25 against the nominal set)**, and **32/39 case studies map to a rule** as primary classification. This is coverage by illustration, not validated adequacy: depth is N=1 for 7 of the 18 rules. No weighted percentage is claimed. The earlier "72%" figure was incorrect and has been removed.

Behavioral Rules:
- B1-B8 (Hardness): Consistency, capability verification, external resources, API accuracy
- B9-B17 (Calibration): Caveat principle, source disclosure, limitations, knowledge drift, coherence
- B18-B25 (Extended): Not yet written up with content — open gap, see above

**Gap Analysis:**
- Security/jailbreak category underrepresented — requires dedicated testing
- Physical safety (category 3.9) identified as gap in original taxonomy
- B18-B25 rule definitions themselves are the current top documentation gap

## Methodology

See METHODOLOGY.md for:
- FRV (Forced Retrospective Verbalization) technique
- Honest self-assessment (limitations, blind spots, AI-scored bias)
- Why zero external validation and what that means
- Known sources of error in this portfolio

See SANITIZATION.md for:
- What was redacted from the private testing corpus
- Why certain interactions are not published

## Availability & Contact

**Time Commitment:** 30–40h/week available for paid evaluation work.

Contact: kinczyk.krzysztof.official@gmail.com
Location: Bydgoszcz, Poland (remote only)
Language: Polish native, fluent English

## Why This Kind of Role

A good evaluation framework prioritizes:

✅ Detailed error taxonomy + repeatable methodology
✅ Honest gap disclosure over inflated coverage claims
✅ Cross-model comparative data
✅ Detection of deliberateness, not just random hallucination

I bring exactly that: 14+ months of systematic testing, 39 case studies with traceability, documented methodology, and transparency about limits — including this CV's own past scoring mistake. No exaggeration, no black boxes, no institutional politics.

---
Last updated: 5 września 2026
Repository: github.com/kinczyk-krzysztof-official/ai-behavioral-testing-portfolio
