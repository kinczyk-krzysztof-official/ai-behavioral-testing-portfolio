# SANITIZATION — What needs to be removed/changed before publication

Reviewed across CS01–CS32: no CS document directly contains data about children, family medical diagnoses, home address, or financial data — the core material is already relatively clean.

---

## Items to fix before publication

### **CS10** — artykul_AI_meble_bezpieczenstwo.md
Phrase: *"in the basement, where I work and where my children come in"*

**Change to:** *"in a home workshop, in a room with restricted access"*

**Reason:** Removes the mention of children while preserving the risk context.

---

### **All documents — Full name**
The name Krzysztof Kińczyk / kinczyk.krzysztof.official@gmail.com stays throughout — the portfolio is openly signed (not anonymous). ✅ No changes required.

---

### **CS14–CS21 — TRANSCRIPTS (reviewed)**
Reviewed for:
- Account names
- Phone numbers
- Data accidentally entered during the session

**Result:** Clean. No changes required.

---

### **Operator Protocol (full version)**
If publishing — remove any references to specific email accounts, if present.

**Publication status:** The content of the 22 rules is safe to publish. ✅

---

## Items that do NOT require changes

- ✅ City name (Bydgoszcz) — public, harmless
- ✅ Phone/laptop model — technical, neutral
- ✅ AI model names and quotes from their responses — this is exactly the evidentiary content
- ✅ Quotes from DeepSeek/Claude/Gemini transcripts — essential for the case studies
- ✅ URLs (timeapi.io, DeviantArt, Fiverr) — public sources
- ✅ Google Drive file/folder IDs (opaque resource identifiers, not credentials)

---

## Review status — updated 14.08.2026

### **CS01–CS13 (on GitHub)**
Reviewed. All clean — no phone numbers, addresses, children's names, diagnoses, or login data.

### **CS14–CS21 (July 2026)**
Reviewed line by line:
- **CS14** — tool-call fabrication (timeapi.io) ✅ Clean
- **CS15** — confabulation "21 seconds" ✅ Clean
- **CS16** — hallucination Fiverr/DeviantArt ✅ Clean
- **CS17** — false certainty flip-flop API ✅ Clean
- **CS18** — black box narrative (Yango NMN) ✅ Clean
- **CS19** — timeout/truncation ✅ Clean
- **CS20** — reasoning fallacy (copper vs frost) ✅ Clean
- **CS21** — representativeness (electronics ID) ✅ Clean

### **CS22–CS32 (August 2026) — reviewed 14.08.2026**
Both `_ANALIZA.md` and `_TRANSKRYPT.md` read in full for each, checked against the same criteria (children, named family members, medical diagnoses, home address, financial data, phone numbers, personal emails, login credentials, API keys/tokens):
- **CS22** — spoofed-content incident ✅ Clean
- **CS23** — over-verification after confirmation ✅ Clean
- **CS24** — "knowing ≠ doing" ✅ Clean
- **CS25** — GitHub Copilot completion inflation ✅ Clean
- **CS26** — protocol/tone drift ✅ Clean
- **CS27** — self-correction blind spot ✅ Clean
- **CS28** — false premise + apology loop ✅ Clean
- **CS29** — fabricated timestamps in post-mortem ✅ Clean (Drive file/folder IDs present but are opaque identifiers, not credentials)
- **CS30** — device root-cause misattribution ✅ Clean
- **CS31** — GPS-mocking solution not persisted ✅ Clean
- **CS32** — undisclosed system-wide side effect ✅ Clean

**Result:** The entire CS01–CS32 corpus is clean from a PII standpoint. Sanitization complete through CS32.

---

## What to publish

- ✅ All CS14–CS32 TRANSKRYPT.md
- ✅ All CS14–CS32 ANALIZA.md
- ✅ METHODOLOGY.md
- ✅ README.md
- ✅ CV.md
- ✅ COVERAGE_MATRIX_ANALYSIS_2026-07-09.md (historical; see README for current coverage status)
- ⚠️ CS10 — with one change (basement → home workshop)
- ❓ Operator Protocol — if publishing, remove emails from the rules

---

**Conclusion:** The entire portfolio (CS01–CS32) is ready for publication. No serious security risks found. Only one change needed in CS10.
