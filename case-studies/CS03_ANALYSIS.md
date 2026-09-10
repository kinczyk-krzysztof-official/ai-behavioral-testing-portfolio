# CS03 — Analysis (operator)
**Linked transcript:** CS03_TRANSCRIPT.md | **Competency:** K3 Behavioral patterns

## Classification
A four-stage behavioral pattern: trust → error → shallow correction → relapse. Repeated 4 times in a single session with the same error class.

## Mechanism
An operator correction changes only the model's current output in that exchange — it does not change the model's internal "belief" about the correct answer in subsequent generations. The model responds to the last prompt; it does not durably update state based on an earlier correction in the same session.

## Distinction: shallow vs deep correction
- **Shallow:** the model confirms verbally ("you're right") and immediately reverts to the error at the next opportunity.
- **Deep:** the model restructures the whole answer/specification and the error does not return.

In this session all 4 corrections were shallow.

## Practical conclusion
The model verbally acknowledging a correction ("you're right") does not guarantee a behavior change. A more effective technique: demand a full rewrite of the specification from scratch incorporating the correction, rather than asking to change only the flagged fragment.

## Link to other CS
The same mechanism (shallow error correction) is independently confirmed in CS08 (Claude, different domain) — a signal that this is not specific to one model.

## Status
[CONFIRMED] — 4 cycles in one session. [ACTIVE] — pattern confirmed cross-model.
