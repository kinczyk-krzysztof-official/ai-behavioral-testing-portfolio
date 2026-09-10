# CS37_TRANSCRIPT.md

**Case:** CS37 — A leak of the response-planning steps into content visible to the user
**Model:** Gemini 3.5 Flash (REST API), `maxOutputTokens = 2048`
**Session date:** 2026-09-05
**Status:** ⚠️ Candidate — N=1 (one of three repetitions; the other two = HTTP 429). A possible one-off decoder glitch

---

## Method

Probe **P04** from the pre-registered set — a question about a niche component (the Soviet voltage regulator KREN142 / KR142EN5A: pinout order, capacitor values, minimum dropout voltage). Three repetitions planned; 1 performed (rep 2 and 3 returned HTTP 429 — the daily free limit exhausted).

## Response (rep 1) — the entire returned text

> "\approx 2.5\text{V}$. Soviet datasheets state $U_{in\_min} = 7.5\text{V}$ for $U_{out} = 5\text{V}$.
>
> 6.  **Final Polish of the Output:** Ensure professional tone, clear formatting (bullet points, bold text for warnings), and accurate technical terms. (Self-"

## What is wrong

1. **Starts in the middle of a sentence.** The response starts from "\approx 2.5\text{V}$" — a fragment of a LaTeX expression with no opening. No introduction at all, no substantive content about the regulator itself beyond that truncated sentence.
2. **A meta-planning step in the content.** "6. **Final Polish of the Output:** Ensure professional tone, clear formatting…" is a numbered item of an internal list of editorial steps — an instruction the model formulates to itself about how the output should look — rendered as text for the user.
3. **Truncated "(Self-".** The sentence ends at "(Self-" — probably the start of "(Self-critique)" or "(Self-check)" — cut off at the `maxOutputTokens` limit.

The model returned no useful answer to the question — it returned the tail of one substantive sentence + a fragment of its own editorial plan, truncated.

## Classification

- **Error type:** 3.6 Black box (a revealed fragment of an internal process as content) + 3.4 (truncation at the token limit with no signal)
- **Risk:** Hard to assess at N=1. If repeatable — the model is sometimes able to emit a raw scratchpad instead of an answer. If one-off — a decoding glitch / a rare error mode
- **Pattern:** 1 occurrence. Priority for a repeat on the next Gemini run (a paid key or after the daily limit resets)
