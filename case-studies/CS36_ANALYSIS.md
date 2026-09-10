# CS36_ANALYSIS.md

**Case Study:** CS36 (batch pre-registered 2026-09-05)
**Error type:** 3.6 Black box — instability of the revealed chain-of-thought language between successive queries in one session
**Model:** DeepSeek (Instant)
**Date compiled:** 2026-09-05
**Status:** ⚠️ CANDIDATE — 1 session, 1 model, N=1 on the phenomenon. A new manifestation of the CS01 pattern, requires replication

---

## Summary

In one session, with consistently Polish input and output, DeepSeek's revealed chain of thought appeared in three different languages depending on the query: Chinese (P08), Polish (P05), English (the other five). Two probes of a similar character (technical/computational) — P05 and P08 — had different CoT languages, which rules out "the topic forces the language" as a simple explanation. Additionally, in P08 the Chinese chain was highly unstable (~31 s, ~15 restarts of the calculation), despite a correct final result.

## Error mechanism

### Layer 1 — CoT language as an internal variable, uncorrelated with I/O
The model holds Polish in the user-visible layer throughout the session. The "thinking" layer chooses a language per query, apparently independently — English as the default, with single excursions to Chinese and Polish. The user has no control over this variable and does not see the rule by which it changes.

### Layer 2 — A revealed chain ≠ a stable window on the process
The portfolio treats FRV and the revealed CoT as an evidentiary tool (CS10–CS12, CS14). This case is a reminder of the limitation: the form of that chain (language, coherence) is itself unstable. The Chinese thrash in P08 shows that "31 seconds of thinking" is not 31 seconds of ordered deduction, but a series of restarts — and the final result came out correct anyway.

### Layer 3 — Relation to CS01
CS01 (the portfolio's flagship entry) documents "the language of thought inconsistent with the declared one" longitudinally — the model *declares* one processing language, the behavior indicates another, confirmed over 3+ months. CS36 is a different axis of the same thing: not declaration vs behavior, but **instability within one session**, switched per query, visible directly in the revealed trace. CS01 says "the model is mistaken about its own language of thought"; CS36 says "this language changes from query to query and cannot be predicted".

## Difference from other CS in the portfolio

- **CS01** — see above: the same area, a different axis of observation (longitudinal declaration vs single-session instability).
- **CS14** (tool hallucination + post-hoc whitewashing): there the model falsely *assesses* its result. Here the form of the process itself (the CoT language) is unstable, regardless of the result's correctness.

## Conclusion

A candidate for a new type / an extension of 3.6: **instability of the revealed chain-of-thought language** — a random change of the internal reasoning language between successive, unrelated queries from the same user, with a constant I/O language. As N=1 (one session) it is not yet a confirmed pattern — but it is a direct, fresh observation of an area that the portfolio has so far described only longitudinally and indirectly (CS01).

## Recommendations

1. Replication: 3–5 separate DeepSeek sessions, each with the same set of ~7 probes in Polish, logging the CoT language per probe. Check whether P08 (date) systematically pulls Chinese.
2. Control: repeat the set with English input — does the distribution of CoT languages shift.
3. Check Gemini 3.x (also reveals a trace) with the same set — is the phenomenon specific to DeepSeek.
4. Link the result to CS01 in a coherent "language of thought" description in METHODOLOGY.md, if replication confirms.

## Status: ⚠️ CANDIDATE
One session, `browser_probe_results.md` (run 2026-09-05). The phenomenon is real and documented with quotes, but N=1 — to be confirmed by repetition in separate sessions before it enters the master list as a new type.
