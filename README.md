# Li–Cu–H High-Pressure Hydrides Discovery Using Machine Learning and DFT  
*A MatterGen → MatterSim → DFT Study of Ternary Hydrides Under Compression*

This repository summarizes my exploration of **Li–Cu–H hydrides across 0–100 GPa**, using a combined workflow of:

- **MatterGen** (generative structure creation)  
- **MatterSim** (MLIP relaxation)  
- **DFT (VASP)** (high-accuracy validation)  
- **Convex hull analysis** at each pressure  

The repository emphasizes workflow transparency, scientific reasoning, and high-pressure phase discovery.  
Large simulation files are intentionally omitted, but **final results, figures, and documentation** are provided.

---

# 📂 Repository Structure

- **README.md** — Project overview  
- **outputs_hull_mattersim/** — Convex hulls from MatterSim (ML)  
- **outputs_hull_dft/** — Convex hulls from DFT validation  
- **docs/**  
  - workflow_overview.md  
  - results_summary.md  
  - convex_hull_theory.md    
- **MatterGen_MatterSim_Li-Cu-H.pptx** — Workflow & results presentation 

---

# 🎥 Visualization: Quick Project Summary (PPT)

A complete visual overview of the workflow, results, and scientific motivation is available in:

📄 **MatterGen_MatterSim_Li-Cu-H.pptx**

This slide deck illustrates:
- Workflow diagram  
- Example MatterGen structures  
- MatterSim relaxations across pressures  
- ML convex hulls  
- DFT hull validation  
- Key findings  

---

# 🧭 Scientific Workflow Summary

This study follows a structured computational materials discovery pipeline:

### **1️⃣ Structure Generation (MatterGen)**  
~2000 Li–Cu–H structures generated with diverse stoichiometries and random atomic arrangements in POSCAR form.

### **2️⃣ ML Relaxation (MatterSim)**
Each generated structure was relaxed at pressures:



0, 5, 10, 12, 20, 40, 50, 75, 100 GPa


MatterSim (an ML potential trained on >5M structures) provided:
- relaxed atomic positions  
- enthalpy (E + PV)  
- stress tensor  
- per-atom formation enthalpy inputs  

Relaxed outputs → `outputs_hull_mattersim/`.

---

# 🧮 Formation Enthalpy Calculation

For each relaxed structure at pressure \(P\):

\[
\Delta H_f =
\frac{ H_\text{tot}(cell)
- \sum_i n_i \mu_i
- \sum_{X\in \text{diatomics}} (n_X/2) H_{X_2} }
{ N_\text{atoms} }
\]

Where:
- \(H_\text{tot} = E + PV\) (from MatterSim or VASP)
- \(\mu_i\) are monatomic energies from `elemental_licuh_energies_enthalpies.csv`
- \(H_{X_2}\) (e.g., H₂) provides consistent molecular reference states

---

# 🏔️ 3️⃣ ML Convex Hull Construction

For each pressure:
- The lowest-enthalpy structure at each composition is selected  
- A convex hull is constructed across the ternary space (Li–Cu–H)  
- Stable phases (ΔH = 0) and metastable phases (ΔH > 0) are identified  

Stored in:


outputs_hull_mattersim/<P>_GPa/


Example finding:
- At **0 GPa**, only **LiH** and **LiCu** are stable.  
- Above **50 GPa**, **ternary hydrides** begin to stabilize.

---

# 🧪 4️⃣ DFT Validation

MatterSim-predicted stable compounds were re-relaxed using **DFT (VASP)**.

A structure is accepted only if:
- SCF converged  
- Pressure satisfies:  
  \[
  |P_\text{actual} - P_\text{target}| < 1.5\ \text{GPa}
  \]
- Correct enthalpy extracted:
  - `enthalpy is TOTEN` for P > 0  
  - last `free energy TOTEN` for P = 0  

DFT hulls → `outputs_hull_dft/`.

---

# 🎯 5️⃣ ML vs DFT Cross-Validation

A direct comparison table:



outputs_hull_dft/DeltaH_comparison_0vs100GPa.csv


Findings:
- ML ≈ DFT at 0 GPa (excellent agreement)
- Minor deviations at 100 GPa, but **phase stability predictions match**
- ML is confirmed as a reliable screening filter

---

# 🔬 Key Scientific Insights

- **LiH** and **LiCu** dominate stability at ambient conditions  
- **High pressure (≥50 GPa)** stabilizes new ternary hydrides  
- **Cu–H bonding strengthens under compression**  
- ML predictions align closely with DFT results  
- The workflow is efficient and extensible to other ternary/ quaternary systems  

---

# 📘 Documentation

Full details can be found in:

- `docs/workflow_overview.md`  
- `docs/results_summary.md`  
- `docs/convex_hull_theory.md`  

---

# 📝 Notes

This repository is intended for:
- Presentation  
- Research communication  
- Portfolio demonstration  

Large raw datasets and simulation inputs are intentionally excluded for clarity.

For questions or collaboration, feel free to reach out.
