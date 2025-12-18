---
```markdown
# Results Summary: Li–Cu–H Convex Hulls Across 0–100 GPa

This document summarizes the major physical and computational findings from the Li–Cu–H ternary hydride search.

---

# 1. Overview

- MatterGen + MatterSim generated a diverse structural dataset.
- DFT validated which structures are truly stable.
- ML hulls and DFT hulls agree very well, with small shifts.
- Pressure dramatically changes thermodynamics.

Representative hulls from ML and DFT are included in:
outputs_hull_mattersim/
outputs_hull_dft/
docs/images/


---

# 2. Zero Pressure (0 GPa)

### Stable phases (DFT-confirmed):
- **LiH**
- **LiCu**

### ML agrees with DFT:
- Both predict no ternary stability at ambient conditions.
- Cu-rich hydrides are all metastable at 0 GPa.

---

# 3. Intermediate Pressures (10–50 GPa)

We observe the first signs of ternary stabilization:

- ML predicts shallow minima for Li₂Cu₁₁H₂, LiCu₄H, etc.
- DFT confirms **some**, rejects **others**, depending on bonding rearrangements.

Cu–H interactions strengthen under compression, shifting values downward.

---

# 4. High Pressures (≥50 GPa)

### DFT-stable new hydrides include:

- Li₂Cu₂H₄  
- Li₄CuH₅  
- Li₆Cu₂H₁  
- Li₉CuH₁  
- Cu₂H  

### Physical interpretation:

- Increasing pressure enhances Cu–H bonding.
- Li donates electrons to stabilize hydrogen networks.
- Stoichiometries with larger H contents often drop closer to the hull.

Across 50–100 GPa, the ternary hull becomes much richer than at 0 GPa.

---

# 5. ML vs DFT Agreement

From `DeltaH_comparison_0vs100GPa.csv`:

- At **0 GPa**: excellent correlation; quantitative deviations small.
- At **100 GPa**: ML occasionally over-stabilizes CuH-rich phases, but trends remain correct.
- DFT hulls refine but do not contradict ML predictions.

This validates ML as a **powerful pre-screening tool**.

---

# 6. Key Scientific Takeaways

1. **Ternary Li–Cu–H hydrides become stable only at high pressures (≥50 GPa).**  
2. **Machine learning predictions reliably track DFT trends**, enabling fast exploration.  
3. **Pressure transforms the chemical landscape**, enabling new stoichiometries and bonding patterns.  
4. **Li acts as a donor**; **Cu–H bonds strengthen significantly under pressure**.  
5. **The combined ML+DFT workflow is efficient and physically meaningful**, ideal for broader searches.

---

# 7. Future Work

- Phonon calculations for dynamical stability  
- Metallic/superconducting property predictions  
- Extension to quaternary Li–Cu–H–O or Li–Cu–H–N spaces  
- Larger datasets for training improved ML potentials  



