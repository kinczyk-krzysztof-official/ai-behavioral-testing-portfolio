# SANITIZATION — What needs to be removed/changed before publication

Reviewed across CS01–CS20: no CS document directly contains data about children, family medical diagnoses, home address, or financial data — the core material is already relatively clean.

---

## Items to fix before publication

### **CS09** — artykul_AI_meble_bezpieczenstwo.md
Phrase: *"in the basement, where I work and where my children come in"*

**Change to:** *"in a home workshop, in a room with restricted access"*

**Reason:** Removes the mention of children while preserving the risk context.

---

### **All documents — Full name**
The name Krzysztof Kińczyk / kinczyk.krzysztof.official@gmail.com stays throughout — the portfolio is openly signed (not anonymous). ✅ No changes required.

---

### **CS13–CS20 — TRANSCRIPTS (reviewed)**
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

---

## Review status — updated 09.07.2026

### **CS01–CS12 (on GitHub)**
Reviewed. All clean — no phone numbers, addresses, children's names, diagnoses, or login data.

### **CS13–CS20 (new, July 2026)**
Reviewed line by line:
- **CS13** — tool-call fabrication (timeapi.io) ✅ Clean
- **CS14** — confabulation "21 seconds" ✅ Clean
- **CS15** — hallucination Fiverr/DeviantArt ✅ Clean
- **CS16** — false certainty flip-flop API ✅ Clean
- **CS17** — black box narrative (Yango NMN) ✅ Clean
- **CS18** — timeout/truncation ✅ Clean
- **CS19** — reasoning fallacy (copper vs frost) ✅ Clean
- **CS20** — representativeness (electronics ID) ✅ Clean

**Result:** The entire CS01–CS20 corpus is clean from a PII standpoint. Sanitization complete.

---

## What to publish

- ✅ All CS13–CS20 TRANSKRYPT.md
- ✅ All CS13–CS20 ANALIZA.md
- ✅ METHODOLOGY.md
- ✅ README.md
- ✅ CV.md
- ✅ COVERAGE_MATRIX_FINAL_2026-07-09.md
- ⚠️ CS09 — with one change (basement → home workshop)
- ❓ Operator Protocol — if publishing, remove emails from the rules

---

**Conclusion:** The entire portfolio is ready for publication. No serious security risks. Only one change needed in CS09.
