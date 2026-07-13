# 3. Protein Structure Prediction and Modeling

**Source:** `Protein_structure_prediction.pdf`  
**Instructor:** Amitava Roy.

The structure-prediction session explained why prediction is needed: sequence databases contain vastly more proteins than the number of experimentally solved structures. Experimental methods such as X-ray crystallography, cryo-EM, and NMR remain essential, but they cannot cover the full sequence universe.

Three classical modeling routes were covered:

1. **Comparative / homology modeling:** use a known related structure as a template.
2. **Threading / fold recognition:** fit a sequence onto possible known folds even when sequence identity is low.
3. **Ab initio / de novo modeling:** predict structure from physical/statistical principles without a close template.

The practical modeling lesson was that “a model” is not automatically a structure. A model must be judged by template quality, sequence alignment quality, coverage, missing loops, side-chain placement, clashes, and the biological state represented. CASP and metrics such as GDT_TS were introduced as community benchmarks for prediction quality.

This prepared the ground for AlphaFold: AlphaFold is powerful, but the workshop treated it as part of a modeling ecosystem, not as a magical replacement for structural judgment.

See also: [`lectures/03-protein-structure-modeling.md`](lectures/03-protein-structure-modeling.md)
