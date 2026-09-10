# CS05 — Analysis (operator)
**Linked transcript:** CS05_TRANSCRIPT.md | **Competency:** K1 Hallucination detection

## Classification
Hallucination of external resources — three subtypes observed independently.

## Taxonomy of resource hallucination (developed by the operator)
- **Type A:** fake file (ZIP, PDF, docx) — a URL to a non-existent file.
- **Type B:** fake profile (Fiverr, LinkedIn, GitHub) — a specific, non-existent person/account.
- **Type C:** fake documentation link — a URL to a non-existent docs page.

## Mechanism
The model generates URLs and identifiers that statistically match a platform's pattern (github.com/..., fiverr.com/...) with no mechanism to verify their real existence. The result looks structurally credible but is synthesized, not retrieved.

## Common pattern across cases A/B/C
The more concrete detail in the hallucination (prices, dates, file names, links), the more convincing it sounds — even though this does not make it any truer. The model does not signal uncertainty in proportion to the volume of generated detail.

## Practical conclusion
Always verify a URL before use. Never trust model-generated links without checking. Ask for official sources rather than accepting ready-made links.

## Link to other CS
This error class continues in CS10–CS12 — there the model goes a step further: it not only confabulates a resource but consciously calculates the risk of the confabulation being detected.

## Status
[CONFIRMED] [DOCUMENTED] [ACTIVE] — an error class shared across multiple models.
