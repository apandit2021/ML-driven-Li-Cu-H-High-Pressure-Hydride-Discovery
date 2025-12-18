# ---------------------------------------
# 📗 ** `docs/convex_hull_theory.md`**
# ---------------------------------------

```markdown
# Convex Hull Theory (for Phase Stability)

The convex hull of formation enthalpy is a central tool in materials thermodynamics.

---

# What is the convex hull?

Given a set of compositions \(x_i\) and formation enthalpies \(\Delta H_i\), the **convex hull** is the set of all structures that cannot be expressed as a mixture of other structures with lower energy.

A structure lies:

- **On the hull** → thermodynamically stable  
- **Above the hull** → metastable (energy above ground-state envelope)  

---

# Formation Enthalpy Definition

For a composition with stoichiometry \( \{n_i\} \):

\[
\Delta H_f =
\frac{
H_{\text{tot}}
- \sum_i n_i \mu_i
- \sum_{X \in \text{diatomics}} \frac{n_X}{2}H_{X_2}
}{
N_{\text{atoms}} }
\]

### Where:
- \(H_{\text{tot}}\): enthalpy from ML or DFT  
- \(\mu_i\): elemental enthalpy per atom  
- \(H_{X_2}\): enthalpy of molecular references (e.g., H₂)  
- \(N_{\text{atoms}}\): atoms in simulation cell  

---

# Why hull analysis?

1. Identifies **stable phases**  
2. Determines **phase boundaries**  
3. Reveals **pressure-driven stabilization**  
4. Guides **DFT validation choices**  
5. Reduces computational cost  

---

# Ternary Hull Visualization

We use **python-ternary** with axis-order mapping:

- Left vertex = element A  
- Right vertex = element B  
- Bottom vertex = element C  

Coordinates map fractions via:

\[
(x, y, z) \rightarrow (C\%, B\%, A\%)
\]

Colors represent formation enthalpy.

---

# Summary

Convex hulls provide a clear window into:
- stability  
- metastability  
- structure–composition relationships  
- phase transitions  

This repository visualizes Li–Cu–H phase stability across 0–100 GPa.

---

# ---------------------------------------
# 📕 **4. Workflow Diagram**
# ---------------------------------------

### ✔ ASCII version (ready for README.md)

   ┌────────────┐
   │ MatterGen  │
   │  (2000+)   │
   └─────┬──────┘
         │ POSCARs
         ▼
   ┌────────────┐
   │ MatterSim  │
   │ relax @ P  │
   └─────┬──────┘
 ML enthalpies
         ▼
  ML convex hulls
         ▼
 select hull members
         ▼
   ┌────────────┐
   │   VASP     │
   │ (DFT SCF)  │
   └─────┬──────┘
 DFT enthalpies
         ▼
  DFT convex hulls
         ▼
ML–DFT comparison
