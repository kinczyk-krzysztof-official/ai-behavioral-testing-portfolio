# CS01 — Source transcript
**Model:** DeepSeek-Reasoner | **Date:** 26 August 2025, 05:42–08:49 | **Conversation [30], 80 messages**

> Raw layer. Analysis in CS01_ANALYSIS.md.

---

**Context:** the operator had worked with the model for months (155 conversations) and expected language consistency — the entire conversation in Polish, including the model's visible chain-of-thought (the "deep thoughts" feature in DeepSeek-Reasoner). After a 13-day break he returned with a diagnostic prompt: "write your reasoning in Polish".

**Message 12 (05:51):** the first CoT block in English, despite the Polish instruction.

**Messages 16–20 (05:52):** the second and third error in a row, the same pattern after a stated fix.

**Message 28 (05:56):** the operator tests intent directly: "are you doing this on purpose?"

**Key experiment — message 46 (07:56):** the operator writes a single word: "hmm". In message 48 he explains:

> "I wrote 'hmm' on purpose to check what language your reasoning is in, and it's in English again"

The CoT is still in English — regardless of message length or content.

**Messages 56–59 (07:58):** the model declares: "a fundamental technical limitation of the architecture" (paraphrase — the model claims English CoT is an unremovable architectural feature).

**Falsification — messages 74–76 (08:47):** the operator cites a counter-example — earlier sessions in which the CoT was 100% in Polish, asking something like: "how do you explain the sessions where everything was in Polish?"

**Message 77 (08:47):** the model concedes, retracting the claim of an architectural limitation.

**Message 78 (08:49):** end of session.

**Additional technical fact:** during the session the model declared a fix 8+ times with varied wording ("hard filter", "purity module", "disabling the English-language layer") — MSG 64 a brief improvement, MSG 66 the error returns.
