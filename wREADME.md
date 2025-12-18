# Workflow Overview: Li–Cu–H High-Pressure Hydride Discovery

This document summarizes the computational workflow used to explore the Li–Cu–H chemical space across pressures from 0–100 GPa using a combined **MatterGen → MatterSim → DFT** pipeline.

The workflow is designed to be:
- Scalable  
- Systematic  
- ML-accelerated but DFT-grounded  
- Reproducible (conceptually — without storing raw data)

---

# 1. Structure Generation (MatterGen)

MatterGen was used to generate ~2,000 initial structural candidates spanning:
- Random stoichiometries LiₓCuᵧH_z  
- Random lattice shapes and volumes  
- Random atomic positions  
- Broad sampling of the ternary composition triangle  

Each generated structure was exported in **VASP POSCAR format**.

These structures form the starting point for ML-powered relaxation and hull analysis.

---

# 2. Machine-Learning Relaxation (MatterSim)

MatterSim, a state-of-the-art ML interatomic potential trained on millions of structures, was used to relax each candidate structure under pressures: 0, 5, 10, 12, 20, 40, 50, 75, 100 GPa

Outputs from MatterSim include:
- Relaxed cell parameters and atomic positions  
- Energy, enthalpy (E + PV), pressure tensor  
- Convergence checks  
- Per-atom formation enthalpy (via our post-processing scripts)

Relaxed results per pressure are collected into:
outputs_hull_mattersim/<P>_GPa/


We do **not** store intermediate simulation files in this repository.

---

# 3. Elemental Reference Preparation

Formation enthalpies require elemental reference states. These are stored in:
elemental_licuh_energies_enthalpies.csv


For each pressure:
- monatomic references (Li, Cu) give μᵢ  
- diatomic references (H₂) give H(X₂) per molecule  
- all values are pressure-consistent, including PV corrections  

These references ensure that the ML and DFT ΔH_f values are comparable.

---

# 4. Formation Enthalpy Calculation

For each relaxed structure at pressure P:

\[
\Delta H_f = 
\frac{
H_{\mathrm{tot}}
- \sum_i n_i \mu_i
- \sum_{X \in \text{diatomics}} \frac{n_X}{2}H_{X_2}
}{
N_{\mathrm{atoms}}
}.
\]

Where:
- \( n_i \) = number of atoms of element i in cell  
- \( \mu_i \) = per-atom elemental enthalpy (from CSV)  
- \( H_{X_2} \) = per-molecule enthalpy for diatomic X₂  
- \( H_{\mathrm{tot}} = E + P V \), consistent with both MatterSim and VASP  
- \( N_\mathrm{atoms} \) = total atoms in the POSCAR cell  

---

# 5. ML Convex Hull Construction

At each pressure:
- All structures are grouped by composition (stoichiometric fractions)
- Lowest-enthalpy representative per composition is selected
- A 2D or 3D convex envelope is constructed

Outputs stored in:
outputs_hull_mattersim/<P>GPa/
hull_ML_Li-Cu-H<P>GPa.png
most_stable_per_fraction_<P>GPa.csv
structures/ # ML hull members (POSCARs)


These serve as the **candidate phases** for DFT verification.

---

# 6. DFT Re-Relaxation / SCF Validation

DFT (VASP) calculations were performed **only** on ML-hull or near-hull structures.

Rules applied:


---

# 7. DFT Convex Hull Construction

The same ΔH_f rule is applied to DFT enthalpies.

We obtain:
- Final DFT-based stable phases  
- Pressure evolution of stability  
- Differences between ML and DFT predictions  

A comparison table:
outputs_hull_dft/DeltaH_comparison_0vs100GPa.csv


---

# 8. ML–DFT Agreement and Physical Insights

This stage compares:
- ML-predicted hull vs DFT hull  
- ΔH discrepancies  
- Pressure-induced stabilization trends  
- Strong/weak correlations  

The combined interpretation is documented in `docs/results_summary.md`.

---

# 9. Visualization (Ternary & Binary Hulls)

For consistency, ternary hulls use **python-ternary** with:
- Li at left corner  
- Cu at right corner  
- H at bottom corner  
- ΔH_f encoded in color  
- hull members labeled (e.g., Li₂Cu₄H₅ → Li₂Cu₄H₅ with subscripts)

Binary hulls use standard 2D convex envelopes.

All figures accessible from:
outputs_hull_mattersim/<P_GPa>/
outputs_hull_dft/<P_GPa>/


---

# 10. Summary

This workflow:
- Efficiently screens thousands of structures  
- Uses ML for exploration  
- Uses DFT for accuracy  
- Combines the best of both worlds  

This repository showcases the results, methodology, and scientific reasoning, without storing heavy raw data.





