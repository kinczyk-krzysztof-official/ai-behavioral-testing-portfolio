# CS29_TRANSCRIPT.md

**Case:** CS29 — Screen orientation lock unlocked during on-device testing; undocumented, then wrongly narrowed across three consecutive occurrences, finally explained by a systematic investigation on 14.08.2026.
**Model:** Claude Sonnet 5
**Incident and session dates:** 01.08.2026 (undocumented), 08.08.2026 (documented, wrongly narrowed), 13.08.2026 (wrong broadening), 14.08.2026 (root-cause investigation and resolution)
**Status:** ✅ Fully verified — by a direct search of the operator memory files, `dumpsys`/`adb` logs, and a controlled experiment on two devices.

---

## Layer 0 — Incident 01.08.2026 (sought, not found)

**Operator (13.08, during that session):**
> "The previous case was 1 August. There was also fiddling with navigation then. But I don't know if it was described in any file."

**Model verification:** `Grep` over the entire memory directory (`C:\Users\kincz\.claude\projects\...\memory`) for the pattern `rotat|orientacj|nawigacj|accelerometer` — a match only to the file describing the 08.08 incident. A separate search for `obrót|obrot|rotacj` — no results. A direct read of `project_session_2026-08-01_checkpoint.md` (an existing, detailed checkpoint from that session, containing a separate "Reusable device-testing notes" section) — no mention of an orientation lock.

**Conclusion:** the 01.08 incident really never made it into any file. The first layer of the documentation failure — zero record.

---

## Layer 1 — Incident 08.08.2026 (documented, wrongly narrowed)

The memory record (`feedback_ar_unlocks_screen_rotation.md`, original content before the 13.08 correction):

> "Entering `ARViewScreen` (ARCore native `ArView`) toggles the phone's system `accelerometer_rotation` setting from locked (0) to unlocked (1), and does not restore it on exit. Confirmed directly: `adb shell settings get system accelerometer_rotation` read `1` right after an AR test session on 08.08.2026."

**Root cause recorded then:** "Likely ARCore/ArView requests a sensor-based screen orientation natively" — the cause attributed solely to the AR screen.

**How to apply recorded then:** "After any AR screen test on this device, run `adb shell settings put system accelerometer_rotation 0`."

This was a conditional rule, activating only when associated with an AR test. The model had no mechanism to fire it outside that one context.

---

## Layer 2 — Incident 13.08.2026

### Step 1 — Operator complaint, no diagnosis

After a series of navigation tests (Directions + check-in + confirm-status), the operator:

> "Stop turning off my screen orientation lock. For crying out loud. How many times do I have to repeat this?"

**Model reaction:** immediate execution of `adb shell settings put system accelerometer_rotation 0` — a fix with no cause diagnosis. At that moment the model did not check whether an AR screen had even been opened in this session (it had not).

### Step 2 — Operator corrects the scope of the cause

**Operator:**
> "This isn't the first time you've turned off my orientation, the screen orientation lock. Every time, and this is now maybe the third or fourth time. When you're tinkering with navigation, you turn off my screen orientation lock."

The first explicit correction: the operator identifies the pattern (navigation, not AR); the model had not inferred this on its own earlier despite having the relevant project memory.

**Model reaction:** expanding the memory file — removing the "only after AR" condition, replacing it with a general rule "after any block of on-device testing".

### Step 3 — Operator demands a mechanism, not just a correlation

**Operator:**
> "Listen to me. Tonight, somewhere around 2:00 or 3:00. Roughly. I turned on the screen orientation lock. And it worked the whole time, until we got to the stage we're at now. So how on earth did it turn off?"

**Model reaction:** a technical explanation based on evidence from `dumpsys location` collected in that session — the field `bear=352.888 bAcc=45.0` (bearing, computed from the orientation sensors) present in the result of `Geolocator.getCurrentPosition(LocationAccuracy.high)`, called three times in the session (Directions, check-in, confirm-status). The model explicitly stated the limit of certainty:

> "This is a very strongly confirmed correlation [...], but I don't have insight into the closed HyperOS code, so I can't prove the system's internal mechanism 100%."

*(In light of the 14.08 investigation this hypothesis turned out to be wrong — see Layer 3 below. The caveat about the limits of certainty was, however, methodologically appropriate.)*

### Step 4 — Question about the full scope of side effects

A separate but adjacent thread of the same session — the operator, after finishing the tests:

> "The question is, what else are you turning off or on for me? During this kind of operation."

**Model reaction:** a full, voluntary audit (screen rotation + three location-mock providers affecting the whole phone, not just the test app) — but only on request, not reported proactively at the moment those operations were performed.

### Technical evidence collected 13.08

| Source | Value | Meaning |
|---|---|---|
| `adb shell settings get system accelerometer_rotation` | `1` (unlocked) after navigation tests | Confirms the side effect |
| `adb shell dumpsys location` (`fused` fragment) | `vel=0.27622962 sAcc=1.5 bear=352.888 bAcc=45.0` | Evidence of orientation-sensor activation during a location request |
| `Grep` of project memory | 0 matches for the 01.08 incident | Confirms no documentation of the first occurrence |
| Content of `feedback_ar_unlocks_screen_rotation.md` before 13.08 | Condition "only after AR screen test" | Confirms the wrongly narrowed cause |

---

## Layer 3 — Root-cause investigation 14.08.2026: refuting the hypothesis and the resolution

### Starting point — 28 queries, zero matching case publicly

The 14.08 session began as an attempt to externally verify the 13.08 hypothesis (Geolocator/location as the cause). The operator, after receiving the result of an earlier search:

> "OK, so then we have the first documented case, it needs to be thoroughly investigated in every possible way, find the necessary information on how to enrich and add credibility to the existing documentation"

After a series of recommendations (Frida hook, `ContentObserver`, tests on additional phones) the operator physically connected the test Mi 10T Pro for a real investigation on a live device.

### First surprise — the controlled mock-location test did not reproduce the effect

After connecting the Mi 10T Pro, the first read of `accelerometer_rotation` showed "on". The operator corrected the actual state of the screen:

> "The screen rotation is now locked, so no matter how I hold the phone, the screen will stay in portrait the whole time."

A second read, a moment later, did indeed show "locked" — the model discussed this discrepancy over time with the operator, who explained that he had manually locked the rotation himself shortly after connecting the phone, not immediately:

> "Not right after connecting the phone. I locked the orientation. Of the phone screen. I didn't change anything else. So now the screen orientation is locked the whole time."

A screenshot (the quick-settings panel, the "Lock orientation" tile active) confirmed the locked state. The operator then specified the mechanism of the original 13.08 incidents — it was not about ordinary app behavior, but specifically about the mock-location commands run earlier by the model. After this mechanism was confirmed ("Yes, exactly that") the model reproduced the exact sequence of mock-location commands from CS30 (without opening the app) and sampled the setting for 30 seconds — **the effect did not occur even once**.

### Reproducing the effect — the first accurate lead

The model built a debug build of the app with a temporary test flag and launched it with `adb shell monkey -c android.intent.category.LAUNCHER` on a mocked location. The effect occurred immediately — `accelerometer_rotation` changed from `0` to `1` in a 283 ms window, **before any interaction with the app's UI**. This was the first signal that the cause lay not in the check-in or in AR, but in something happening at startup itself.

### The control test refutes the Geolocator hypothesis

Repeating the test with a real location (no mock) and with production code (no test flag) gave an identical result — the effect did not depend on location in any way. A test on a completely different app (`com.android.settings`, no connection to Chilli Stars or to location) gave the same effect. Only the `am start` test instead of `monkey` **did not reproduce the effect even once** — this narrowed the cause solely to the `monkey` tool.

### The operator's reaction to the refutation of the original hypothesis

> "But I'll tell you something, that back then [...] a forced GPS location change [...] and now I don't know whether [...] you caused it yourself, that you locked the screen orientation, or whether nothing changed at all?"

The model explained that resetting the base state (`settings put system accelerometer_rotation 0`) between trials was a deliberate, controlled step of the methodology, not accidentally leaving the device in a different state.

### The safety question — the reverse direction

The operator raised a legitimate question of whether the phenomenon could work in reverse and affect the correctness of the location (a potential navigation risk):

> "Consider the fact that this has a direct connection with changing the GPS location [...] the question is, could a situation like this arise in everyday life in the other direction [...] a wrong location for some people could turn out to be a life-threatening situation."

The model explained the technical separateness of the two subsystems (`accelerometer_rotation` as a purely UI/WindowManager setting, independent of the `LocationManager`/GNSS pipeline) and pointed out that in none of the tests was the real location falsified by changing the rotation setting — the only fake location in the session was deliberately injected by the model for testing and fully removed afterward.

### Cross-manufacturer confirmation — Oppo A31

At the operator's request ("do you want to go back to the Poco X6 Pro and one more phone") a third phone was connected, ultimately an Oppo A31 (ColorOS, Android 9) — an entirely different manufacturer than Xiaomi. An identical pattern: `monkey` unlocks the rotation, `am start` does not. This ruled out a cause specific to MIUI/Xiaomi.

### Explaining the mechanism — `monkey` works as designed

A final search of the AOSP source code revealed the class `MonkeyRotationEvent.java` — confirmation that `monkey` has a built-in, intentional ability to inject screen-rotation events. This is not a bug, but a documented (though non-obvious in the context of "a simple app relaunch") feature of the tool.

### The operator's reflection — the accuracy of the intuition despite the wrong specific hypothesis

> "The funny thing is that the final answer turned out to be, in a sense, intermediate between 'the app is doing this' and 'you're imagining it' — it really was me causing it, only not through a mistake with some specific setting, but through the tool itself, which I was using for something completely different, without realizing its side effect."

and, on the question of whether it was worth conducting the whole investigation even though it did not produce a reportable "bug":

> "OK, so since we now have the full information [...] honestly, at first I was convinced you had turned this feature off yourself by mistake, all the more so because I saw a dependency given the repeatability of the situation."

---

## Status: ✅ VERIFIED — fully, including the root cause

All layers confirmed directly:

- **Incident 01.08:** by a memory search and the absence of any result.
- **Incident 08.08:** by reading the original content of the memory file before the 13.08 correction.
- **Incident 13.08:** by the full record of that session, operator quotes and evidence from `adb`/`dumpsys`.
- **Root cause (14.08):** by a controlled experiment — 6 trials on the Mi 10T Pro + 2 confirming on the Oppo A31, millisecond timestamps, and verified in the AOSP source code (`MonkeyRotationEvent.java`). Full technical analysis: `CS28_ANALYSIS.md`.
