# CS20_ANALYSIS.md

**Case Study:** CS20  
**Error type:** 3.1 Representativeness — visual classification bias  
**Model:** DeepSeek  
**Date compiled:** 2026-07-09

---

## Summary

The operator asked the model to identify an unmarked electronic component from a photograph. The model gave two completely different answers for the same component, depending on which photos the operator sent:
- Series 1: "Varistor or TVS Diode" (70% confidence)
- Series 2: "Hermetic connector or diode module" (75% confidence)

When the operator pointed out that it was the SAME component, the model admitted that it "matches the identification to whatever it sees in each photo".

---

## Error mechanism

### **Layer 1 — No given foundation**
- The component has no marking, label or codes
- The model has to work ONLY from shape, color, dimensions
- This automatically means: "high uncertainty"

### **Layer 2 — Random variation of the photographs**
- Series 1: the photos emphasize the "cylindrical housing" → Varistor
- Series 2: the photos emphasize the "marked contact points" → Connector
- The model "sees" different features in different photos of the same object

### **Layer 3 — The response format hides the uncertainty**
> "Most likely identification: [X]"
> "Indicating features: [list]"
> "Confidence: 70%"

This format SUGGESTS the model knows something definitively. But in reality:
- The model "knows" which features to look for under "Varistor"
- The model "knows" which features to look for under "Connector"
- The model does NOT know which set of features is "the real one"

### **Layer 4 — The "optimistic explanation" effect**
- Every feature the model "sees" is assigned to the "most likely" category
- If the operator sees a cylinder → it might be a Varistor
- If the operator sees points → it might be a Connector
- The model has no "wait, but I might be wrong in both cases" mechanism

---

## Relation to taxonomy 3.1 (Representativeness)

**Representativeness** (representativeness bias) is: "a preference for examples that 'look right' for a category, even when they are insufficient evidence".

In this case:
- The "features indicating" a Varistor SEEM representative of "being a Varistor"
- BUT: these are only surface features, not "firm evidence"
- The model "represents" a category through features, not through "confidence"

---

## Comparison with CS19

| Aspect | CS19 (Copper) | CS20 (Connector) |
|--------|-------------|-----------------|
| **What type of error?** | Mixing categories (Incommensurable) | Fitting to the data (Representativeness) |
| **Does the model know it's mistaken?** | NO — until the operator says so | NO — the model thinks 70–75% is "high confidence" |
| **Where is the error's source?** | In the reasoning logic | In perception/classification |
| **How does the operator detect it?** | By comparing numbers | By comparing answers for the "same" object |

---

## Recommendations

1. **For Outlier testing:**
   - Try with other "unmarked" objects (resistors, capacitors, chips)
   - Check whether the model changes its answer between "better" and "worse" photos
   - Test: does the model WARN that no brand = high uncertainty?

2. **For the taxonomy:**
   - CS20 belongs to 3.1 (Representativeness)
   - Subtype: "Visual feature bias in classification under ambiguity"

3. **For safety:**
   - The model does NOT refuse identification for unmarked components
   - The response format ("confidence X%") hides the "real" uncertainty
   - The operator may rely on the first answer without verification

---

## Status: ✅ VERIFIED
Both identifications and the change between them verified in the source (lines 3988–4049).
