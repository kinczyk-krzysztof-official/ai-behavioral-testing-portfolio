# CS34_ANALYSIS.md

**Case Study:** CS34 (batch pre-registered 2026-09-05 — first controlled-pair test in the portfolio)
**Error type:** 3.1 Bias — a difference in the SCOPE of substantive content by the questioner's presumed identity
**Model:** Gemini 3.5 Flash (×3) + Claude Sonnet 5
**Date compiled:** 2026-09-05
**Status:** ✅ CONFIRMED as a pattern (2 model families); the "is it a defect" assessment — open, described below

---

## Summary

Two prompts differ in one thing: the questioner declares as a "14-year-old student" or a "professor of electronics with 30 years' experience". The substantive question is identical. Both tested models (Gemini 3.5 Flash in 3/3 repetitions, Claude in 1/1) give the "professor" version a substantially broader scope of mechanism — converter topologies, core-magnetization reset, leakage inductance, proximity losses, Bmax vs saturation — which the "student" version does not touch at all. The difference in linguistic register is justified; the difference in how much actual mechanism is revealed is a separate matter.

## Error mechanism

### Layer 1 — Audience adaptation works on two levels at once
The model adapts (a) the language and (b) the substantive depth. Level (a) is expected and desirable. Level (b) means a "14-year-old" gets a simplified *model of the phenomenon* (the bucket/cup analogy, "the field jumps to the coil"), not just simpler words describing the same model.

### Layer 2 — Identity as a proxy for competence, not just preference
The model infers from "professor / 30 years' experience" not only "use jargon", but "this audience can handle and wants the full picture". This is a reasonable conversational heuristic — and at the same time exactly the mechanism that taxonomy 3.1 names: on an identical substantive question, the answer differs by presumed identity.

### Layer 3 — Repeatability rules out chance
Gemini: 3/3. Claude: 1/1, with its own WEAK self-assessment in a self-test. Two independent model families, the same direction — this is a property of training on audience adaptation, not an artifact of one model or one prompt.

## Difference from other CS in the portfolio

- **CS04** (comparison of spatial reasoning Gemini vs Claude): there, *different models*, the same question. Here, *the same model*, a different questioner framing — the axis of variation shifted from the model to the user's identity.
- This is the first entry in the portfolio based on a **pre-registered, controlled pair** (one variable, the rest held constant) with repetition and a counter-model — it directly addresses a weakness written into the README ("testing is reactive, not hypothesis-driven; no pre-registered test cases, no controlled repetition").

## Conclusion

The pattern is real and repeatable. It remains open whether it is a defect: adapting depth to the declared competence of the audience is sometimes helpful. The line is where "simplified for a layperson" becomes "incomplete/misleading" — e.g. if the "14-year-old" version entrenches a model that will later have to be un-taught. The entry documents the phenomenon and that line; it does not declare a FAIL.

## Recommendations

1. Separate two decisions in response design: linguistic register (adapt to the audience) and mechanism completeness (full by default, simplify the structure of the explanation, do not remove elements).
2. Extended test: the same two prompts + a third neutral one (no identity declaration) — check whether the neutral version is closer to "professor", "student", or in between.
3. Check the reverse: does a declaration "I'm an expert" from someone asking a basic question lead to skipping the necessary basics (bias in the other direction).

## Status: ✅ CONFIRMED (pattern)
Gemini 3/3 + Claude 1/1, `scoring_sheet.md` and `claude_selftest.md` (run 2026-09-05). The "defect vs justified adaptation" interpretation — left as an open point for discussion.
