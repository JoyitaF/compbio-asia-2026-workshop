# CompBio Asia 2026 Workshop Summary

**Program:** CompBio Asia 2026  
**Location:** National University of Singapore, Singapore  
**Dates:** 14–27 June 2026  
**Focus:** cross-disciplinary computational biology training for graduate students, spanning protein structure, molecular dynamics, sequence annotation, neural networks, AlphaFold, docking, representation learning, quantum computing, and a final group project.

This summary is organized by session/resource. For each topic, it records the practical teaching: what the session was trying to teach, the key concepts, what the tools were for, and how the topic connected to the final A2A receptor molecular-dynamics project.

---

## 1. Computing Environment and Cyberinfrastructure

**Source:** `0615-02-CompBioAsia2025_compute_environment.pptx`  
**Date indicated by filename:** 15 June 2026  
**Instructor / credit shown:** Travis Wheeler; material also credited to Michele Cosi.

The computing-environment session explained the basic workshop infrastructure: instead of requiring every participant to install complicated scientific software locally, the workshop provided remote machines with software already installed. Participants only needed to log in and work in the provided environment.

The practical teaching was not just “use the server.” It introduced the difference between local laptops, remote virtual machines, HPC/supercomputer resources, CPUs, GPUs, and persistent storage. A key lesson was that computation in biology is often limited by environment management before it is limited by algorithms. If Python packages, GPU drivers, molecular simulation packages, or database paths are broken, the science cannot even start.

Important practical ideas:

- **SSH:** a secure way to log into a remote machine from your own computer.
- **Persistent storage:** a directory that keeps your files even if the temporary compute environment disappears.
- **Ephemeral systems:** compute sessions that may reset; files stored only there can vanish.
- **Symlink:** a symbolic link is like a shortcut or alias from one filesystem location to another. The workshop example used a command like `ln -s /data/user_dirs/[your_name] ~/my_files`, which creates `~/my_files` as a convenient pointer to a persistent directory.
- **Jupyter/CACAO-style managed environments:** participants could open notebooks without manually installing every dependency.

This mattered later because molecular dynamics and AlphaFold workflows produce many large files, and a small path mistake can break a pipeline. The same logic applies to cluster work: keep raw inputs, outputs, scripts, and analysis results in durable locations.

See also: [`lectures/01-computing-environment.md`](lectures/01-computing-environment.md)

---

## 2. Protein Structure Overview

**Source:** `Protein_structure_overview.pdf`  
**Instructor:** Amitava Roy.

This session built the conceptual foundation for structural biology. The core chain was:

```text
DNA → RNA → Protein sequence → Protein structure → Biological function
```

The session distinguished **configuration** and **conformation**. Configuration refers to fixed chemical connectivity or stereochemistry that cannot change without breaking bonds. Conformation refers to different spatial arrangements available through rotations and molecular motion. This distinction matters in MD because simulations are primarily exploring conformational change, not changing the underlying covalent chemistry.

Key teachings:

- Proteins are polymers made from amino acids.
- Amino acid properties influence folding, secondary structure, interfaces, and binding.
- Protein structure is described at multiple levels: primary sequence, secondary structure, tertiary fold, and quaternary assembly.
- Structure is stabilized by many interactions: hydrogen bonds, electrostatics, hydrophobic packing, van der Waals interactions, and sometimes disulfide bonds or metal coordination.
- Biological function depends on shape, dynamics, and interaction surfaces, not just sequence.

This session gave the vocabulary needed for later AlphaFold, docking, and MD lectures.

See also: [`lectures/02-protein-structure-overview.md`](lectures/02-protein-structure-overview.md)

---

## 3. Protein Structure Prediction and Modeling

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

---

## 4. PDBe and AlphaFold Database

**Source:** `Introduction of the PDBe and AFDB.pdf`  
**Date shown:** 16 June 2026  
**Instructor:** Maxim Tsenkov.

The PDBe/AFDB session taught how to evaluate structural data. A PDB entry is not simply “the truth”; it is an interpretation of experimental data. The session emphasized checking:

- experimental method,
- resolution,
- missing residues or loops,
- clashes,
- water and ligand treatment,
- biological assembly,
- conformation/state,
- whether the structure matches the biological question.

The AlphaFold Database was presented as a large-scale source of predicted structures. Its strength is broad coverage; its limitation is that predicted models need confidence interpretation and may not represent all functional states.

For the A2A project, this mattered directly: choosing inactive, active, and intermediate GPCR structures requires checking whether loops, fusions, mutations, ligands, and sodium/water molecules should be retained or removed.

See also: [`lectures/04-pdbe-afdb.md`](lectures/04-pdbe-afdb.md)

---

## 5. Introduction to Molecular Dynamics

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

---

## 6. ChimeraX Visualization and Movie Workflows

**Sources:** `ChimeraX_user_interface.pdf`, `ChimeraX_image_command_line.pdf`, `ChimeraX Tutorial selection and script.pdf`, `ChimeraX_movie_custom.pdf`.

The ChimeraX materials taught structure visualization as an analysis tool, not just a figure-making tool. Participants learned to open structures, select chains/residues, color by properties, control views, and save reproducible commands.

The movie tutorial showed how to build a custom molecular video by:

- opening a structure,
- setting visual style and background,
- coloring the model,
- defining saved views,
- recording frames,
- interpolating between views with `fly`,
- adding rotation/crossfade effects,
- encoding the final movie.

The deeper lesson is reproducibility: if visualization is done through commands/scripts instead of only clicking around, the figure or video can be regenerated and adjusted consistently.

In the final project, ChimeraX was useful for inspecting receptor conformations, checking missing loops, coloring pLDDT/PAE-related confidence, and preparing visual explanations of PCA/cluster results.

See also: [`lectures/06-chimerax.md`](lectures/06-chimerax.md)

---

## 7. Sequence Annotation

**Source:** `0616-CompBioAsia2026_annotation.pptx`  
**Date indicated by filename:** 16 June 2026.

The sequence-annotation session explained how we go from raw sequence data to biological meaning. The central question was: once we have a genome or metagenome assembly, how do we identify genes and infer what they do?

Important teachings:

- Bacterial and eukaryotic genomes have different annotation challenges.
- ORFs can be detected using start/stop codons, but longest ORF is only a heuristic.
- Introns, repeats, pseudogenes, and alternative splicing complicate eukaryotic annotation.
- Metagenomic assembly is harder because reads come from mixed organisms.
- Binning can group contigs into MAGs, but MAGs are still reconstructed approximations.
- Functional annotation often uses enzyme families, KEGG, KOfam, and pathway databases.
- Transposable elements are mobile DNA sequences; they complicate assembly and gene prediction.

The teaching was useful beyond genomics because it showed a recurring computational biology theme: raw data is not knowledge. Each annotation step makes assumptions, and those assumptions need validation.

See also: [`lectures/07-sequence-annotation.md`](lectures/07-sequence-annotation.md)

---

## 8. Neural Networks Intro

**Source:** `0617-01-NeuralNetworks_Intro.pdf`  
**Date indicated by filename:** 17 June 2026  
**Instructor:** Travis Wheeler.

The neural-networks lecture built intuition from the simplest idea: a function maps inputs to outputs. A lookup table can map known inputs to known outputs, but it fails when inputs are large, continuous, or unseen. Neural networks learn a flexible function from data.

Key teachings:

- Inputs can be vectors, images, sequences, or tensors.
- Weights determine how input features influence later representations.
- Hidden layers transform input into intermediate representations.
- Activation functions introduce nonlinearity.
- Logits are raw output scores.
- Softmax converts logits into class probabilities.
- Training adjusts weights so predictions better match labels.

The MNIST example gave an intuitive bridge from vectors to probabilities. This foundation was later reused in CNNs, protein language models, and representation learning for drug discovery.

See also: [`lectures/08-neural-networks.md`](lectures/08-neural-networks.md)

---

## 9. Neural-Network Hands-on Concepts

**Source:** `NNs-handson-a-few-slides.pptx`.

The hands-on neural-network slides explained the mechanical building blocks:

- **Tensor:** multidimensional array used to store model inputs, parameters, and outputs.
- **Neuron:** computes weighted input sum plus bias.
- **Activation:** transforms the neuron output; ReLU, sigmoid, and tanh were examples.
- **Softmax:** turns scores into probabilities.
- **Loss:** numerical penalty for wrong predictions.
- **One-hot encoding:** represents class labels as vectors.

This was important because later biological ML models use the same vocabulary even when the inputs are protein sequences, graphs, or molecular structures.

See also: [`lectures/08-neural-networks.md`](lectures/08-neural-networks.md)

---

## 10. CNNs for Protein Secondary Structure

**Source:** `SecondaryStructure_neural-networks.pptx`.

The CNN session used protein secondary-structure prediction as a concrete biological ML problem. Given an amino-acid sequence, the model predicts a local structural class for each residue.

Key teachings:

- Protein sequence can be represented as an array of residue-level features.
- Labels can be Q8 secondary-structure classes.
- Datasets such as CullPDB and CB513 provide training/evaluation examples.
- Class imbalance matters because some structural states are more common than others.
- A one-dimensional convolution scans along a sequence window and learns local motifs.
- Kernels, input channels, and output channels are the basic CNN mechanics.

The session connected model architecture to biological locality: secondary structure is strongly influenced by nearby sequence context, so convolution is a natural first approach.

See also: [`lectures/09-cnns-secondary-structure.md`](lectures/09-cnns-secondary-structure.md)

---

## 11. LLMs and Protein Language Models

**Source:** `LLMs_and_PLMs.pdf`.

This session explained language models through prediction tasks. Text LLMs learn from token sequences, often by predicting the next token. Protein language models adapt the idea to amino-acid sequences, often using masked-language modeling: hide amino acids and train the model to predict them from context.

Important teachings:

- Tokens can be words, subwords, or amino acids.
- Embeddings convert discrete tokens into numerical vectors.
- Attention allows the model to learn which other positions matter for representing a token.
- Protein embeddings can capture functional, structural, and evolutionary information.
- Protein models can support mutation-effect prediction through likelihood changes.
- Embeddings are not the same as alignment or phylogeny, but they can encode related information.

For computational biology, this reframed sequences as learnable objects: models can learn patterns from millions of proteins even before solving a specific downstream task.

See also: [`lectures/10-llms-plms.md`](lectures/10-llms-plms.md)

---

## 12. AlphaFold2

**Source:** `introduction_to_alphafold.pdf`.

The AlphaFold2 session taught what AF2 predicts and how to read its confidence metrics.

Core points:

- AF2 predicts 3D protein structure from sequence and evolutionary information.
- It is strong for many well-folded protein domains.
- It does not directly predict dynamics, ligand binding, protonation, allosteric pathways, or every biologically relevant conformation.
- Confidence must be interpreted residue-by-residue and domain-by-domain.

Key metrics:

- **pLDDT:** local confidence score per residue.
- **PAE:** predicted aligned error; useful for domain orientation uncertainty.
- **pTM:** global fold/topology confidence.
- **ipTM:** confidence for predicted interfaces in complexes.

The workshop emphasized that low pLDDT often corresponds to flexible, disordered, or uncertain regions, not necessarily “bad biology.” For GPCRs, loops may be both functionally important and difficult to predict.

See also: [`lectures/11-alphafold2.md`](lectures/11-alphafold2.md)

---

## 13. AlphaFold3

**Source:** `introduction_to_alphafold3.pdf`.

The AlphaFold3 session compared AF2 and AF3. AF3 extends the modeling scope to broader biomolecular complexes, using a newer architecture and diffusion-based coordinate generation.

Important teachings:

- AF2 heavily used Evoformer-style sequence/pair processing and IPA for structure generation.
- AF3 reduces/changes the MSA role and uses Pairformer-style representations.
- AF3 can model broader interaction systems, but it still has limitations.
- A key lesson was that MSA provides a signal, not a mechanism. Evolutionary covariance helps prediction but is not itself a physical simulation.
- AF3 can hallucinate, mishandle certain chemistry, show clashes/chirality issues, and still does not capture dynamics as MD does.

For the final project, this distinction mattered because the research question was not “can AlphaFold make one good receptor model?” It was “can AF2 MSA-depth ensembles approximate a dynamic conformational subspace?”

See also: [`lectures/12-alphafold3.md`](lectures/12-alphafold3.md)

---

## 14. Hands-on AlphaFold: MCT1

**Source:** `CompBio Hands-on AlphaFold.pdf`.

The AlphaFold hands-on session used MCT1 to teach practical prediction and interpretation. Participants compared UniProt, PDBe-KB, AlphaFold predictions, structural templates, Foldseek matches, and ColabFold custom predictions.

Key practical choices:

- number of recycles,
- MSA depth,
- whether to use templates,
- how to compare predicted and experimental structures,
- how to interpret pLDDT and PAE,
- how to use Foldseek to find structural analogs.

The important teaching was that prediction settings can alter the model state. Shallow MSA and template use can bias a prediction toward alternative conformations. This directly connects to the final A2A project, which explored MSA-depth variation as a way to generate conformational diversity.

See also: [`lectures/13-hands-on-alphafold.md`](lectures/13-hands-on-alphafold.md)

---

## 15. Molecular-Dynamics Analysis

**Source:** `CBA 26- Analysis of MD data.pptx`  
**Instructor:** Charlie Laughton.

The MD analysis lecture taught how to interpret trajectories. A trajectory is a time series of coordinates, but the scientific question is usually about ensembles, states, transitions, stability, and sampling.

Major teachings:

- MD samples a Boltzmann-weighted ensemble only if it samples sufficiently.
- A single trajectory can get trapped in one region of conformational space.
- Replicas are useful because stochastic simulations may explore different states.
- Equilibration must be separated from production analysis.
- Stability of state proportions is more important than arbitrary time length.
- Clustering and PCA can reveal major modes of motion.

PCA was framed as a way to project high-dimensional atomic motion onto a few collective coordinates. For proteins, this can show whether trajectories occupy overlapping or distinct conformational regions.

The most important scientific lesson was that there is no universal answer to “is the simulation long enough?” You can only judge after analysis.

See also: [`lectures/14-md-analysis.md`](lectures/14-md-analysis.md)

---

## 16. CPPTRAJ Practical Analysis

**Source:** `Steps for analysis using CPPTRAJ.pdf`.

The CPPTRAJ practical translated MD analysis into commands. The workflow included cloning/copying analysis scripts, making shell scripts executable, running movie/RMSD workflows, inspecting CSV output, copying files locally, plotting RMSD, and opening trajectories in ChimeraX.

Important workflow names mentioned in the guide:

- `movie.sh`: referenced as the command/script used for trajectory movie workflow.
- `rmsd.sh`: referenced as the command/script used for RMSD analysis.
- `smooth_md.py`: referenced for ChimeraX trajectory visualization.
- CSV outputs: used for plotting RMSD and checking simulation behavior.

These names are kept in the summary because they were part of the practical instructions, but they are not listed as required upload files unless you have the actual script files separately.

The lesson was that analysis needs repeatable scripts. Manual visualization is useful, but quantitative claims require saved, rerunnable workflows.

See also: [`lectures/15-cpptraj-practical.md`](lectures/15-cpptraj-practical.md)

---

## 17. AMBER System Setup and Equilibration Files

**Sources:** `Tleap script explanation.pdf`, `Overall steps to accomplish equilibration.pdf`, `prmtop explanation.pdf`, `inpcrd file explanation.pdf`, `step9.rst7 explanation.pdf`, `prod_in description.pdf`.

These AMBER materials taught what simulation input files mean.

### `tleap` workflow

`tLeap` builds the system topology and coordinates. It loads force fields, ligand parameters, protein structures, water models, ions, and saves AMBER files.

Key ideas:

- `ff19SB`: protein force field.
- `GAFF2`: general force field for small molecules/ligands.
- `.frcmod`: missing or modified parameter file.
- `.mol2`: ligand structure with atom names/types/charges.
- `solvateoct`: creates a solvated box.
- ions: neutralize and set salt concentration.
- `saveamberparm`: writes `.prmtop` and `.inpcrd`.

### `prmtop`

The topology file. It stores atom types, charges, masses, bonds, angles, dihedrals, residue definitions, and nonbonded parameters. Coordinates alone are not enough; the engine needs topology to know what atoms are and how they interact.

### `inpcrd`

The input coordinate file. It stores starting atomic positions and box information. It is paired with `prmtop`.

### `step9.rst7`

A restart/coordinate file after equilibration. It can be used as the starting point for production MD.

### `prod.in`

The production input file. It controls production MD settings such as restart behavior, timestep, number of steps, thermostat/barostat settings, output intervals, restraints, and wrapping.

### Overall equilibration

The tutorial used commands such as cloning the MD workflow, moving `.prmtop`/`.inpcrd`, using `tmux`, running equilibration, and beginning production from `step9.rst7`. Hydrogen mass repartitioning was introduced as a way to permit a larger timestep in some MD setups.

See also: [`lectures/16-amber-setup-equilibration.md`](lectures/16-amber-setup-equilibration.md)

---

## 18. Docking

**Source:** `Introduction_to_Docking.pdf`  
**Instructor:** Amitava Roy.

The docking lecture introduced ligand-protein docking as prediction of binding poses and approximate binding scores. AutoDock Vina and AutoDock4-style ideas were discussed.

Important teachings:

- Docking searches ligand position, orientation, and rotatable bonds.
- The scoring function approximates interaction favorability.
- Exhaustiveness and number of modes affect search thoroughness.
- Grid-based methods precompute receptor interaction fields.
- Docking is useful for pose generation and virtual screening, but scores are approximate.
- Docking cannot replace experimental validation or careful MD/free-energy analysis.

For MD projects, docking can generate starting ligand poses when experimental complexes are unavailable, but the resulting poses need scrutiny.

See also: [`lectures/17-docking.md`](lectures/17-docking.md)

---

## 19. Representation Learning for Drug Discovery

**Source:** `Representation-learning-drug-discovery.pptx`  
**Instructor:** Travis Wheeler.

This lecture connected modern ML representation learning to drug discovery. The key idea is that models can learn embeddings that capture meaningful context and similarity.

Important teachings:

- Representations can encode molecules, pockets, proteins, or complexes.
- Contrastive learning can make related objects close in embedding space and unrelated objects far apart.
- Protein-ligand complexes can be represented as graphs.
- Graph neural networks can model atoms as nodes and bonds/interactions as edges.
- Virtual screening by brute-force docking can be extremely expensive at large library scale.
- Learned representations may help prioritize candidates before expensive docking or simulation.

This connected the AI part of the workshop to structure-based drug discovery.

See also: [`lectures/18-representation-learning-drug-discovery.md`](lectures/18-representation-learning-drug-discovery.md)

---

## 20. Quantum Computing Meets AI for Biology

**Sources:** `Compbioasia Day 1.pdf`, `Quantum Computing In AI for Biology workshop#1.pdf`, `Qdocking_vls_nus - Compbioasia.ppsm`, `qdock_kaiwu_colab.ipynb`.

The quantum sessions introduced quantum/Ising-inspired computing as an approach to difficult sampling and optimization problems in complex systems.

Important teachings:

- Biological systems are nonlinear, multiscale, and complex.
- Standard data-driven AI can struggle when data is sparse, biased, or disconnected from physical laws.
- Quantum or quantum-inspired machines can be framed around sampling and optimization.
- The Kaiwu SDK/KPP workflow exposed QUBO/Ising formulations through Python.
- Boltzmann machines and quantum Boltzmann machines connect energy landscapes to probability distributions.
- “Sample mode” and “optimization mode” serve different purposes.

The quantum docking material connected these ideas to virtual ligand screening and molecular search, although the exact technical depth depends on the notebook and PPSM source files.

See also: [`lectures/19-quantum-computing.md`](lectures/19-quantum-computing.md)

---

## 21. Resource Hub

**Source:** `CompBio26 resources hub`.

The resource hub collected workshop tools, GitHub pages, databases, applications, and training materials. These are grouped in this repository under [`tools-and-resources/`](tools-and-resources/).

Major categories:

- molecular dynamics preparation and analysis,
- OpenMM and AMBER/CPPTRAJ-style workflows,
- AlphaFold/ColabFold and structure prediction,
- protein databases and annotation platforms,
- protein language models and AI explainers,
- docking and interaction scoring,
- quantum computing resources,
- general ML and neural-network training materials.

See also: [`tools-and-resources/README.md`](tools-and-resources/README.md)

---

## 22. Final Project: A2A Receptor MD and AF2 MSA-Depth Ensembles

**Project materials used for this summary:** `A2A apo MD Slides.pptx`, `project outline and rationale`, `protocol tracking document.docx`, `delegation`.

`CompBioprojectpitch.pptx` is intentionally not part of the upload map for this GitHub version, because this repo is organized around the workshop learning record and the final A2A MD project summary rather than an early project-pitch artifact.

The final group project focused on the human adenosine A2A receptor, a GPCR. The core scientific question was:

> Can AlphaFold2 structures generated under different MSA-depth settings, combined with normal-mode analysis, recover the conformational subspace sampled by molecular dynamics?

The project motivation came from a tension in modern structural biology:

- AlphaFold can predict highly accurate static structures.
- Receptor function depends on motion and conformational transitions.
- Molecular dynamics can sample motion but is expensive.
- Normal-mode analysis is cheap but approximate.
- Shallow MSA strategies may coax AlphaFold into alternative plausible conformations.

The project proposed a systematic test using a GPCR model system. It compared AF2 conformational ensembles across MSA depths against MD-derived motion. The idea was not simply to make many AF2 structures, but to ask whether their differences align with meaningful dynamic modes.

Planned/used readouts included:

- PCA of MD trajectories,
- ANM/NMA modes from AF2 structures,
- RMSIP/subspace overlap,
- RMSF comparison,
- endpoint coverage,
- activation descriptors such as TM3–TM6 ionic-lock distance and NPxxY-related features,
- compute-cost comparison.

The project had a clear “sweet spot” hypothesis: agreement between AF2/NMA and MD may be non-monotonic with MSA depth. Very deep MSA may collapse to one confident consensus state; extremely shallow MSA may become noisy; intermediate/shallow depths may expose useful alternative conformations.

See also:

- [`project-work/a2a-project-summary.md`](project-work/a2a-project-summary.md)
- [`project-work/methods-summary.md`](project-work/methods-summary.md)
- [`project-work/collaborator-roles.md`](project-work/collaborator-roles.md)
- [`project-work/final-findings.md`](project-work/final-findings.md)
