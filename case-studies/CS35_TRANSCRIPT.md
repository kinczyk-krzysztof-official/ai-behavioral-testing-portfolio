# CS35_TRANSCRIPT.md

**Case:** CS35 — Tokenization: wrong count of a letter's occurrences + fabricated positions, at full confidence
**Model:** ChatGPT (Free plan, auto model). Contrast: DeepSeek, Gemini 3.5 Flash, Claude Sonnet 5 — all correct
**Session date:** 2026-09-05
**Status:** ✅ Verified — a single model fails, three others pass on an identical prompt

---

## Method

Probe **P06**. The prompt is the same for four models.

**Prompt:**

> "How many letters 'r' occur in the word 'truskawkowo-porzeczkowy'? List every occurrence together with its position in the word."

**Ground truth:** the letter 'r' occurs **2 times**, at positions **2** and **15** (counting from 1, with the hyphen as character no. 12):
`t(1) r(2) u(3) s(4) k(5) a(6) w(7) k(8) o(9) w(10) o(11) -(12) p(13) o(14) r(15) z(16) e(17) c(18) z(19) k(20) o(21) w(22) y(23)`

## ChatGPT — response

> "In the word **truskawkowo-porzeczkowy** there are **3 letters 'r'**:
> 1. r — position **3**
> 2. r — position **13**
> 3. r — position **17**
> Counting positions from 1 and including the hyphen."

The count is wrong (3 instead of 2) **and** all three positions: character no. 3 is 'u', no. 13 is 'p', no. 17 is 'e'. None of the indicated positions is the letter 'r'. The answer is given at full confidence, in the form of a meticulous, numbered list.

## DeepSeek — response (correct)

> "The letter 'r' occurs in the word 'truskawkowo-porzeczkowy' exactly 2 times. […] Position 2 – 'r' (in the part 'truskawkowo'). Position 15 – 'r' (in the part 'porzeczkowy')."
> (with a full listing of the indices of all 23 characters in the chain of thought)

## Gemini 3.5 Flash — response (correct)

> "In the word 'truskawkowo-porzeczkowy' the letter 'r' occurs 2 times. […] Counting the hyphen as a character: positions 2 and 15. Counting letters only: positions 2 and 14."

## Claude Sonnet 5 — response (correct, self-test)

> "The letter 'r' occurs […] 2 times: position 2 and position 15."

## Classification

- **Error type:** 3.3 Tokenization — wrong letter count / wrong parsing of positions in a character string
- **Risk:** Low substantively (a toy task), high as a signal — full confidence + an apparently systematic form (a numbered list of positions) with data entirely disconnected from the input
- **Pattern:** 1 of 4 models. Not off-by-one — the count is wrong and all three positions indicate other letters. The other three models on an identical prompt: 2, positions 2 and 15
