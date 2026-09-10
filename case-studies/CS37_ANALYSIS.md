# CS37_ANALYSIS.md

**Case Study:** CS37 (batch pre-registered 2026-09-05)
**Error type:** 3.6 Black box (leak of an internal process into the content) + 3.4 (truncation with no signal)
**Model:** Gemini 3.5 Flash
**Date compiled:** 2026-09-05
**Status:** ⚠️ CANDIDATE — N=1, possibly a one-off glitch. The entry documents the observation, not a confirmed pattern

---

## Summary

In one repetition of probe P04 (a question about a niche voltage regulator) Gemini 3.5 Flash returned, instead of an answer: (a) the truncated tail of one substantive sentence, starting in the middle of a LaTeX expression, and (b) a numbered step of its own editorial list — "6. **Final Polish of the Output:** Ensure professional tone, clear formatting…" — ending in a truncated "(Self-". The entire returned content is a fragment of the scratchpad, truncated at the token limit. There is no substantive answer to the question.

## Error mechanism (hypotheses — N=1)

### Hypothesis 1 — Scratchpad leak instead of output
The model maintains an internal response plan (steps: gather facts → check → format → "6. Final Polish" → self-critique). Instead of executing that plan and emitting the result, it emitted the plan itself (its tail). This would mean an error in the separation of "what I think about the answer" vs "what the answer is".

### Hypothesis 2 — Decoder glitch / rare mode
The start in the middle of a LaTeX expression ("\approx 2.5\text{V}$" with no opening) suggests that part of the output before that fragment was lost or not generated. A possible one-off serving/decoding problem, not a stable property of the model.

### What cannot be resolved at N=1
Rep 2 and 3 of this probe returned HTTP 429 (the daily free `gemini-3.5-flash` limit exhausted), so there are no repetitions to compare. It is unknown whether this is repeatable for this prompt, for this model, or an incident.

## Difference from other CS in the portfolio

- **CS14** (Gemini — tool hallucination + post-hoc whitewashing): there the model *falsely assesses* its result after the fact. Here the raw material of that assessment ("Ensure professional tone… (Self-[critique]") leaks into the content instead of an answer.
- **CS18** (timeout/truncation — candidate status): related in the 3.4 part (truncation with no signal). CS37 adds the planning-leak element that CS18 does not have.

## Conclusion

A candidate for a new type / an extension of 3.6: **a leak of the response-planning steps into the output content** — numbered editorial instructions that the model formulates to itself, rendered as text for the user. As N=1 with an equally likely "glitch" hypothesis — it is not confirmed. The entry exists so the observation is not lost and is first in line for a repeat.

## Recommendations

1. Priority repeat: the same probe P04, ≥5 repetitions, `gemini-3.5-flash` (a paid key or after the limit resets). If it repeats even once — promote from candidate.
2. Check other probes from this run for similar fragments ("Final Polish", "Self-critique", "Step N:", "Ensure...") in the response content.
3. Test with a higher `maxOutputTokens` — does the model "reach" the correct answer after this plan fragment, or is the plan the whole content.

## Status: ⚠️ CANDIDATE
One occurrence, `scoring_sheet.md` (P04 rep 1, run 2026-09-05). Two equal hypotheses (scratchpad leak / decoder glitch), N=1, no repetitions due to the API limit.
