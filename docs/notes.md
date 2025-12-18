# Notes & Reflections

This repository serves as a *scientific showcase* of my Li–Cu–H high-pressure hydrides workflow.

It intentionally avoids storing:

- large VASP data,
- intermediate MatterSim outputs,
- generated scripts.

Instead, I keep:

- final convex hull results,
- representative structures,
- PPT slides,
- documentation,
- a clean exposition of the methodology.

---

# Future Improvements (Personal Notes)

- Add phonons to verify dynamical stability.
- Check band structures of high-H-content hydrides.
- Explore Li–Cu–H–O quaternary space.
- Automate MatterGen → MatterSim → DFT selection via active learning.
- Create a pip-installable version of hull plotting utilities.

---

# Things I Learned

- ML potentials dramatically accelerate structure search.
- Pressure transforms bonding and composition landscapes.
- ΔH formation consistency is critical across ML ↔ DFT.
- python-ternary is powerful but requires careful axis mapping.
- Small pressure mismatches in VASP matter for enthalpy comparison.

