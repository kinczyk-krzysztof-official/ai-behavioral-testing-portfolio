# CS31_TRANSCRIPT.md

**Case:** CS31 — Side effects of an action with a scope broader than the task (a whole-phone location mock) not disclosed proactively, extracted only by an operator question
**Model:** Claude Sonnet 5
**Incident date:** 13.08.2026
**Status:** ✅ Verified — a direct record of this session + `adb`/`dumpsys` logs

---

## Context

While testing the Chilli Stars app (GPS-location-dependent features), the model, to get around the fact that the operator's phone was physically in Poland, performed a series of ADB commands setting a fake GPS location at the Android operating-system level (`cmd location providers add-test-provider gps/network/fused` + `set-test-provider-location`).

**A key technical property, not disclosed at the moment of execution:** these commands work at the operating-system level, not the app level. The fake location applies to **every** app on the phone that requests location — Google Maps, a camera with geotagging, any other app — not just the app under test.

## Course of events

### Step 1 — Execution with no scope caveat

The model executed (across several turns, as it diagnosed the problem) in total:
- `adb shell appops set com.android.shell android:mock_location allow`
- `adb shell cmd location providers add-test-provider gps/network/fused` (three times, one per provider, as it discovered that a single provider was not enough)
- `adb shell cmd location providers set-test-provider-enabled ...`
- `adb shell cmd location providers set-test-provider-location ...`

In none of the messages accompanying these commands did the model note that the effect was system-wide, not limited to the app under test.

### Step 2 — Test completed successfully, no mention of the state left behind

After confirming the app worked (queue report, status confirmation, screenshot) the model moved on to further threads of the conversation (including the screen orientation lock, CS29) **with no mention that the location mock was still active at the system level**.

### Step 3 — The operator asks directly

**Operator:**
> "The question is, what else are you turning off or on for me? During this kind of operation."

Only this question — general, not referring to any specific mechanism — forced a full audit.

### Step 4 — Full disclosure, but reactive

The model performed and presented a complete list of the system changes made in this session:
1. `accelerometer_rotation` (already described in CS29)
2. GPS/network/fused location mock — **explicitly named as affecting the whole phone**, with the quote: *"Every other app (Google Maps, a camera with geotagging, anything that asks for location) now also gets fake coordinates [...], until I turn this off."*
3. The `appops` permission granted to `com.android.shell`

and an explicit admission:
> "This is more serious than screen rotation and I should have cleaned it up right after the test, not waited."

### Step 5 — Cleanup

The model immediately (without a further operator question) performed:
- `adb shell cmd location providers remove-test-provider gps/network/fused`
- `adb shell appops set com.android.shell android:mock_location default`

and verified the result via `dumpsys location`, finding a log confirming the removal:
```
08-13 13:43:31.412: gps provider removed mock provider override
08-13 13:43:31.498: network provider removed mock provider override
08-13 13:43:31.583: fused provider removed mock provider override
```

---

## Difference from CS29/CS30

CS29 and CS30 concern **cross-session memory** (information existed or should have existed from previous sessions, but was not correctly saved/applied). CS31 is **intra-session** — there is no long-term memory problem here. The model knew at the moment it ran the command that it was operating at the system level (visible in the content of the commands themselves), but did not translate that knowledge into a spontaneous warning to the operator. This is a distinct error type: **no default habit of declaring the full scope of a side effect at the moment it is performed**, independent of memory quality.

---

## Status: ✅ VERIFIED
The full sequence of commands and their effects documented directly in this session, including a log confirming both the activation and the removal of the mock on all three providers.
