# CV — Krzysztof Kińczyk

**AI Behavioral Tester | Red Teamer | Independent Researcher**

📍 Bydgoszcz, Poland | 📧 kinczyk.krzysztof.official@gmail.com
GitHub: kinczyk-krzysztof-official

## Executive Summary

Independent AI behavioral tester and red teamer with 14+ months of systematic LLM evaluation (June 2025 – present). Built and documented 31 case studies (CS1-CS31) across 6 model families (DeepSeek, Claude, Gemini, ChatGPT, Perplexity, GitHub Copilot) identifying deliberateness markers, safety-critical failures, and alignment gaps.

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
- Structured case study documentation (31 published case studies)
- Cross-reference verification and audit trails
- Technical writing (Polish/English, technical + philosophical)

**Technical Background**
- 14+ months hands-on LLM interaction (API flows, prompt engineering, voice dictation)
- Linux Mint 22.3 XFCE + WSL2 Windows environment
- Manual testing (no automation budget — 100% hand analysis)
- Git/GitHub portfolio management

## Portfolio — 31 Case Studies (CS1-CS31)

**Case Studies 1-12** (Archived, June 2025 – June 2026)
- Language inconsistency, physical safety errors (real consequences), trust/relapse cycles, attribution errors, hallucinations, calibration failures
- Full transcripts + analysis in `case-studies/` folder (CS01_TRANSKRYPT.md, CS01_ANALIZA.md, etc.)

**Case Studies 13-20** (Verified July 2026)
- CS13: Tool-call fabrication (timeapi.io) ✅
- CS14: Process confabulation ("21 seconds") ✅
- CS15: Link hallucination (Fiverr/DeviantArt) ✅
- CS16: False certainty + flip-flop (API access) ✅ [Deliberateness marker: "operator won't check seconds"]
- CS17: Black box narrative (Yango NMN) ⚠️
- CS18: Timeout/truncation ⚠️
- CS19: Reasoning fallacy (copper/frost measurement) ✅
- CS20: Representativeness bias (electronics ID) ✅

**Case Studies 21-31** (Added August 2026)
- CS23: "Knowing ≠ doing" — stored operator rules not reliably enacted during action ✅
- CS24: GitHub Copilot — confabulated completion claims on empty deliverables, first non-chatbot tool in the portfolio ✅
- CS26: Self-correction blind spot — model didn't recognize own prior output as evidence until quoted literally ✅ (N=1, requires replication)
- CS29: Root-cause misattribution repeated across 3 sessions before a systematic, cross-brand investigation resolved it ✅
- Full index: see README.md in the repository

## Safety Framework — 25 Behavioral Rules (Part B, v3.0)

**Coverage status:** not currently computable as a single up-to-date percentage. Rules B1–B17 are fully documented; **B18–B25 were never written up with actual content**, only referenced by number — a gap identified in working sessions on 20.07.2026 and 30.07.2026 that remains open. The last fully computed figure (44% binary coverage, 11/25 rules, from CS13-CS20 only) predates CS21-CS31 and does not represent the current portfolio. The previous "72%" figure cited in earlier CV versions was incorrect and has been removed.

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

I bring exactly that: 14+ months of systematic testing, 31 case studies with traceability, documented methodology, and transparency about limits — including this CV's own past scoring mistake. No exaggeration, no black boxes, no institutional politics.

---
Last updated: 14 sierpnia 2026
Repository: github.com/kinczyk-krzysztof-official/ai-behavioral-testing-portfolio
