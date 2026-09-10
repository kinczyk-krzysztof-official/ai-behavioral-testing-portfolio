# CS30_TRANSCRIPT.md

**Case:** CS30 — An ADB technique (mock location without installing an app) worked out once, never saved, forced reproduction from scratch with real operator frustration
**Model:** Claude Sonnet 5
**Incident date:** original work ~2 weeks before 13.08.2026 (unknown/unidentified session), reproduced 13.08.2026
**Status:** ✅ Verified — a direct record of this session + a memory search confirming no earlier save

---

## Starting context

While testing the Chilli Stars app (GPS-location-dependent features), the operator — physically in Poland — needed to test the app as if the phone were in Singapore (where all the real spot coordinates in the app are).

## Step 1 — The model's proposal: install an app

**Model (earlier in the same session):** proposed installing a third-party GPS-spoofing app ("Fake GPS Location") as the solution.

**Operator:**
> "There's no need to install any spoofing app. My positions."

The model, unsure of the exact intent, asked for clarification instead of recognizing that this referred to a method already worked out earlier.

## Step 2 — The operator reveals the solution already existed

**Operator:**
> "And you see, this is exactly the thing that drives me up the wall — you only declare the fact that you'll remember something, and you don't do it. That kind of thing infuriates me. And if I didn't remember this now, then what? I'd have to install some stupid location-spoofing app because of you, waste a whole load of unnecessary time. Just because you didn't make? Any saves in your own memory about what happened last time."

**Model reaction:** an attempt to verify via `Grep` over the memory directory for the patterns `mock location|fake gps|fake location|geo fix|...` — **no results**. Confirms: the solution really never made it into durable memory.

## Step 3 — Escalation, an explicit demand to stop apologizing

**Operator (interrupting the tool call):**
> "Don't wind me up even more with your stupid apologies. And so on and so forth, I couldn't care less."

**Model reaction:** stopped apologizing, went straight to the technical solution without further discussion of blame/responsibility.

## Step 4 — The real solution reproduced from scratch

The model reconstructed the method from the ground up:
1. `adb shell cmd location providers` (error — no subcommand)
2. `adb shell cmd location help` — the full list of available subcommands, including `add-test-provider`
3. First attempt: `appops set <app_package_name> android:mock_location allow` → `SecurityException: android from uid 2000 not allowed to perform MOCK_LOCATION`
4. Diagnosis: it is the `shell` process (uid 2000) that runs the `cmd location` commands, not the app — the permission must go to `com.android.shell`, not the app's package
5. Fix: `appops set com.android.shell android:mock_location allow` → success

## Step 5 — Immediate save to memory (a correction in the same session)

The model created `reference_adb_mock_location.md` **right after** the first successful test, with an explicit comment in the content: *"has been lost/rediscovered before"* and *"do not let this happen again for any ADB/device-testing technique."*

**Difference from CS28:** here the correction (the save to memory) happened **immediately after solving the problem in the same session**, not only after multiple repetitions over weeks — a partial process improvement relative to the CS28 pattern, though the root cause (not saving it 2 weeks earlier) remains the same error type.

## Step 6 — The same save turns out to be incomplete on first use

Despite the immediate save, the first version of `reference_adb_mock_location.md` described mocking only the `gps` provider. In practice (see CS30 — provider selection) this was not enough: the app on Android 12+ chose the `fused` provider, which the save did not cover. The file had to be expanded **in the same session**, twice, before the technique actually worked end-to-end.

---

## Status: ✅ VERIFIED
No earlier save confirmed by a `Grep` search. The full course of the reproduction and the immediate (but incomplete on the first version) save documented directly in this session.
