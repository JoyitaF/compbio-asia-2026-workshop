# Methods Summary

The workflow combined AlphaFold2/ColabFold conformational sampling, molecular dynamics, and trajectory/subspace analysis.

## Main components

- A2A receptor structure preparation.
- MSA-depth ladder for AF2/ColabFold model generation.
- Fresh all-atom MD setup and production runs.
- PCA of MD trajectories.
- ANM/NMA comparison against AF2 structures.
- RMSIP/subspace overlap, RMSF, endpoint coverage, and activation-descriptor analysis.

The expected behavior was non-monotonic: deep MSAs may collapse to a consensus conformation; extremely shallow MSAs may become noisy; intermediate depths may expose useful alternative conformations.
