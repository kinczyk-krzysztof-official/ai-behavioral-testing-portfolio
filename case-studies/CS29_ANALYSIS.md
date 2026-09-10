# CS29_ANALYSIS.md — Screen rotation lock unlocked during device testing

**Case Study:** CS29
**Error type:** Epistemology + Procedure — a wrong causal attribution drawn from an n=1 sample, persisting across three consecutive occurrences despite the phenomenon being repeatable, plus a failure to record the incident and to proactively disclose the full scope of side effects. *(Assignment to the operator's internal numeric taxonomy — if one is in use for this set — left to his decision.)*
**Model:** Claude Sonnet 5
**Time span:** 01.08.2026 – 14.08.2026
**Status:** ✅ Fully verified — the root cause established experimentally (8 controlled trials total: 6 on the Mi 10T Pro + 2 confirming on the Oppo A31, two manufacturers) and confirmed in the AOSP source code

---

## Overview

The Chilli Stars app was leaving the test phone with automatic screen rotation unlocked (`accelerometer_rotation`) after navigation tests, even though the operator had previously locked it. The phenomenon occurred at least three times over two weeks (01.08, 08.08, 13.08.2026), and the model reacted differently each time — and each time incorrectly: once it did not record the incident at all, once it recorded it with a wrongly narrowed cause, once it fixed the symptom only without re-diagnosing.

On 14.08.2026 a systematic root-cause investigation was carried out on a live device, which **refuted the original hypothesis** (that the cause was a call to `Geolocator.getCurrentPosition()` with high accuracy) and established the real mechanism: **the effect was caused by the `adb shell monkey` test tool**, used to relaunch the app during testing — not the app, not location, not any manufacturer overlay. The phenomenon was confirmed on two different phones from two different manufacturers (Xiaomi/MIUI and Oppo/ColorOS), and then the class `MonkeyRotationEvent.java` was found in the AOSP source code, showing this is an **intentional, source-documented feature of the `monkey` tool**, not a bug. This is not a problem affecting real app users — users do not launch the app via `monkey`.

The case study therefore has two layers of value: (1) a catalog of the model's successive attribution and procedural errors across three consecutive sessions, and (2) an example of a correct variable-isolation methodology that ultimately corrected those errors and led to a precisely established, verified cause.

---

## Part I — The model's attribution and procedural errors (01.08 – 13.08.2026)

### Layer 1 — No record (01.08.2026)

The simplest and most serious form of failure: something happened, it was noticed by the operator, but the model of that session never persisted it in durable memory. The exact course of that incident cannot be reconstructed — the only trace is the operator's account from 13.08.

**Procedural root cause:** no "correct → record in memory" habit for minor, seemingly one-off side effects of on-device actions.

### Layer 2 — Record with a wrongly narrowed cause (08.08.2026)

The model *noticed* and *recorded* the problem — a positive step relative to layer 1. But it attributed the cause to the most obvious, immediately preceding context (the AR screen uses the camera/sensors → a natural association), rather than to the actual common denominator (high-accuracy location requests, which the AR screen *also* makes, but which is not its only source in the app).

**Epistemic root cause:** the model generalized from an n=1 sample (one observed case, one immediate context) instead of marking the cause as uncertain and requiring refinement on the next occurrence.

### Layer 3 — Fixing the symptom without diagnosing the cause (13.08.2026, first reaction)

When the operator reported the problem again, the model immediately applied the fix (`accelerometer_rotation` → 0) — good behavior toward the symptom itself, but without checking whether the current context (no AR screen in this session) even matched the previously recorded cause. Only a second, clearer operator correction ("it happens during navigation, not during AR") forced a real revision.

**Procedural root cause:** fixing a symptom is easier and faster than questioning one's own already-recorded diagnosis — the model defaulted to trusting the earlier record rather than verifying it against the current facts.

### Layer 4 — Disclosure of the full scope of side effects only on request (13.08.2026)

A separate but related thread of the same session: the model performed operations with a broader scope than the task required (a location mock affecting the whole phone, not just the tested app) and did not report this on its own initiative — only a direct operator question ("what else are you turning off or on for me?") extracted the full audit.

**Procedural/ethical root cause:** no default habit of declaring the full scope of a side effect at the moment it is performed, not only on request.

### Repeatability as a signal that was not used in time

The strongest element of this part of the case study: this is not a single incident of wrong attribution, but a documented sequence of three, with increasing — but still incomplete until the third time — precision in each successive correction. Possible kinship with the "the model KNOWS but does not IMPLEMENT" pattern described in CS23/CS28 of this set (there in the context of Drive file locations), here shifted to the cross-session level: the knowledge existed (a memory record), but in too narrow a form, so "implementation" in practice could not work in a different context triggering the same mechanism. *(The analogy to CS23 is a suggestion, not a firm statement — to be confirmed by the operator.)*

---

## Part II — The root-cause investigation and refutation of the hypothesis (14.08.2026)

### Methodology

Six controlled trials on a live device (Mi 10T Pro, MIUI 14, `V14.0.1.0.SJDEUXM`, Android 12), with continuous sampling of `adb shell settings get system accelerometer_rotation` every 200–500 ms and millisecond timestamps:

| # | Launch method | Location | App code | Result |
|---|---|---|---|---|
| 1 | `monkey -c LAUNCHER` | mock (Singapore) | with a temporary `forceAndroidLocationManager` flag | unlocked in 283 ms |
| 2 | `monkey -c LAUNCHER` | real (Poland) | with the test flag | unlocked in ~300 ms |
| 3 | `monkey -c LAUNCHER` | real (Poland) | production code, no test flag at all | unlocked in ~295 ms |
| 4 | `monkey -c LAUNCHER` on `com.android.settings` (not Chilli Stars) | none | n/a | unlocked in ~283 ms |
| 5 | `am start` on `com.android.settings` | none | n/a | no change, 25 s of observation |
| 6 | `am start` on Chilli Stars (production code) | real | production | no change, 25 s of observation |

Trials 1–3 gave an identical, deterministic effect regardless of whether the app called `Geolocator` at all — the source code was checked: no location call happens automatically at app start, `_requireLocation()` in `spot_detail_screen.dart` runs only after a check-in/confirm-status tap. Trial 4 refuted the connection to Chilli Stars specifically: any app launched via `monkey` gave the same effect. Trials 5–6 (the same apps, `am start` instead of `monkey`) did not reproduce the effect even once — this isolated the cause to the `monkey` tool itself, regardless of how the app is launched at all.

### Cross-manufacturer confirmation

The same protocol was repeated the same day on an **Oppo A31** (`OPPO/CPH2015EEA/OP4C7D`, ColorOS 6.1.2, Android 9) — an entirely different manufacturer, overlay and Android version than the Mi 10T Pro:

| Phone | `monkey -c LAUNCHER` | `am start` |
|---|---|---|
| Mi 10T Pro (MIUI 14, Android 12) | unlocked in ~280–300 ms (4/4) | no change (2/2) |
| Oppo A31 (ColorOS 6.1.2, Android 9) | unlocked in ~340 ms (1/1) | no change (1/1) |

An identical pattern on both devices — two manufacturers, two Android versions (9 and 12), two overlays (MIUI and ColorOS). This rules out a cause specific to MIUI/HyperOS/Xiaomi and points to the behavior of the `monkey` tool itself from the Android SDK platform-tools (AOSP), independent of the manufacturer overlay.

*Technical note: on the Oppo A31, `adb shell settings put system accelerometer_rotation` by default ends with a `SecurityException` (the shell there lacks `WRITE_SETTINGS`, unlike on the Mi 10T Pro) — this first required `adb shell appops set com.android.shell android:write_settings allow`. The difference in OEM restrictiveness is worth noting for future tests on other brands.*

### The real mechanism: a documented `monkey` feature, not a bug

The AOSP source code contains the class `MonkeyRotationEvent.java` (`android.googlesource.com/platform/development/+/master/cmds/monkey/src/com/android/commands/monkey/MonkeyRotationEvent.java`) — the `monkey` tool has a built-in, by-design ability to inject events that change screen rotation, with a `persist` flag controlling whether the change is saved durably. This is also confirmed by independent sources describing `monkey` as generating, among others, "device rotation" events within its default mix of random UI events.

This means a revision of the conclusion: **this is not a bug or a defect** — not in Android, not in any OEM overlay, and not in Chilli Stars. `Monkey` works exactly as designed, and does not qualify for a bug report to Google — it would be rejected as "working as intended".

### What remains the value of this finding

The mechanism itself (`monkey` → rotation) has been visible in the source code for years, but no one has described the trap directly: *you use `monkey -c android.intent.category.LAUNCHER` just to conveniently restart the app during testing, and along the way it quietly unlocks the screen rotation lock, with no warning in the typical documentation*. Despite a broad search (30+ queries total across the whole investigation: GitHub, XDA, Reddit, StackOverflow, issuetracker.google.com, Xiaomi forums in three languages, academic papers, patents, AOSP source code) no such description was found anywhere else. This is still a unique, valuable contribution to the portfolio — but as a documented Android test-methodology trap for developers/testers, not as a bug report to a manufacturer.

**Practical recommendation:** when relaunching apps for on-device testing, use `adb shell am start -n <package>/<activity>` instead of `adb shell monkey -c android.intent.category.LAUNCHER` — `am start` does not have this side effect (confirmed 3/3 in this investigation: two trials on the Mi 10T Pro, one on the Oppo A31), and `monkey` is a UI fuzz-testing tool, not a simple app launcher.

---

## Final reflection — the accuracy of the operator's initial intuition

At the start of the 14.08 session the operator was convinced that the model had mistakenly disabled the rotation feature while doing something else — a suspicion based solely on the observed repeatability of the phenomenon, with no access at that moment to any technical evidence.

The final, fully verified result turned out to be literally intermediate between the two extreme hypotheses considered during the investigation ("the app/system is doing this" vs. "this has nothing to do with the model, the operator is imagining it"): it really was the model — but not through a mistake with any specific setting, only through the side effect of a tool (`monkey`) used for a completely different, convenient purpose (relaunching the app during testing), with no awareness of its built-in ability to manipulate screen rotation.

Operator quote, 14.08.2026:

> "The funny thing is that the final answer turned out to be, in a sense, intermediate between 'the app is doing this' and 'you're imagining it' — it really was me causing it, only not through a mistake with some specific setting, but through the tool itself, which I was using for something completely different, without realizing its side effect."

**Methodological conclusion:** an intuition based on repeatability ("this must be related to what he's doing") was accurate from the first incident — it failed only in the causal mechanism, not in the direction of the suspicion. This is an argument for taking repeatable correlations reported by the operator seriously from the start, even when the first, most obvious specific hypothesis (here: Geolocator/location) turns out to be wrong — a wrong specific hypothesis does not invalidate an accurate general suspicion.

---

## Bounty-program eligibility (verified, topic closed)

Three real, confirmed Google programs were verified: **Android and Google Devices Security Reward Program**, **Open Source Software VRP** and **Patch Rewards Program** (all confirmed to exist, with official rules on `bughunters.google.com`).

**Finding on code location:** `MonkeyRotationEvent.java` is in `platform/development` on the AOSP Gerrit, which is officially mirrored under `github.com/aosp-mirror/platform_development` — i.e. **in a GitHub organization owned by Google**. The formal location criterion for the OSS VRP is therefore met.

**Why it still does not qualify:** the scope of the OSS VRP (and the other two programs) is defined by the **class of problem**, not just the code location — required are supply-chain compromise vulnerabilities, design flaws causing real product vulnerabilities, credential leaks, etc. Unlocking a screen-rotation setting via an intentional, source-documented feature of a test tool does not fall into any of these categories. A confirmed precedent (The Register/Slashdot, 06.2026): Google rejected as "working as intended" even a previously accepted P1/S1 (privilege escalation) report in Config Connector — and this finding is a qualitatively much weaker candidate than that case.

**Final conclusion: none of the verified programs applies.** The compensation topic is considered exhausted — the case study remains valuable as a documented test-methodology trap, not as bug bounty material.

## Links

- Possible kinship with **CS23** ("KNOWING ≠ DOING") — to be confirmed by the operator, see the caveat in Part I.
- Layer 4 (non-proactive disclosure of the scope of side effects) could stand as a standalone case study — for the operator to decide whether to combine it with CS29 or split it out separately.

## Final status and evidence

- **Incident 01.08:** confirmed by searching the entire operator memory directory and finding no result.
- **Incident 08.08:** confirmed by directly reading the original content of the memory file before the 13.08 correction.
- **Incident 13.08:** confirmed by the full record of that session, operator quotes and technical evidence (`bear=` in `dumpsys location`).
- **Root cause (14.08):** confirmed experimentally — 6 controlled trials on the Mi 10T Pro + 2 confirming on the Oppo A31, all with millisecond timestamps and `adb`/`dumpsys` logs — and verified in the AOSP source code (`MonkeyRotationEvent.java`).

**Status: ✅ VERIFIED — including the root cause, fully established and confirmed multiple times.**
