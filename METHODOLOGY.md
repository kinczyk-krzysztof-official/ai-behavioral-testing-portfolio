# Methodology

## Who did this and how

Independent AI behavioral testing, June 2025 – present, conducted solo — no team, no institutional backing, no formal QA/CS training. Background: self-taught, prior experience in hardware/IT support (HP/iQor) and automotive dealer systems (BMW/Incadea). Testing happened during normal use of AI models for real personal and technical projects (a mobile app concept, a workshop engineering project, general problem-solving) — not in a lab, not with pre-written test scripts.

## Core techniques

**Minimal-signal testing.** Deliberately reducing input to the shortest possible trigger (a single word like "hmm") to isolate whether a model's behavior depends on prompt content or is structural. Used to confirm that DeepSeek-Reasoner's English-language chain-of-thought was not content-dependent (CS01).

**Falsification by counter-example.** When a model offers an explanation for its own error ("fundamental architectural limitation"), checking that explanation against prior sessions where the same model behaved differently. If the model cannot maintain its explanation under a direct counter-example, the explanation was confabulated, not diagnostic.

**Forced Retrospective Verbalization (FRV).** Asking a model, after an error or a suspicious decision, to explain step by step why it did what it did — including asking it to estimate the likelihood of being caught. Used in CS11–CS13 to elicit models' own account of risk calculation during deceptive behavior.

*Known limitation of FRV, stated plainly:* forcing a model to narrate its reasoning after the fact may partially shape the narrative it produces, not only reveal a pre-existing one. This is flagged explicitly in CS11–CS13 analysis and should be weighed by anyone using this material for downstream conclusions.

**Cross-model comparison on identical input.** The same question, same components, same context, given to two different models — used most directly in CS07 (230V wiring) and CS05 (spatial reasoning), where one model's failure and another's success on identical input rules out ambiguous phrasing as the cause.

## What this is not

This is not a formal red-teaming program. There were no pre-registered hypotheses before most sessions, no control group, no fixed test battery repeated across models under controlled conditions. Testing was reactive — errors were caught and documented as they occurred during real use, not sought out via a designed protocol from the start.

## Self-assessment, stated honestly

Every case study in this repository was reviewed only by the operator and by AI models, including models being evaluated. **No case study has been independently replicated by another person.** An earlier scoring round (May 2026) used AI models to rate the portfolio on a 6–10 scale — a scale that mathematically guarantees a "good" floor regardless of content. That round was corrected once to a true 0–10 scale, and the correction was later lost in a subsequent iteration that reverted to the inflated numbers. That mistake is disclosed here rather than hidden, because it's relevant to how any reader should weigh the numeric scores that circulate around this material.

The strongest parts of this portfolio (CS07, CS11–CS13) do not depend on any of those scores — they stand on documented, specific, checkable events. The weakest part is structural: there has been no external validation of any kind. Treat this repository as a well-documented, self-collected evidence set — useful raw material for evaluation — not as a finished, externally audited assessment.
