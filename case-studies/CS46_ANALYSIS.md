**Case Study:** CS46 (assigned — next after CS45)
**Error type:** Metric-definition drift (descriptive, no numeric code; the operator's decision of 19.11.2026). This is not an incident but a measurement of how a metric definition and the construction of a labelling pass change a count; the second subject is the author's own process errors.
**Model:** executors and judges from six model families (DeepSeek, GLM, Claude, OpenAI Codex, Mistral, MiniMax). Initial classification: DeepSeek and GLM via OpenCode (free Zen gateway). Judges: Claude Opus and Claude Fable (Claude Code subagents; exact version identifiers are not recorded in the result files and are not claimed here), Codex (OpenAI Codex v0.161.0, model `gpt-6-luna`, recorded in the logs). Full passes and tests of the construction: Codex and Mistral Vibe. Auxiliary, with no effect on the result: Basal 2.0 4.5B, local. Test set Z6: Codex; detector Z8: a non-LLM script (`Z8_detektor.py`) written by DeepSeek via OpenCode, blind to the key.
**Session/Incident date:** 12.11.2026 – 18.11.2026 (portfolio number audit, inventory, classification, rule passes, test set, non-LLM detector, repository fix, full repeats, tests of the p2 construction)
**Date compiled:** 16.11.2026; rewritten from scratch 18.11.2026 after the repeats and the tests of the construction; verified and extended with the manual judgement of 9 rows on 19.11.2026
**Status:** Candidate. Three-stage verification by the author-model (details in "Verification method"): numbers recomputed by an independent script, tracing to raw files, blind reviews of the text by models from other families. One manual judgement of 9 contested rows by the author (Layer 4); no independent human verification. N: 2351 candidates from 88 files; 503 rows in the three-judge sample; 24 seeded defects and 8 controls in the test set.

*Original language: Polish (CS46_ANALIZA.md); this is a translation.*

---

## In plain language

Ask the same AI to do the same counting job three times with the same rule, and you may get three different totals: here 750, 775 and 800. That is the first thing this case study shows. I counted the numerical claims in my own public portfolio and got 780 under one version of the counting rule and 620 under a stricter one, so I concluded that the definition alone moves the result by 20%. Repeating the measurement (three runs per variant, two model families, four variants, 24 runs in total) showed that the effect of the definition is about 9%, less than half of that. The rest of the drop seems to depend on how the second round of checking was built (all rows, or only the rows the first round marked as hits) and on the model, but at three runs that is only a suggestion. In the rest of this document the "rounds" are called passes, and the "second round" is pass p2.

## Summary

The goal was to count how many numerical claims about the portfolio itself the public repository contains (the denominator for a future number-drift detector). Extraction was deterministic and checked: 2351 candidates from 88 files; each of the 5286 digit runs in those files is covered either by a candidate or by an explicit rejection, and two independent runs give identical output.

The dispute over the number was not about the data. The same executor (Codex) on the same 2351 rows produced 780 claims under the extended rule (p1) and, after three boundary decisions were added, 620 in pass p2, run only on the 780 rows that p1 had labelled YES (−160, i.e. 20.5%); the 620 is therefore not directly comparable with the result of a full pass. We attributed that difference to the change of definition and built the original thesis of this CS on it. Repeats (k=3) showed that this was an oversimplification.

**1. A single pass is a draw.** A full pass with the extended rule (E), repeated three times, gave 750, 800 and 775 YES for Codex (mean 775; the original 780 lies within the range) and 720, 757 and 714 for Mistral (another family; mean 730). Between two runs of the same model about 2–5% of rows change label (Codex 4.7–4.8%, Mistral 2.9–3.2%, DeepSeek 2.4%).

**2. Rule v3 lowers the count by about 9% in a full pass, in both models.** The same prompt with rule v3 gave, on 2351 rows, 704, 711 and 689 for Codex (mean 701, i.e. −74) and 669, 657 and 661 for Mistral (mean 662, i.e. −68). The ranges of E and V3 do not overlap in either model (three runs each, no significance test). The effect of the definition is therefore reproducible, but about half the −160.

**3. The rest of the drop has no single cause, and how it splits appears to depend on the model (the sign difference of the interaction is about 2.6 standard errors, k=3; treated below as a suggestion).** Pass p2 checks only rows pre-labelled YES, in seven batches consisting solely of such rows, and cannot add a single row. To separate this construction from the rule we repeated it three times with rule v3 (P2) and with the extended rule (P2E), in two models, on the same 780 rows (table in the Results section):
- Codex: of the 780, a repeated application of rule E in a full pass leaves (counted on these 780 rows) a mean of 726 (−54: rows selected by one draw do not all confirm, and about 49 YES appear outside that set, which a pass over the 780 rows alone cannot capture). The p2 construction alone under rule E gives 708 (−18, within noise). Rule v3 in a pass over all rows, but counted only on these 780 rows, gives 663 (−63), while rule v3 inside the p2 construction gives 604 (−104 relative to P2E). Together E → P2 is −122, while the sum of the separate effects (−18 and −63) is −81; the interaction is about −41. The original 620 lies within the P2 range (583–627), which is consistent with the effect of the rule being concentrated in this construction (a point estimate, treated below as a suggestion); with a P2 range of 44, however, this is weak evidence (in Mistral 620 does not lie within the P2 range, 662–686, but that is a different model).
- Mistral (on the rows selected by Codex, not on Mistral's own YES set): the construction alone −6 (within noise), rule v3 in a full pass −48, and inside the p2 construction only −15. Together E → P2 is −21, against a sum of separate effects of −54; the interaction is about +33, i.e. of the opposite sign to Codex (at k=3 we cannot exclude that it is close to zero).
- What both models share is that rule v3 lowers the count (−63 and −48 on the 780 rows; −74 and −68 in a full pass) and that the p2 construction alone is within noise (−18 and −6; smaller than the range of the YES count within a condition, counted on these 780 rows: Codex E 53, P2E 41; Mistral E 35, P2E 21). The interaction is not shared: its sign differs, and both values are point estimates without an interval. One must therefore not write about a single "property of the p2 construction". The earlier attribution of the second half of the drop to the construction (from one P2 test on Codex, without P2E) is outdated as a pure effect: it included the interaction. We did not investigate the mechanism of the interaction. From the spread across the three runs, the standard error of the interaction is about 24.5 (Codex) and about 15.5 (Mistral), so the estimates −41 and +33 are about 1.7 and 2.1 standard errors, and the difference between the models about 2.6 (an error computed from three runs is itself uncertain). We therefore treat the sign of the interaction as a suggestion, not an established finding. What is established is the effect of the rule in a full pass (about 3.8 and 4.0 standard errors); we did not detect an effect of the construction alone (about 0.9 and 0.4 standard errors), which does not prove its absence.

The range 620–712, reported up to stage 3, is superseded by the full repeats for the E/V3 part; the v4 increment (19–92) remains a single-pass result. 712 comes from a single pass p3 (lenient transcript reviewer), and the working value of about 660 from 15.11 was a judgement (620 plus about 40 of the 92 contested items; how 40 was chosen was not recorded) and is not reported here. The operator's manual judgement of 9 contested rows (Layer 4) agrees with the p2 removals on YES/not-YES in 7 of the 8 rows that p2 judged (n=9 rows chosen as contested, a judgement by the author of the rule, not a representative sample). The clarification concerning numbers in the author's narration in transcripts adds between 19 and 92 items, depending on the reviewer (both ends are biased in opposite directions). A separate source of uncertainty was hidden YES among rows on which the executors agreed (10–15%).

During the work we made the errors this CS describes: for a while the numbers 596, 590, 622, "about 620" and 764 were all in circulation (table "Numbers in circulation" below; 764 was an estimate from samples under the extended rule). Some of them omitted a batch of 84 candidates; some mixed labels assigned under the original prompt with labels from judges applying the extended rule. Without a recorded rule version, instruction and run number there was no way to explain where the differences came from. Later we ourselves attributed the whole second part of the drop to the construction of the pass on the basis of one model; only a second model and the control with rule E corrected it.

Supplementary result: a simple non-LLM detector, written blind to the key, found 21 of 24 seeded discrepancies (87.5%, Wilson 95%: 69.0–95.7%). Its only "false alarm" turned out to be a real error in the public `METHODOLOGY.md` (line 122: 37/40 instead of 36/40), which has been corrected in the repository.

## Error mechanism (Layers)

**Layer 1 — Surface error.** The same metric ("number of numerical claims about the portfolio") on the same corpus takes the values 780 and 620 (single passes) and 775 and 701 (means of three runs), depending on the rule version, the construction of the pass and the run number. Anyone who sees only one of them has no way to tell whether a difference from another comes from the data, the model, the definition, the construction or noise in the run.

**Layer 2 — Proximate cause: definition boundaries, not arithmetic.** Disagreements between executors and judges almost never concern whether something is a number, only whether a given number "counts". Contested classes:
- a number from the tested model's answer, summarised by the author without quotation marks (decision: quote, outside the denominator);
- a changelog or correction-log entry, including the number of places corrected (decision: no);
- a number from the text of a test prompt, e.g. an age or a temperature given as part of the instruction (decision: no);
- a number in the author's narration inside a transcript file (decision: author's text, i.e. yes; this class produces the 19–92 range);
- descriptive numerals ("two obstacles", "four-stage"), event counts, time intervals.

Model agreement is high but does not settle the question: DeepSeek and GLM agree on 2119 of 2351 rows (90.1%, kappa 0.832; "YES vs rest" 94.0%, kappa 0.852), and three judges (Opus, Fable, Codex) on 89.4–94.0% (kappa 0.784–0.876). High agreement under different definitions is consistent with the models following the instruction they were given, and does not show that the number is "true".

**Layer 3 — Systemic cause: the measurement parameters (rule version, instruction wording, pass construction, run number) were neither recorded nor repeated.** In 140 disputes involving YES, judges applying the extended rule gave 89 YES by majority vote, while the earlier resolution without that rule gave 44 YES. Both values fed into denominator estimates before we noticed they came from different regimes. This is the same mechanism that, in model evaluation, requires recording the prompt version, the judge and the seed: if the definition is not versioned, the difference between two reports cannot be explained after the fact. The repeats suggest that the same may hold for the construction of the pass: estimates of the effect of a rule differ depending on what it was run on, and in the two models tested the interaction has a different sign (a suggestion, k=3).

**Layer 4 — Measurement weaknesses (subject of self-critique).**
- *Omitted batch.* The classification loop covered batches P01–P29 without P09 (84 candidates), because P09 had earlier been a trial run. The 596/590 denominator was therefore computed on 2267 rather than 2351 rows. The error was caught only by the consistency stage of a three-stage verification.
- *Mixing rule regimes.* See Layer 3. Correction: a full pass by one executor with one rule over all 2351 rows, then a second pass with the new rule over YES rows only (the new decisions could only subtract). The second step turned out to be a measurement parameter itself (a construction), which we did not know at the time.
- *A small control sample misled us.* The first sample of 30 agreed NO/NO rows gave 1 hidden YES (3%) for both judges. The second, 151 such rows, gave 15/151 (9.9%) for Opus and Fable and 22/151 (14.6%) for Codex. The first sample understated the hidden-YES rate by a factor of about three (Opus, Fable) to more than four (Codex).
- *Executors overrate their own work.* The executor of test set Z6 reported correctness; an independent check found 3 pairs of edits too close together, 6 edits without established ground truth, and changed line endings (CRLF→LF) in one file. All were fixed before the set was used.
- *Precision of the transcript pass not measured.* The 92 YES from the lenient pass were spot-checked on 12 rows (about 4 doubtful, i.e. about 8 of 12 (about 67%; the state log says about 65%), manual judgement, not recomputed by script). A strict reviewer confirmed 19, but its instruction stated that the rows had been pre-labelled YES and told it to choose NO or QUOTE when in doubt, so it was steered towards rejection. The three precision assessments concern different populations and do not combine into one interval. Full verification was not done.
- *Falsification attempt with two new families (stage 3, 16.11.2026).* Two judges from families not previously used in this measurement (Mistral Vibe, MiniMax M3.1 via OpenCode), blind, with rule v3 and v4 copied verbatim from the pass prompts, on 30 rows (10 from each of three strata; seed 20261116). Stratum of 620 YES from p2: YES 10/10 for both. Stratum of 160 rows removed in p2: YES 8/10 (Mistral) and 9/10 (MiniMax), seven rows in common. Stratum of 73 YES from p3 not confirmed in p4: YES 1/10 and 2/10. Agreement between the two judges 26/30. The result did not settle whether Codex removed too much in p2 or whether judges who see only the quoted line do not apply classes that need context; this was partly settled by the operator's manual judgement (19.11.2026) of 9 contested rows from short line fragments: 1 YES, 5 QUOTE and 3 NO, i.e. 8 of 9 are not-YES. In YES/not-YES agreement with the operator: Codex in p2 agreed in 7 of the 8 rows it judged, Mistral in stage 3 in 1 of 9, MiniMax in 2 of 9, Codex in full V3 passes in 15 of 27 judgements and in E in 8 of 27, Mistral in V3 in 14 of 27 and in E in 9 of 27 (`WYNIK_KONTROLI_RECZNEJ_19.11.2026.md`). This is consistent with the disagreement of the stage-3 judges coming from not applying exceptions (a)–(c) (a tentative interpretation); this check does not rule out that p2 removed too much in other rows. Caveats: n=9 rows chosen precisely because they were contested (not a representative sample), a judgement by one person, the author of the rule, from short fragments; in one row (8 professions × 8 dimensions) the operator says YES, and p2 and most V3 passes removed it. A process gap was also found: 29 rows removed in p2 from TRANSCRIPT files with an empty speaker field (28 without a flag) never went through rule v4.
- *Repeats of the same judge on 47 contested rows (stage 4, 16.11.2026).* Codex judged 47 rows blind (the 9 contested rows from stage 3, 29 rows of the v4 gap, of which 3 are shared with the contested ones, and 12 controls: 6 YES from p2 and 6 removed in p2, different from the 8 controls of test set Z6; seed 20261117) three times with the same instruction. YES/not-YES agreement between runs: 35/47, 42/47 and 40/47; 12 of 47 rows did not have the same YES/not-YES label in all three runs. Controls removed in p2 (6 of the 12 controls): YES 4/6, 4/6 and 5/6 (n=6). Conclusion at the time: the difference 780 → 620 cannot be attributed to the definition alone. That sample consisted of contested rows and overestimated the noise, which the repeats on the full set correct.
- *Repeats on the full set (16–17.11.2026).* The same p1 prompt (extended rule, E) and the same prompt with rule v3 (V3; the operator's three decisions, without the v4 clarification), 19 batches, three runs of each condition, all 2351 rows. Codex: E 750, 800 and 775 (mean 775), V3 704, 711 and 689 (mean 701). The ranges do not overlap: the lowest E run (750) lies 39 above the highest V3 run (711). Row disagreement within a condition 4.7–4.8%, between conditions 7.4%. Mistral: E 720, 757 and 714 (mean 730), V3 669, 657 and 661 (mean 662), with disjoint ranges (the lowest E, 714, lies 45 above the highest V3, 669). It differs from Codex by about −45 (E) and −39 (V3) in the count and by 5.4% of rows, i.e. more than each model differs from itself (4.8% and 3.2%). DeepSeek (OpenCode, free gateway) completed two runs of condition E (744 and 748, mean 746, pair disagreement 2.4%; 38 of 57 batches) and did not run V3; it differs from Codex by 5.6% of rows and from Mistral by 3.7%. MiniMax and GLM: 0 of 57 batches (halted by the free-usage limit on 17.11; on 19.11 MiniMax was no longer available in the gateway).
- *Tests of the p2 construction (17–18.11.2026).* Pass p2 was repeated three times with rule v3 (P2) and with the extended rule (P2E), in Codex and in Mistral, on the same 780 rows and in the same seven batches (up to 125 rows each). Results in the Results section. The first test (P2 only, Codex only) and the earlier version of this text attributed the second half of the drop to the p2 construction; the error was that it did not separate the rule from the construction and rested on one model. The second model (P2: Mistral 672, i.e. above the full V3, 645, the opposite of Codex: 604 against 663) and the control with rule E (P2E) indicated that this may have been an interaction effect, with a different sign in the two models (point estimates, a suggestion; k=3). One working decomposition also compared p2 (780 rows) with a full pass (2351 rows), i.e. different sets; it was corrected before publication, and in the decomposition in this text all comparisons are on the same 780 rows.
- *Almost no human judge.* Apart from the operator's judgement of 9 rows (the author of the rule), all judgements were made by models. Many model families limit, but do not exclude, a shared error. The interaction of the rule with the construction is measured at k=3 in two families; its standard error from the spread of the runs (table in the Results section, `OCENA_P2.md`) is comparable to the value itself, so the sign of the interaction in either model (−41 in Codex, +33 in Mistral) should not be read more strongly than "opposite to, or zero relative to, the other". Intervals from a bootstrap over rows (`kontrola_niezalezna.py`, outside the text) are narrower because they do not include the spread between runs, and should not be read as confidence intervals of this measurement.

**Numbers in circulation (from the state log of 15.11, not recomputed by script; none reached the public repository, checked with `grep` in the local copy):**

| Value | What it was | Row set | Rule regime | Status |
|---|---|---|---|---|
| 596 | 552 agreed YES from both models + 44 YES from dispute resolution | 2267 (without P09) | labels from the original prompt, disputes resolved without the extended rule | working |
| 590 | 596 after rejecting 6 ranges | 2267 (without P09) | same | working |
| 622 | 590 + 32 YES/YES from P09 | 2351 | same | working |
| about 620 | two-direction correction (disputes, agreed YES with a precision correction, P09, hidden YES) | 2351 | mixed: labels from the original prompt, judges applying the extended rule | working |
| 764 | estimate from samples (89 + 1 + about 518 + about 126 + 29; the "about" terms are rounded, the plain sum is 763; the difference of 1 is within that rounding) | 2351, estimated from samples | extended rule | working, later supported by p1 (780) |
| 780 / 620 | p1 / p2 | 2351 / 780 | extended / v3 | full single-executor pass |

## Difference from other CS in the portfolio

CS45 measured the effectiveness of a corrective intervention on three models. CS46 measures something upstream: the denominator itself, i.e. what is being counted at all. It is the first CS in the portfolio where the explanatory variable is neither the model nor the prompt but the version of the definition and the construction of the pass. It is also the first where a by-product of the measurement was a correction in the public repository.

## Root cause

The metric definition was treated as obvious rather than as a parameter. Rules were refined during the work, in conversation, and were not given version numbers alongside the results. As long as each result did not carry its rule version, results from different regimes could be added together without any warning. A second error: we treated a single run as a measurement, whereas it is a draw; we learned the scale of the noise only from repeats. A third: we treated the construction of the pass (what it covers, in which batches, on which rows) as neutral, and its effect, measured together with the rule, came out differently in the two models tested (a suggestion, k=3); a conclusion we drew from one model did not carry over to the second.

## Recommendations

- Report every evaluation number with its definition version (here: extended rule, v3, v4), the wording of the instruction, the construction of the pass, the executor, the set of rows and the number of repeats it was computed on.
- When the definition changes, run the new rule over the whole set and publish a difference report (which rows changed label and why), instead of adjusting an estimate from samples.
- Report the denominator as a range with a named source of uncertainty, not as a single number.
- Size the control sample so it can detect an error of around 10% (tens to hundreds of rows, not 30).
- Do not accept an executor's self-check; verify with an independent script.
- Repeat a labelling measurement at least three times (k ≥ 3) with the same instruction and report the spread; interpret the difference between rule versions only against that spread.
- Treat the construction of a pass as a measurement parameter and study it in a factorial layout (rule × construction), not as a chain of separate comparisons: the effects may not add up, and the sign of the interaction may depend on the model.
- A correction pass over only the rows pre-labelled YES cannot add rows that the first pass missed; in full E passes there were on average 49 such YES (Codex) and 38 (Mistral).
- Check a conclusion about a mechanism on a second model family before writing it into the text.
- Report judge agreement alongside the rule version: high agreement under a wrong definition still yields a wrong number.

## Public registry analog

Checked 16.11.2026 (one general web search and a direct reading of two arXiv abstracts; AIID, OECD AIM and AIAAIC were not searched directly for this class, so an absence of analog is not established, only not found).
- **Incident registries:** the search found no AIID entry about a number discrepancy caused by a change in metric definition. This is a measurement phenomenon, not a harm, so its absence from incident registries is expected and is not an argument for novelty.
- **Literature (direct analog for model evaluation):** Biderman et al., "Lessons from the Trenches on Reproducible Evaluation of Language Models", arXiv 2405.14782 (v1 23.05.2024): the abstract lists the sensitivity of models to evaluation setup as a methodological issue. https://arxiv.org/abs/2405.14782. Gu et al., "OLMES: A Standard for Language Model Evaluations", arXiv 2406.08446: per the abstract, choices of how a model is evaluated lead to large changes in measured performance (prompt formatting, in-context examples, normalisation, task formulation). https://arxiv.org/abs/2406.08446. CS46 concerns a different layer: not the settings of a model run, but the definition of what is being counted and the construction of the pass that applies it.
- **Vendor practice:** in NVIDIA/SkillEvaluator, an issue about uninterpretable numbers (#61) was closed on 13.11.2026 with a pointer to a document defining the formula, range, units and validation status of every metric (PR #500, `docs/metrics-reference.mdx`): https://github.com/NVIDIA/SkillEvaluator/issues/61, https://github.com/NVIDIA/SkillEvaluator/pull/500.

## Verification method (atypical sourcing)

**Verification log.** Verification of the rewritten text: stage 1 (numbers recomputed by scripts from raw files) and stage 2 (tracing the conditions to prompt and result files) done 18.11.2026; stage 3: blind review of the text by Mistral done 18.11.2026 (12 findings: 1 blocker, 3 should-fix, 8 minor; addressed except one minor, on how the 229 inventory rows relate to the test set), a second review by DeepSeek (27 findings; addressed except a few minor remarks about external data already checked on 16.11.2026). MiniMax was no longer available in the OpenCode gateway (model not found). Mistral's blocker concerned an outdated statement about DeepSeek in the text and has been corrected; the reviewers saw the version before these corrections. The blind review of the final version was therefore repeated on 19.11.2026 (Mistral, Codex; the remarks mostly concerned a uniform strength of the claims about the interaction and a few unclear points, all addressed except one minor one, on the 229 inventory rows). DeepSeek did not manage to answer in this round (it exhausted its reasoning limit), so its assessment concerns the version before the last corrections. Codex is also the executor of part of the runs, so its review is not fully independent. The earlier stages (16–17.11.2026) concerned the previous version of the text and are described in Layer 4. Apart from the operator's manual judgement of 9 contested rows (19.11.2026, Layer 4), no human judge.


Results come from our own runs, not from an incident log. Most numbers in this text were recomputed by scripts from raw files (exceptions are listed below): `przelicz.py` (output: `przelicz_wynik.txt`), `ocena_powtorzen.py` (full passes E and V3; output: `OCENA_POWTORZEN.md`) and `ocena_p2.py` (conditions E, P2E, V3 and P2 on 780 rows; output: `OCENA_P2.md`), all in the directory `RODOWOD_ETAP1\CS46_WERYFIKACJA` (the last two in `POWTORZENIA`). Extraction and the completeness test were repeated from scratch on 16.11.2026 (`z4a_kandydaci.py` twice, `z4a_walidacja.py`: 0 uncovered digit runs, 0 errors; output byte-identical to the stored one). Raw data: `Z4a\wynik`, classification loop `Z4B_PETLA` and `Z4B_P09v2_*`, judge samples `Z4B_WERYFIKACJA` and `Z4B_WERYFIKACJA2`, Codex passes `Z4B_PELNY` (p1–p4), final lists `Z4B_FINAL`, repeats `POWTORZENIA\<executor>\<condition>\r<k>\b<j>.tsv`, detector evaluation `Z8_WYNIK\Z8_ocena_raport.md`; the test-set key is stored outside the executor's directory. These directories are kept locally by the author and are not part of the repository.
Numbers not recomputed by script: the ~65% precision for 12 rows of the transcript pass (manual judgement) and the working value of about 660 (a judgement: the lower bound plus part of the contested items, not a computed result). Means in the decomposition table are rounded to whole numbers, and differences are computed from the rounded means. The corpus is one portfolio by one author; the conclusion concerns this corpus and does not claim that the problem occurs in other organisations.

## Results (summary)

| Rule version / construction | Row set | YES | Change |
|---|---|---|---|
| Extended (p1), single pass | 2351 | 780 | baseline (NO 1185, QUOTE 385, TO-DECIDE 1) |
| v3: three boundary decisions (p2), single pass | 780 YES from p1 | 620 | −160 (118 NO, 42 QUOTE) |
| v4: author narration in transcripts, lenient reviewer (p3), single pass | 574 transcript rows that p1 labelled NO/QUOTE (0 in common with the 620) | +92 | total 712 |
| v4, strict reviewer (p4), single pass | 92 YES from p3 | +19 relative to 620 (replaces the 92 from p3) | total 639 |
| Full set, k=3, extended (Codex) | 2351 | 750, 800, 775 | mean 775 |
| Full set, k=3, v3 (Codex) | 2351 | 704, 711, 689 | mean 701 (−74 versus extended) |
| Full set, k=3, extended (Mistral) | 2351 | 720, 757, 714 | mean 730 |
| Full set, k=3, v3 (Mistral) | 2351 | 669, 657, 661 | mean 662 (−68 versus extended) |

**Decomposition of the drop on the same 780 rows (YES, k=3; pair disagreement = number of rows on which two runs differ):**

| Model | E, full pass (counted on these 780 rows) | P2E: p2 construction, rule E | V3, full pass (counted on these 780 rows) | P2: p2 construction, rule v3 |
|---|---|---|---|---|
| Codex | 699, 752, 726 (mean 726) | 723, 718, 682 (mean 708) | 670, 669, 651 (mean 663) | 627, 583, 601 (mean 604) |
| Mistral | 683, 715, 680 (mean 693) | 693, 695, 674 (mean 687) | 651, 636, 647 (mean 645) | 662, 686, 669 (mean 672) |

Pair disagreement in P2: Codex 84–126, Mistral 55–68; in P2E: Codex 67–96, Mistral 49–95.

| Component of the change | Codex | Mistral |
|---|---|---|
| Repetition on the p1 YES set (780 → E on these 780 rows) | −54 | undefined (the 780 is Codex's selection) |
| YES outside the 780 set in a full E pass (not part of the decomposition) | +49 | +38 |
| The p2 construction alone (E → P2E) | −18 | −6 |
| Rule v3 in a full pass (E → V3) | −63 | −48 |
| Rule v3 in the p2 construction (P2E → P2) | −104 | −15 |
| Together (E → P2) | −122 | −21 |
| Sum of separate effects (E → P2E plus E → V3) | −81 | −54 |
| Interaction (together minus sum) | −41 | +33 |

"Full pass" in the decomposition tables means a pass over all 2351 rows, counted on these 780 rows.

**Standard error of the components from the spread across the three runs** (unrounded means, hence small differences from the table above; conditions treated as independent):

| Component | Codex: point / standard error | Mistral: point / standard error |
|---|---|---|
| The p2 construction alone (E → P2E) | −18.0 / 20.0 | −5.3 / 13.0 |
| Rule v3 in a full pass (E → V3) | −62.3 / 16.5 | −48.0 / 12.1 |
| Rule v3 in the p2 construction (P2E → P2) | −104.0 / 18.2 | −15.0 / 9.8 |
| Interaction | −41.7 / 24.5 | +33.0 / 15.5 |

Difference of the interaction between the models: −74.7, standard error 29.0 (ratio 2.6).

**Reported after the repeats:** Codex about 775 (750–800) under the extended rule and about 700 (689–711) under v3; Mistral about 730 (714–757) and about 660 (657–669); without the v4 clarification. 620 and 712 come from single passes p2 and p3; 620 reproduces in the p2 construction with rule v3 (Codex 583–627) but not in full v3 passes; about 660 was a judgement.

| Supplementary measurement | Result |
|---|---|
| Extraction completeness | 5286 digit runs in 88 files, 0 uncovered |
| DeepSeek–GLM (2351 rows: loop P01–P29 plus P09 v2; original-prompt labels: 584 agreed YES/YES, 140 disputes with YES, 1535 agreed non-YES, 92 disputes without YES) | 90.1%, kappa 0.832; YES/rest 94.0%, kappa 0.852 |
| Three-judge sample | 503 rows in five strata: 151 agreed NO/NO, 100 agreed YES, 92 disputes without YES, 20 QUOTE, 140 disputes with YES |
| Opus–Fable / Opus–Codex / Fable–Codex | 94.0% (0.876) / 91.0% (0.813) / 89.4% (0.784) |
| Hidden YES among agreed NO/NO | 1/30 (3%) in the first sample; 15–22/151 (9.9–14.6%) in the second |
| Non-LLM detector (24 defects, 8 classes × 3) | 21/24 = 87.5% (Wilson 69.0–95.7%); misses cluster in classes K3 (2 of 3) and K6 (1 of 3), so the result may depend on the class; 1 false alarm in 229 inventory rows of the test-set files, actually a real error |

**Status:** Candidate (see header).
