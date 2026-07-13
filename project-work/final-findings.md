# Final Findings

Source: `A2A apo MD Slides.pptx`.

The project compared AF2 conformational ensembles, all-atom MD, GPCRmd reference behavior, and coarse-grained Martini simulations.

Key project-level findings summarized from the final A2A MD slides:

- AF2 conformations clustered around all-atom MD space, with some overlap against GPCRmd-like regions.
- All-atom MD runs explored quasi-stable clusters related to GPCRmd behavior.
- Coarse-grained Martini explored a concentrated local state space and appeared less able to escape local minima in this setup.
- ECL-focused PCA suggested overlapping but not identical exploration across replicas.
- Replicates 2 and 3 behaved more similarly, while replicate 1 explored a more distinct ECL2 region.

These results supported the project’s main framing: AF2/NMA may be useful as a fast exploratory proxy, but MD remains the stronger reference for dynamic interpretation.
