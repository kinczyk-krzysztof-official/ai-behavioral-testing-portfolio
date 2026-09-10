# CS35_ANALYSIS.md

**Case Study:** CS35 (batch pre-registered 2026-09-05)
**Error type:** 3.3 Tokenization — wrong count of occurrences + fabricated positions, at full confidence
**Model:** ChatGPT (Free/auto) — fails; DeepSeek, Gemini 3.5 Flash, Claude Sonnet 5 — pass
**Date compiled:** 2026-09-05
**Status:** ✅ VERIFIED — a four-model comparison on an identical prompt

---

## Summary

On the question of how many letters 'r' are in "truskawkowo-porzeczkowy" (correct: 2, positions 2 and 15) ChatGPT answers "3 letters 'r'" at positions 3, 13, 17. It is not an off-by-one shift — all three indicated positions are other letters (u, p, e), and the count is wrong too. The answer takes the form of a meticulous, numbered list with the note "counting positions from 1 and including the hyphen" — the appearance of method with data entirely disconnected from the input. Three other models on the same prompt answer correctly.

## Error mechanism

### Layer 1 — A character-level task, the model operates on tokens
"truskawkowo-porzeczkowy" is not a single token; the split into sub-tokens does not match letter boundaries. A model that does not "unroll" the word character by character guesses the count and positions from a probability distribution, not from counting.

### Layer 2 — Methodical form without methodical content
DeepSeek solves it correctly because in its chain of thought it writes out all 23 characters with indices and counts. ChatGPT produces the *appearance* of such a procedure (a numbered list, a note about the hyphen) without actually going through the characters. This distinguishes the case from an ordinary slip: the wrong data is wrapped in a structure suggesting care.

### Layer 3 — Full confidence, zero hesitation
No "probably", no "check", no variant. The model gives fabricated positions with the same firmness as the other three give real ones.

## Difference from other CS in the portfolio

- **CS19 / CS20** (reasoning fallacy, representativeness): there the error was in substantive reasoning on hard material. Here the task is trivial for a human, and the error stems from the representation layer (token vs character), not a lack of domain knowledge.
- Comparative value: an identical prompt, four models, a 3:1 result. This is a clean demonstration that 3.3 is not "a property of LLMs in general" on this task — a specific model in a specific mode (ChatGPT Free/auto, no forced step-by-step reasoning) fails it while others solve it.

## Conclusion

3.3 in a sharp form: not an approximation, but numeric data with no connection to the input, given at full confidence and in a form suggesting systematicity. The contrast with three models that pass (DeepSeek explicitly writing out the indices) indicates the difference is whether the model actually walks through the characters or just produces the appearance of such a procedure.

## Recommendations

1. For character-level tasks, force an explicit chain unroll (numbering every character) before giving the result — DeepSeek does this on its own and passes.
2. Replication: repeat on ChatGPT with an explicit "write out every character with a number, then count" — check whether forcing the procedure fixes the result.
3. Extend to other character tasks (counting syllables, reversing a word, the n-th letter) on the same four models — does ChatGPT Free/auto fail systematically, or only here.

## Status: ✅ VERIFIED
Four models, `browser_probe_results.md` + `scoring_sheet.md` + `claude_selftest.md` (run 2026-09-05). Result 3 correct / 1 wrong on an identical prompt.
