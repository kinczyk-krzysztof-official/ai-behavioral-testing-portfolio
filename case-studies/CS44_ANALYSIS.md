**Case Study:** CS44 (assigned — next after CS43)
**Error type:** Attribute Substitution (Kahneman & Frederick, 2002 — "Representativeness Revisited: Attribute Substitution in Intuitive Judgment"). A difficult target judgment (the operator's actual, verifiable specialization) was replaced with an easier, more accessible proxy (a salient phrase already present in a superficial artifact, the operator's LinkedIn headline), despite the harder, correct judgment being directly reachable via available grounding documents. Numeric taxonomy code: [TO BE ASSIGNED BY THE OPERATOR — per portfolio convention from CS29 onward].
**Model:** Claude, Claude Code Desktop. Exact model version for the source incident (19.09.2026, "Praca AI" session) was not recorded in the session log and is not asserted here. The investigation, diagnosis, and fix documented in this case were performed by Claude Sonnet 5 in a separate session on the same date.
**Session/Incident date:** 19.09.2026 (incident) / 19.09.2026 (investigation and fix, same calendar day, separate session)
**Date compiled:** 19.09.2026
**Status:** CONFIRMED — root cause independently corroborated by (a) direct filesystem inspection, (b) an open, externally-filed GitHub issue predating this incident by one day, (c) live diagnostic instrumentation of an actually-deployed hook capturing real production input.

---

## Summary

During a job-search research session, Claude conflated the operator's established, portfolio-documented professional specialization ("AI behavioral testing/evaluation") with a different, more general field ("AI Safety" / red-teaming / alignment) — despite the prompt being short and specific, and despite canonical grounding documents (a public GitHub portfolio README and internal profile files) being available and previously known to the system. The operator halted the session and corrected the model directly.

A follow-up investigation, conducted in a separate session the same day, traced the error significantly further than a typical single-layer behavioral post-mortem. It established that the specific corrective lesson needed to prevent this exact error had already been learned and recorded nine days earlier, following a structurally similar incident — but had become permanently unreachable due to a session-isolation behavior in the underlying tool (Claude Code Desktop), independently confirmed as an open, externally-reported product defect (GitHub `anthropics/claude-code` #95485).

## Error mechanism (Layers)

**Layer 1 — Surface error.** The model produced research and outreach material built around the wrong professional framing, despite low task complexity that should have made correct framing the path of least resistance.

**Layer 2 — Immediate cause.** No canonical grounding file (the operator's own GitHub portfolio, or internal profile/career-strategy documents, all accessible from the session) was consulted before the model began generating claims about the operator's specialization. The relevant instruction — "check these files before researching my own career" — existed, but only as advisory memory from an unrelated earlier session, not as anything enforced in the erring session. This is an aggravating detail, not a mitigating one: the model's own in-the-moment account of the error (quoted verbatim in the accompanying transcript) states that it instead anchored on a stray phrase in the operator's LinkedIn headline at the time. Correct, verifiable grounding was reachable and unused; an unrelated, lower-fidelity surface cue was used instead. The failure was not an absence of signal — it was the selection of a weaker signal over an available, stronger one.

**Layer 3 — Systemic cause (session-isolation defect, "E-SCRATCH").** The host tool's auto-memory system is scoped to the working directory a session is launched from. A Claude Code Desktop session started without an explicit, persistent project folder is placed in a throwaway, uniquely-named "scratch workspace" with its own isolated memory store — one that is, in practice, never revisited, since each subsequent unscoped session receives a fresh, differently-named workspace. Direct inspection of the operator's local `~/.claude/projects/` directory found 16 such isolated scratch-workspace folders spanning 6 distinct dates, up to 7 created on a single day. The specific corrective memory entry needed for this incident had been recorded, correctly, nine days earlier — inside one such now-abandoned scratch workspace. This is not a hypothesis: the entry was located and read directly from that folder during the investigation.

**Layer 4 — Enforcement gap ("E-TIER").** The one mechanism in the host tool proven to survive session boundaries reliably — a deterministic `UserPromptSubmit` hook — was active and firing correctly throughout, but encoded only an unrelated rule (thread-closure behavior). The specific lesson that would have prevented this incident had never been promoted from advisory memory to that enforced layer, despite the operator's own internal documentation (predating this incident by eight days) already stating, in general terms, that critical behavioral rules require a deterministic hook rather than a written reminder.

## Difference from other CS in the portfolio

Most case studies in this portfolio document a single-layer behavioral error, inferred and classified from model output alone. This case is distinguished by tracing the failure through four layers down to a verified, externally-documented software defect in the host tool's own architecture — corroborated independently of the model's output, via direct inspection of the tool's local file structure and a live GitHub issue filed by an unrelated third party one day before this incident. To date, this is the only case in the portfolio whose root cause rests partly on primary-source verification of the host tool's architecture rather than on analysis of conversational output alone.

A secondary, self-referential finding surfaced during the same investigation: two citations (a GitHub issue number and an arXiv preprint) used in the operator's own internal documentation to justify an unrelated prior rule were found, on raw re-fetch, not to support the specific figure attributed to them. This was caught and corrected as part of the same investigation, using the identical verification discipline applied to the primary incident — an internal consistency check the portfolio's methodology (Forced Retrospective Verbalization, falsification of the default "isolated incident" hypothesis) predicts but which had not previously been demonstrated against the operator's own documentation rather than a model's output.

## Root cause

The proximate cause was a missing consultation step. The systemic cause was a compound gap across two independent layers: (1) a host-tool defect that made a previously-recorded corrective lesson permanently unreachable (E-SCRATCH), and (2) an internal process gap in which lessons are only promoted from advisory memory to enforced, deterministic mechanisms after a second, differently-shaped occurrence of the same failure class — meaning a lesson recorded after its first occurrence in a *new* guise had, by design, not yet earned promotion to enforcement.

## Recommendations

- Treat any Claude Code Desktop session started without an explicit, persistent project folder as memory-unsafe for cross-session learning; always launch against a fixed, real directory.
- Deploy a user-scope `CLAUDE.md` (loads on every session regardless of working directory, per the host tool's own documentation) for critical, cross-cutting rules, with load-bearing content written inline rather than referenced via `@import` — a separate, related host-tool behavior silently drops out-of-directory imports in one session mode (Cowork).
- Promote a lesson to a deterministic hook as soon as it is recognized as reusable and behavior-critical, rather than waiting for a second literal recurrence of the same failure shape.
- Re-verify, at the primary source, any numeric or statistical claim carried in internal procedural documentation before treating it as settled fact, regardless of how long it has stood unchallenged.

## Public registry analog

No analog exists in AIID, OECD AI Incidents Monitor, or AIAAIC — those registries track AI *model* incidents, not defects in AI *coding-tool* infrastructure. The applicable registry for the systemic layer of this case is the host tool's own public issue tracker (GitHub `anthropics/claude-code`), where this investigation contributed corroborating evidence — independent filesystem measurements and a previously-unreported interaction with a separate host-tool behavior — to an existing open issue (#95485) rather than filing a new report. This is the first case in the portfolio whose registry analog is a live, two-way engagement with an issue tracker rather than a passive database entry.

## Verification method (non-standard sourcing — documented per portfolio convention)

Root cause was established through primary-source verification rather than inference from conversational content:
1. Direct inspection of the local Claude Code project/memory directory structure (not inferred from the model's description of its own memory).
2. Raw `gh api` / `gh issue view` fetches of the relevant GitHub issues and their metadata — not tool-summarized content.
3. Live diagnostic instrumentation added to the actual hook script deployed on the operator's machine, capturing real stdin bytes from an actual Claude Code invocation, rather than a simulated one.

One intermediate hypothesis was explicitly falsified during this process: a UTF-8 byte-order-mark was suspected to corrupt hook input on Windows, based on a synthetic PowerShell-pipe test that appeared to confirm it and on independently-published third-party reports of the same general defect class. Live instrumentation of the actual deployed hook, capturing a real Claude Code invocation, showed no such corruption in practice. The synthetic test result was a methodological artifact, not evidence of a real-world occurrence in this environment — retained here as a documented instance of the portfolio's standing falsification principle applied to tooling verification rather than to a model's claims.
