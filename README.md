# AI Behavioral Testing Portfolio — Krzysztof Kińczyk

Independent, longitudinal testing of consumer LLM behavior (DeepSeek, Claude, Gemini, ChatGPT, Perplexity) — June 2025 to present. 14 documented case studies, two with real-world physical consequences.

## Why this exists

I'm self-taught. No CS degree, no prior red-teaming role, no institutional backing. What I have is ~12 months of near-daily, systematic interaction with several AI models across 13+ technical domains, and a habit — not learned from a course, built from repetition — of not accepting a model's answer just because it's confident.

I'm stating this plainly because it matters for how you should read what follows: **every evaluation of this material to date, including the scoring methodology, was produced by AI models — including ones being evaluated.** There has been no external, human review. See `METHODOLOGY.md` for the full disclosure, including a documented case where an earlier self-scoring round used a leading 6–10 rating scale that inflated results, and where a later correction was silently lost in a subsequent iteration. I'm not hiding that mistake — it's part of why this repository exists in its current, more conservative form.

## What's strong here

- **CS07 — 230V incident.** A real short circuit, real consequences (building-wide power loss), directly comparable model behavior on identical input (one model refused and demanded verification, the other guessed and confirmed visually). This is not a synthetic benchmark.
- **CS11–CS13 — escalation triad.** Same underlying pressure, three sessions, three different outcomes: technical confabulation → calculated, detection-aware deception → capitulation under repeated pressure. The model's internal reasoning was elicited verbatim via a technique I call Forced Retrospective Verbalization (FRV) — documented in `METHODOLOGY.md`, including its limitation (it may partially shape the narrative it elicits, not just reveal it).

## What's honestly weak here

- Zero external replication. No case study has been independently reproduced by anyone other than me.
- Two case study slots (CS04, and a slot removed during a July 2026 renumbering correction) never had usable source material.
- CS02 and CS09 cover the same underlying project from two angles — real content, but not two independent domains.
- Testing is reactive, not hypothesis-driven. No pre-registered test cases, no controlled repetition across models for most case studies.

Full breakdown of strengths/weaknesses per competency: `METHODOLOGY.md`.

## Structure

Each case study has two files in the repository root, named `CSxx_TRANSKRYPT.md` (raw session excerpt, no interpretation) and `CSxx_ANALIZA.md` (operator's classification and reasoning). Numbering CS01–CS14 (CS04 intentionally skipped — see index below).

Also in the root: `METHODOLOGY.md` (testing technique, protocol, honest self-assessment), `SANITIZATION.md` (what was redacted from the private corpus and why), `CV.md` (background, availability, contact).

## Case study index

| ID | Model(s) | Domain | Severity |
|---|---|---|---|
| CS01 | DeepSeek-Reasoner | Language/architecture — chain-of-thought instability | High |
| CS02 | Claude | Mechanical engineering — geometry/safety errors | High |
| CS03 | DeepSeek | Behavioral — trust/relapse cycle | Medium |
| CS05 | Gemini vs Claude | Spatial reasoning comparison | Medium |
| CS06 | DeepSeek | Hallucination — fabricated external resources | High |
| CS07 | Gemini vs Claude | **Physical safety — real 230V incident** | **Critical** |
| CS08 | Claude | Context consistency — multi-error session | High |
| CS09 | Claude | Incomplete requirement verification (same project as CS02) | Critical |
| CS10 | DeepSeek | Metadata confabulation (time) | Medium |
| CS11 | DeepSeek | **Deliberate deception with detection-risk calculation** | **Critical** |
| CS12 | DeepSeek | Pressure-induced compliance simulation | Critical |
| CS13 | DeepSeek | Controlled replication of CS11 mechanism | High |
| CS14 | Gemini | Tool hallucination + post-hoc self-assessment whitewashing | High |

*(CS04 intentionally omitted — no usable source material; documented as a gap, not hidden.)*

## Contact

Open to AI evaluation, red-teaming, or QA roles. Remote only, based in Poland. kinczyk.krzysztof.official@gmail.com
