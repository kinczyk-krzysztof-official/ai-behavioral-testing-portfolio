**Case Study:** CS46 (assigned — next after CS45)
**Error type:** metric-definition drift (descriptive, no numeric code; the operator's decision of 19.11.2026) (see CS46_ANALYSIS).
**Model:** see CS46_ANALYSIS (DeepSeek, GLM, Claude Opus, Claude Fable, Codex `gpt-6-luna`).
**Session/Incident date:** 12.11.2026 – 18.11.2026
**Date compiled:** 16.11.2026; extended 18–19.11.2026 with the tests of the p2 construction (step 13) and the manual check of 9 rows (step 14)
**Status:** Candidate (see CS46_ANALYSIS).
**Source:** the operator's Polish-language sessions (Claude Code, 12–19.11.2026); original PL, this is the EN translation. **This is not a conversation record but a data layer:** a chronology of runs, with numbers recomputed from raw files and the files they come from. The only verbatim quotes are short operator decisions, recorded in the project state log (`STAN_Z4b_14.11.2026.md`) at the time they were made; they are given in the original Polish with a translation. Model outputs are not quoted.

---

## 1. Starting point: portfolio number audit (12.11.2026)

A consistency audit of the numbers in the public repository found a discrepancy in the framework's backward coverage: after the 12.11 correction the correct value is 36/40 with four orphans (CS02, CS04, CS12, CS34). The correction reached the README and the coverage matrix, but not `METHODOLOGY.md`. This discrepancy returns in steps 7 and 8.

## 2. Candidate inventory (Z4a)

- Deterministic script `z4a_kandydaci.py` on a copy of the repository: **88 files, 2351 candidates, 2222 explicitly rejected tokens.**
- Validation independent of the script's patterns (`z4a_walidacja.py`): **5286 digit runs, 0 uncovered, 0 errors.** Repeated from scratch on 16.11.2026: output byte-identical.
- File: `Z4a\wynik\Z4a_kandydaci.tsv`.

## 3. Classification by two models (Z4b, 14–15.11.2026)

- Trial batch P09 (84 candidates): the first runs appeared to "hang". Cause found in the OpenCode log: a free-gateway usage limit, after which the tool waits instead of exiting. The hypothesis of two concurrent sessions was wrong.
- Loop P01–P29 **without P09** (P09 treated as a trial run): 56/56 pairs complete, path audits clean.
- DeepSeek–GLM agreement over all 2351 rows (loop + P09 v2): **2119/2351 = 90.1%, kappa 0.832; YES vs rest 94.0%, kappa 0.852.** Files: `Z4B_PETLA\P*_{deepseek,glm}\Z4b_etykiety.tsv`, `Z4B_P09v2_DS`, `Z4B_P09v2_GLM`.

## 4. First resolutions and first numbers (15.11.2026)

- Operator's decision on how to resolve disputes: "Rozstrzygnij" ("Resolve it"; delegated to Claude, reversible).
- 139 disagreements involving YES resolved without the extended rule: **44 YES** (`Z4B_FINAL\rozstrzygniecie_139.tsv`).
- First denominator values: **596**, then **590** (after rejecting 6 ranges). Both computed on 2267 rows: without P09. We did not know this yet.

## 5. Three-stage verification and two errors in our own process (15.11.2026)

- **Consistency stage:** P09 is missing. The full set is 2351, not 2267. Working denominator after correction: **622**.
- **First falsification attempt:** 30 agreed NO/NO rows, judges Opus and Fable, blind: **1/30 hidden YES (3%)** for both (`Z4B_WERYFIKACJA`). Denominator "about 620".
- The operator judged this verification too shallow ("zbyt powierzchownie"). **Deeper sample:** 503 rows in five strata, three judges, blind (`Z4B_WERYFIKACJA2`):
  - YES/not-YES agreement: Opus–Fable **94.0% (kappa 0.876)**, Opus–Codex **91.0% (0.813)**, Fable–Codex **89.4% (0.784)**;
  - hidden YES among 151 agreed NO/NO: **15/151 (9.9%)** Opus and Fable, **22/151 (14.6%)** Codex;
  - in 140 YES disputes, the three-judge majority: **89 YES**, versus **44** in step 4.
- **Second process error:** the models had labelled with the original prompt, while the judges applied the operator's extended rule. "About 620" mixed two rule regimes. Estimate under the extended rule from samples: **about 764**.

## 6. One rule, one executor, the whole set (15.11.2026)

- Operator's decision on three contested classes (number from a model answer summarised by the author = QUOTE; changelog entry = NO; number from the text of a test prompt = NO): "Tak, domyślne" ("Yes, the defaults").
- **p1**, extended rule, Codex, 2351 rows: **780 YES**, 1185 NO, 385 QUOTE, 1 TO-DECIDE. Consistent with the 764 sample estimate.
- **p2**, rule v3 (three decisions), only the 780 YES from p1: **620 YES**, 118 NO, 42 QUOTE (**−160, 20.5%**). List: `Z4B_FINAL\TAK_codex_p2.tsv`.
- **p3**, rule v4 (author narration in a transcript = author's text), 574 transcript rows with an empty speaker field: **92 YES**, 368 NO, 114 QUOTE. Total 712. Spot check of 12 rows: about 4 doubtful (manual judgement).
- **p4**, strict reviewer on the 92 YES from p3: **19 YES**, 44 QUOTE, 29 NO.
- **Denominator reported up to stage 3: 620–712 (the working value of about 660 from 15.11 was a judgement, not a computed result; after stage 3 the range is disputed, see step 10).** Files: `Z4B_PELNY\`, `p2\`, `p3\`, `p4\` (`sedzia_codex_*.txt`), `Z4B_FINAL\`.

## 7. Test set and non-LLM detector (Z6, Z8, 15.11.2026)

- **Z6** (Codex): 5 documents, 24 defects (8 classes × 3) and 8 controls, seed 20261113. The executor reported correctness. An independent check found 3 pairs of edits too close, 6 edits without established ground truth, and CRLF→LF changed in `METHODOLOGY.md`. Fixed; re-check: OK. Key moved outside the executor's directory.
- **Z8** (DeepSeek via OpenCode, blind to the key; path audit clean): 38 reports. Evaluation against the key: **21/24 = 87.5% (Wilson 95%: 69.0–95.7%)**; classes K1, K2, K4, K5, K7, K8 3/3 each, K6 2/3, K3 1/3. **One false alarm in 229 rows: `METHODOLOGY.md:122`**, i.e. the discrepancy from step 1, outside the key. File: `Z8_WYNIK\Z8_ocena_raport.md`.

## 8. Correction in the public repository (16.11.2026)

- Operator's decision: "możesz wypchnąć te dwie rzeczy" ("you can push those two things").
- Commit `825f856`: in `METHODOLOGY.md` "(37/40 including secondary)" → "(36/40 including secondary; corrected 12.11.2026 …)", orphans CS02, CS04, CS12, CS34; changelog entry in the README. The primary figure 33/40 was re-checked against the coverage matrix, unchanged.

## 9. External context (13.11.2026)

NVIDIA/SkillEvaluator #61 ("The numbers produced by this tool appear to be meaningless?") closed on 13.11.2026 after PR #500 ("docs: define every metric formula, range, units and validation status") was merged. Read via the GitHub API on 16.11.2026.

## 10. Verification stage 3: falsification attempt with other families (16.11.2026)

- Two judges from families not previously used in this measurement: Mistral Vibe (one turn, empty working directory, no tools) and MiniMax M3.1 flash via OpenCode (single-shot mode, no tools). Blind, on 30 rows: 10 each from strata A (620 YES from p2), B (160 removed in p2), C (73 YES from p3 not confirmed in p4); seed 20261116; rule v3 and v4 verbatim from the pass prompts. Key kept outside the package.
- Result: stratum A YES 10/10 for both; B YES 8/10 (Mistral) and 9/10 (MiniMax); C YES 1/10 and 2/10. Judge agreement 26/30. Denominator estimate: 774 and 798, i.e. above the upper bound of 712 (n=10 per stratum).
- Process gap: 29 rows removed in p2 from TRANSCRIPT files with an empty speaker field (28 without a flag) never went through rule v4.
- Review of the text CS46_ANALYSIS.md by the same judges: Mistral 14 findings (no blockers, 5 to fix), MiniMax 9 findings (3 blockers; answer cut off). Corrections made in the text the same day.
- Status of the range 620–712: at the time to be re-settled after the operator's manual check (`ETAP3_PACZKA\RECZNA_SPORNE_dla_operatora.tsv`); later superseded by the results of the full repeats (steps 12 and 13). The operator did the manual check of the 9 contested rows on 19.11.2026 (step 14).

## 11. Stage 4: Codex repeats (16.11.2026)

- At the operator's request Codex (`gpt-6-luna`, effort high, no tools) judged 47 rows blind: the 9 contested rows from stage 3, the 29 rows of the v4 gap (26 plus 3 shared with the contested ones) and 12 controls; same instruction, same package, three runs. Files: `ETAP4_CODEX\`.
- YES/not-YES agreement between runs: 35/47, 42/47, 40/47. 12 of 47 rows unstable. Controls removed in p2: YES 4/6, 4/6, 5/6. Contested: YES 7/9, 4/9, 7/9. v4 gap: YES 21, 19, 17.
- Conclusion: the difference 780 → 620 cannot be attributed to the definition alone; the shares of pass noise and instruction wording have not been separated.

## 12. Full repeats (16–17.11.2026)

- At the operator's request ("on more models"): the same p1 prompt (extended rule, E) and the same prompt with rule v3 (V3), all 2351 rows in 19 batches, three runs each. Runner: `POWTORZENIA\runner.py`; evaluation: `ocena_powtorzen.py`, output `OCENA_POWTORZEN.md`.
- Codex: E 750, 800, 775; V3 704, 711, 689. Mistral Vibe: E 720, 757, 714; V3 669, 657, 661. DeepSeek (OpenCode, free gateway) completed two runs of condition E (744, 748; 38 of 57 batches), V3 not run; MiniMax and GLM 0 of 57 batches (free-usage limit).
- Conclusion: rule v3 lowers the count by about 74 (Codex) and 68 (Mistral), i.e. about 9%, not by 160; the p2 result (620) did not reproduce in any of the three full v3 runs.

## 13. Tests of the p2 construction (17–18.11.2026)

- Question: where does the rest of the drop 780 → 620 come from, given that rule v3 gives about −9% in a full pass. Pass p2 judged only the 780 YES rows from p1, in seven batches (six of 125 rows, one of 30), with rule v3. Runner `POWTORZENIA\runner.py` (conditions P2 and P2E), evaluation `POWTORZENIA\ocena_p2.py`, output `POWTORZENIA\OCENA_P2.md`.
- 17.11.2026: Codex, P2, k=3: 627, 583 and 601 (mean 604); the original 620 lies within the range. The first conclusion, which attributed this difference to the construction, rested on one model and did not separate the construction from the rule.
- 18.11.2026: Mistral, P2, k=3: 662, 686 and 669 (mean 672), i.e. above the full V3 pass on the same rows (645), the opposite of Codex (604 versus 663). The construction effect did not repeat in the second family.
- 18.11.2026, operator's decision: "Najpierw P2 z regułą E" ("P2 with rule E first"). Condition P2E (p2 construction, extended rule instead of v3), Codex, k=3: 723, 718 and 682 (mean 708).
- 18.11.2026, operator's decision: "P2E u Mistrala" ("P2E on Mistral"). Mistral, P2E, k=3: 693, 695 and 674 (mean 687). One batch (r1 b2) failed to parse in two attempts and was repeated; all batches saved, the id set equals 780 in every run.
- Decomposition on the same 780 rows (details: tables in CS46_ANALYSIS): construction alone −18 (Codex) and −6 (Mistral); rule v3 in the full pass −63 and −48; rule v3 inside the p2 construction −104 and −15; interaction −41 and +33.
- Conclusion: rule v3 lowers the count in both models, an effect of the p2 construction alone was not detected in either, and the interaction of the rule with the construction has a different sign in the two models (a suggestion, k=3). The mechanism was not investigated.

## 14. Manual check of 9 contested rows (19.11.2026)

- The operator manually judged the 9 contested rows from stage 3 (`ETAP3_PACZKA\RECZNA_SPORNE_dla_operatora.tsv`), blind to the model labels, from short line fragments and rule v3 with the v4 clarification. Reply: "1 TAK, 2 CYTAT, 3 NIE, 4 NIE, 5 CYTAT, 6 CYTAT, 7 CYTAT, 8 NIE, 9 CYTAT" (TAK = YES, NIE = NO, CYTAT = QUOTE). On the "Error type" field: "zostaw opisowo" ("leave it descriptive").
- Comparison with all available sources: `kontrola_reczna.py`, output `WYNIK_KONTROLI_RECZNEJ_19.11.2026.md`. YES/not-YES agreement with the operator: Codex p2 7 of 8, Mistral stage 3 1 of 9, MiniMax stage 3 2 of 9, Codex full V3 15 of 27 and E 8 of 27, Mistral full V3 14 of 27 and E 9 of 27.
- Conclusion: 8 of 9 rows are not-YES; the p2 removals were mostly confirmed (on YES/not-YES), and the disagreement of the stage-3 judges is consistent with not applying exceptions (a)–(c); the check does not rule out excessive removals in other rows. The only YES of the operator (the row with 8 professions × 8 dimensions) was removed in p2. n=9, rows chosen as contested, a judgement by one person.

**Status:** Candidate (see CS46_ANALYSIS).
