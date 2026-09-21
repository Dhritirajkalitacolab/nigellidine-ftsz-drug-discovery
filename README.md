# Nigellidine-FtsZ Structure-Based Drug Discovery

**Status:** In progress  
**Workflow:** ADMET and toxicity screening -> molecular docking and validation -> mammalian-tubulin selectivity counter-screen -> molecular dynamics -> energetic and experimental validation

A computational investigation of *Nigella sativa* alkaloids against *Staphylococcus aureus* FtsZ. The project follows the staged workflow recorded for the project: compounds are first screened for predicted drug-likeness and toxicity, then evaluated by validated docking, counter-screened against mammalian tubulin, and finally examined by a corrected 100 ns molecular-dynamics simulation.

> **Lead candidate:** Nigellidine  
> **Reserve candidates:** Nigellicine and Nigellimine  
> **Scope:** All current findings are computational predictions requiring experimental validation.

---

## Workflow

```text
Compound selection
        |
ADMET and toxicity screening
        |
Ligand and receptor preparation
        |
Molecular docking
        |
Native-ligand redocking validation
        |
Cross-method pose and ranking evaluation
        |
Mammalian-tubulin selectivity counter-screen
        |
Blind-docking reproducibility analysis
        |
Corrected 100 ns molecular dynamics
        |
Structural and interaction analyses
        |
MM-GBSA/MM-PBSA and experimental validation
```

---

## 1. ADMET and Toxicity Screening

| Compound | Predicted LD50 | Toxicity class | Carcinogenicity | Mutagenicity | Bioavailability score |
|---|---:|---:|---|---|---:|
| **Nigellidine** | 1000 mg/kg | 4 | Active, probability 0.52 | Inactive | 0.55 |
| Nigellicine | 1300 mg/kg | 4 | Active, probability 0.50 | Inactive | 0.85 |
| Nigellimine | 1300 mg/kg | **3** | Inactive | **Active, probability 0.78** | 0.55 |

All three compounds were recorded as passing the Lipinski, Ghose, Veber, Egan, and Muegge filters with zero evaluated rule violations and high predicted gastrointestinal absorption.

Nigellimine remains a reserve because of its predicted Class 3 toxicity and mutagenicity signal. Borderline carcinogenicity predictions for Nigellidine and Nigellicine are screening alerts, not confirmed biological outcomes.

> ADMET and toxicity-server outputs are model predictions. Experimental pharmacokinetic, cytotoxicity, genotoxicity, and toxicological testing remain necessary.

---

## 2. FtsZ Molecular Docking

### Target

```text
Target: Staphylococcus aureus FtsZ
PDB structure: 3VOA
Docking region: GTP/GDP-binding region
Lead ligand: Nigellidine
```

### Cross-method Nigellidine results

| Method | Result | Interpretation |
|---|---:|---|
| AutoDock Vina | -8.37 kcal/mol | Favorable predicted score |
| AutoDock4 | -7.25 kcal/mol | Lead ranking reproduced within this workflow |
| GNINA | -8.25 to -8.63 kcal/mol | CNN-assisted scoring supported favorable predicted binding |
| DiffDock-L | Consistent predicted pose | Independent pose prediction supported the consensus region |

Scores from different engines are not treated as directly interchangeable binding free energies because the engines use different search and scoring methods.

### Original AutoDock Vina screening

| Compound | Vina score |
|---|---:|
| GDP reference | -9.55 kcal/mol |
| **Nigellidine** | **-8.37 kcal/mol** |
| Nigellicine | -6.70 kcal/mol |
| Nigellimine | -6.14 kcal/mol |

Nigellidine ranked first among the three alkaloids. A later reproducibility run generated -8.4 kcal/mol for Nigellidine and approximately -9.5 kcal/mol for recreated GDP. These reruns support the rounded presentation values but do not replace the original results.

Ligand-efficiency values are omitted until the formula, heavy-atom counts, and calculation file are deposited.

### FtsZ validation

```text
Native ligand: GDP
Redocking RMSD: 0.307 A
Acceptance threshold: <2.0 A
Validation status: PASS
```

A later reconstructed GDP run is not treated as an exact reproduction of the original result because the original prepared receptor was unavailable and GDP was recreated.

---

## 3. Mammalian-Tubulin Selectivity Counter-Screen

Two workflows are reported separately because they used different structures, preparations, and validated methods.

### 3.1 1JFF workflow

| Method | Native-ligand redocking RMSD | Status |
|---|---:|---|
| AutoDock Vina | 2.68 A | Failed the predefined <2.0 A criterion |
| GNINA | 0.991 A | Passed |

Vina was excluded from the final 1JFF affinity comparison. GNINA was retained.

#### GNINA result under reconciliation

```text
Workflow record:      tubulin = -5.48 kcal/mol
Presentation Slide 2: tubulin = -6.33 kcal/mol
```

The presentation pairs -6.33 kcal/mol with FtsZ -8.63 kcal/mol, giving a 2.30 kcal/mol gap. The workflow record pairs -5.48 kcal/mol with FtsZ -8.25 to -8.63 kcal/mol, giving a 2.77 to 3.15 kcal/mol gap.

The original GNINA output files must be matched to their run provenance before either tubulin score is designated authoritative. Both records favor FtsZ, but no single exact GNINA selectivity gap is final yet.

### 3.2 4I55 workflow

PDB 4I55 contains bovine tubulin and is used as a mammalian-tubulin model, not described as a human structure.

#### Targeted AutoDock Vina

| Target | Nigellidine Mode 1 score |
|---|---:|
| FtsZ | -8.4 kcal/mol |
| 4I55 tubulin | -7.3 kcal/mol |
| Absolute gap | 1.1 kcal/mol |

The 1.1 kcal/mol difference is close to typical docking-score uncertainty and is therefore insufficient by itself to establish selectivity.

#### 4I55 validation status

```text
Documented GDP-redocking RMSD: 0.235 A
Acceptance threshold: <2.0 A
Recorded status: PASS
```

The 0.235 A value remains labelled **documented** until independently recalculated from the deposited crystal and redocked GDP coordinates.

---

## 4. Blind-Docking Reproducibility

Two independent blind runs were compared using the top-ranked Mode 1 pose and the same 22 Nigellidine heavy atoms. Hydrogen atoms were excluded.

| Target | Run 1 | Run 2 | Verified spatial result |
|---|---:|---:|---|
| FtsZ | -8.4 kcal/mol | -8.4 kcal/mol | Direct heavy-atom RMSD: **0.006 A** |
| 4I55 tubulin | -7.8 kcal/mol | -8.0 kcal/mol | Mode 1 centroid separation: **59.90 A** |

### FtsZ calculation

```text
Run 1 centroid: (3.740182, -7.473409, 19.799591) A
Run 2 centroid: (3.742227, -7.478091, 19.800500) A
Centroid separation:    0.005189 A
Direct heavy-atom RMSD: 0.006453 A
Fitted heavy-atom RMSD: 0.001108 A
```

The previously recorded 0.015 A value was not reproduced. The actual Mode 1 coordinates support 0.006 A direct heavy-atom RMSD.

### Tubulin calculation

```text
Run 1 centroid: (4.325409, 44.384727, 15.580182) A
Run 2 centroid: (30.730500, 3.497545, -19.329318) A
Centroid separation:    59.897109 A
Direct heavy-atom RMSD: 59.971850 A
Fitted heavy-atom RMSD: 0.149337 A
```

The low fitted RMSD means the ligand retained a similar internal shape after superposition. The approximately 59.90 A centroid separation means the two top poses occupied different receptor locations.

The evaluated runs therefore show stronger blind-pose spatial reproducibility for FtsZ. This does not prove that Nigellidine cannot bind tubulin or that no tubulin-binding site exists.

---

## 5. Corrected 100 ns Molecular Dynamics

### Preparation correction

The first production setup retained co-crystallized GDP alongside Nigellidine. An approximately 28 A ligand-coordinate offset was traced to using an unposed CGenFF structure instead of the validated docked coordinates.

The corrected workflow:

1. Recovered the validated docked Nigellidine pose
2. Applied rigid-body Kabsch alignment
3. Removed GDP
4. Rebuilt the GDP-free FtsZ-Nigellidine complex
5. Repeated preparation and equilibration
6. Repeated the full 100 ns production simulation
7. Performed analyses on the corrected trajectory

The corrected system is described as **GDP-free**, not apo, because Nigellidine remained present.

### Results

| Metric | Finding |
|---|---|
| Protein backbone RMSD | Approximately 0.196 nm during the first 10 ns and 0.267 nm during the final 10 ns; remained below approximately 0.3 nm |
| Radius of gyration | Mean 1.985 nm; range 1.952-2.029 nm; first-versus-final 10 ns difference approximately 0.004 nm |
| Ligand behavior | Initial adjustment at 0-15 ns; plateau at 15-45 ns; transition at 45-50 ns; second plateau at 50-95 ns; additional movement near 95-100 ns |
| Ligand-to-pocket distance | Generally 0.4-0.6 nm for approximately 85 ns after the initial adjustment |
| Ligand per-atom RMSF | Most atoms below 0.04 nm; terminal methyl hydrogens approximately 0.10-0.11 nm |
| Phe183 occupancy | 94.50% |
| Gly22 occupancy | 85.92% |
| Gly104 occupancy | 82.31% |
| Gly21 occupancy | 80.11% |
| Arg29 occupancy | 73.58% |
| Hydrogen bonding | Mean 0.15 hydrogen bonds per frame |

RMSD and radius of gyration together support overall structural stability, but do not prove that every local region remained unchanged.

The ligand-to-pocket distance supports retention near the selected pocket during most of the trajectory, but does not imply one unchanged atom-level orientation.

Contact occupancy used a 0.4 nm cutoff. Simulation-contact residues should not automatically be interpreted as crystallographic GDP-contact residues. Residue identities, especially residue 105, require verification against the final topology.

The low hydrogen-bond count shows that persistent hydrogen bonding was uncommon. MM-GBSA/MM-PBSA or another energy-decomposition method is required before assigning energetic dominance to hydrophobic or van der Waals forces.

> The observed transitions are supported by one 100 ns trajectory. Independent replicates are required.

---

## Current Interpretation

The computational evidence supports Nigellidine as the lead among the three screened alkaloids, favorable predicted FtsZ docking, reproducible FtsZ blind poses, overall structural stability during the corrected MD trajectory, and predicted drug-like properties.

The evidence does not establish experimental FtsZ inhibition, antibacterial activity, mammalian selectivity, clinical efficacy, or therapeutic safety.

---

## Open Work

- [ ] Reconcile the -5.48 and -6.33 kcal/mol GNINA tubulin records
- [ ] Recalculate the documented 4I55 GDP-redocking RMSD
- [ ] Verify MD residue identities, especially residue 105
- [ ] Run MM-GBSA or MM-PBSA
- [ ] Run independent MD replicates
- [ ] Complete statistical replicate comparison
- [ ] Complete protein-ligand interaction mapping
- [ ] Perform FtsZ polymerization and GTPase assays
- [ ] Determine *S. aureus*/MRSA MIC
- [ ] Perform mammalian-cell cytotoxicity and tubulin counter-assays
- [ ] Complete manuscript Results and Discussion

---

## Repository Structure

```text
.
|-- structures/
|   |-- ftsz/
|   |-- tubulin/
|   `-- ligands/
|-- docking/
|   |-- ftsz/
|   |-- tubulin/
|   `-- gnina/
|-- analysis/
|   |-- admet/
|   |-- selectivity/
|   |-- md/
|   `-- interactions/
|-- scripts/
|-- figures/
|-- presentation/
|-- documentation/
|-- environment/
|-- README.md
|-- LICENSE
|-- CITATION.cff
`-- .gitignore
```

Only files actually deposited should be represented as available.

---

## Large-File Policy

The repository excludes large production files:

```text
*.xtc
*.trr
*.tpr
*.edr
*.cpt
```

Large simulation data may be archived separately through Zenodo, Figshare, the Open Science Framework, or an institutional repository, with a persistent DOI or archive link added here.

---

## Software Stack

- **ADMET/toxicity:** SwissADME, ProTox-3.0
- **Docking:** AutoDock Vina, AutoDock4, GNINA, DiffDock-L
- **Preparation:** AutoDockTools/MGLTools, Open Babel
- **Molecular dynamics:** GROMACS, CHARMM36, TIP3P
- **Visualization:** VMD, UCSF ChimeraX

Exact versions should be recorded in `environment/software_versions.txt`.

---

## Responsible Interpretation

This is an ongoing, hypothesis-generating computational project. Nigellidine is not claimed to be a confirmed FtsZ inhibitor, experimentally antibacterial, selective in humans, clinically effective, therapeutically safe, or ready for human or animal use.

---

## Project Status

```text
ADMET screening:               Complete
Compound prioritization:       Complete
FtsZ molecular docking:        Complete
FtsZ redocking validation:     Complete
1JFF tubulin counter-screen:   Complete; GNINA score reconciliation pending
4I55 tubulin counter-screen:   Complete
Blind-docking comparison:      Complete
Corrected 100 ns MD:           Complete
Core MD analysis:              Complete
MM-GBSA/MM-PBSA:               Pending
MD replicates:                 Pending
Experimental validation:      Pending
Manuscript preparation:        In progress
```

---

## Citation and Use

Repository citation metadata should be provided in `CITATION.cff`. Cite the repository, PDB entries 3VOA, 1JFF, and 4I55, and the original publications for all software, force fields, databases, and web predictors used.

**Research and academic use only.** Repository publication, redistribution, and reuse remain subject to institutional requirements, software and database licences, and project-supervisor requirements.
