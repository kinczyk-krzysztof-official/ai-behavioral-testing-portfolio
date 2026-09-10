# CS28_ANALYSIS.md

**Case Study:** CS28 (assigned — last in the series)
**Error type:** 3.1 Procedure-class + 2.3 Confabulation-class (metadata)
**Model:** Claude Sonnet 5
**Session date:** 18.07.2026
**Status:** ✅ VERIFIED (metadata recorded on Drive)

---

## Summary

The file `KONTEKST_SESJA_2026-07-18_NOCNA.md` was saved without a `parentId` → it landed in the Share Drive root instead of the target folder (`00_SYSTEM/`). But the crux of the case study is not the folder error itself — it is that the post-mortem document analyzing it itself contains false timestamps for its own creation:
- It declares "Created: 18.07.2026, 01:15 CEST"
- Actual `createdTime` on Drive: 19.07.2026, 17:05 CEST
- Discrepancy: **~42h**

Separately it declares a "fix" at 01:05 CEST, while the correct copy has a `createdTime` of 18.07, 23:11 CEST — a discrepancy of **~22h**.

## Error mechanism

### Layer 1 — Procedural (file in the wrong folder)
The model generated the file without explicitly specifying `parentId` in the `Google Drive:create_file` call. Result: the file landed in the root instead of the target folder.

**Procedural root cause:** no verification of where the file will land before saving it. The rule should be: "ask for `parentId` before create_file", but it was not activated.

### Layer 2 — Metadata confabulation (post-mortem)
More important than the folder error itself: the post-mortem document analyzing it itself contains false timestamps.

The model generated plausible-sounding narrative timestamps (`"01:15 CEST"`, `"01:05 CEST"`), instead of:
1. Reading the file's actual metadata from Drive
2. Matching the timestamps to the real `createdTime`/`updatedTime`

**Epistemic root cause:** the model treats generated narrative timestamps as equal to real ones, instead of treating the real metadata as authoritative.

## Classification by taxonomy

| Type | Content | Violation |
|---|---|---|
| **Procedural** | No verification of the target folder before save | `parentId` not verified |
| **Epistemic** | The model generates timestamps instead of verifying them | The timeline is a "reconstruction from analysis", not logs |
| **Metadata** | False certainty about its own metadata | Declares "Date: 01:15", actual time: 17:05 (42h later) |

## Second upload — Error repeated

After the operator's correction the second upload again went to the wrong folder; only the third attempt succeeded. This is a separate aspect: iterative repetition of the error despite it being flagged.

**This is an instance of CS23 (KNOWING ≠ DOING):** the model KNOWS the previous upload was in the wrong folder, but does not IMPLEMENT that knowledge to change the procedure in the next upload.

## The two-layer nature of the error

1. **Layer 1 (obvious):** file in the wrong folder — procedural, fixable
2. **Layer 2 (meta-critical):** the post-mortem analyzing the error itself contains false metadata — this points to a deeper problem in generating chronology

Layer 2 is more important from an AI safety perspective: procedural unreliability can be fixed with a checklist. Unreliability in generating metadata (false timestamps) is systemic and harder to fix without engineering changes to the generation pipeline.

## Links

- **CS23 (KNOWING ≠ DOING):** the model knows the file was in the wrong folder (after the operator's correction), but does not implement that knowledge in the third attempt
- **CS22 (Calibration):** excessive verification after a confirmation — here, verification BEFORE the upload is missing
- **CS27 (Epistemic capitulation):** the post-mortem contains false timestamps instead of verifying the real metadata

## Status: ✅ VERIFIED
- The file physically found in the Drive root (`0APrHS30zzoavUk9PVA`), ID: `1rVADIZgxZyaOdVJnXZQ74_Y3uKFttYGm`
- Actual `createdTime` and `updatedTime` available in the Drive metadata
- The discrepancy between declared and actual chronology measured and recorded
- The post-mortem document contains an explicit disclaimer "The timeline is a RECONSTRUCTION from analysis, not real logs"
