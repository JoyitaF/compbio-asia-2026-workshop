# 5. Introduction to Molecular Dynamics

**Source:** `CBA 26- MD Introduction.pptx`  
**Instructor:** Charlie Laughton.

The MD introduction framed molecular dynamics as a **computational microscope**. Many biologically important motions are too small, too fast, or too complex to observe directly in a single experimental snapshot. MD simulates atomistic motion using physics-based force fields.

The core MD loop is:

1. Start from coordinates.
2. Calculate energy and forces.
3. Move atoms a tiny time step forward.
4. Repeat millions to billions of times.
5. Analyze the resulting trajectory.

The session emphasized that MD is an experiment. A useful simulation needs:

- a clear scientific question,
- an appropriate starting structure,
- validated parameters,
- careful system setup,
- equilibration,
- controls/replicates,
- statistical analysis.

A crucial teaching was that **running MD is the least brain-intensive part**. The hard parts are experimental design, system preparation, and deciding whether the trajectory actually supports a conclusion.

Important concepts:

- **Force field:** mathematical model for bonded and nonbonded interactions.
- **Timestep:** usually femtoseconds; long biology requires many steps.
- **Solvation and ions:** simulations need a realistic environment.
- **Periodic boundary conditions:** the system is surrounded by copies of itself to mimic bulk solution or membrane.
- **Limitations:** practical MD is limited by atom count, timescale, and parameter accuracy.

See also: [`lectures/05-md-introduction.md`](lectures/05-md-introduction.md)
