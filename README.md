# Nigellidine–FtsZ Structure-Based Drug Discovery

**Status:** In progress  
**Workflows:** Molecular docking | Molecular dynamics | ADMET and toxicity | Mammalian-tubulin counter-screen

A computational investigation of *Nigella sativa* alkaloids against *Staphylococcus aureus* FtsZ, an essential bacterial cell-division protein. The project integrates validated molecular docking, a corrected 100 ns molecular-dynamics simulation, ADMET and toxicity profiling, and mammalian-tubulin counter-screening to evaluate predicted activity and preliminary selectivity.

> **Lead candidate:** Nigellidine  
> **Reserve candidates:** Nigellicine and Nigellimine  
> **Scope:** All current findings are computational predictions and require experimental validation.

---

## Project Objectives

1. Evaluate the predicted binding of *N. sativa* alkaloids to the FtsZ GTP/GDP-binding region.
2. Validate each trusted docking workflow through native-ligand redocking.
3. Compare Nigellidine binding against FtsZ and mammalian tubulin.
4. Assess the reproducibility of targeted and blind docking.
5. Examine the stability and positional behavior of the FtsZ–Nigellidine complex through 100 ns molecular dynamics.
6. Profile drug-likeness, bioavailability, and predicted toxicity.
7. Prioritize candidates for biochemical and microbiological validation.

---

## Scientific Rationale

### Why FtsZ?

FtsZ is a GTP-binding protein essential for bacterial cytokinesis. It polymerizes to form the Z-ring, which organizes the bacterial cell-division machinery. Inhibiting FtsZ may therefore prevent bacterial proliferation through a mechanism distinct from many conventional antibiotics.

FtsZ is structurally homologous to mammalian tubulin, particularly around the nucleotide-binding region. Selectivity cannot be assumed from the bacterial function of FtsZ and must instead be evaluated through direct counter-screening.

### Why *Nigella sativa* alkaloids?

The antibacterial activity of *N. sativa* is well documented but is attributed mainly to thymoquinone. The plant's alkaloid fraction remains comparatively under-investigated.

This project evaluates:

- **Nigellidine**, the primary lead
- **Nigellicine**, the first reserve candidate
- **Nigellimine**, the second reserve candidate

Nigellidine produced the most favorable AutoDock Vina score among the three alkaloids and was advanced to molecular-dynamics and selectivity analyses.

---

## Workflow Overview

```text
Compound selection
        ↓
Ligand and receptor preparation
        ↓
Native-ligand redocking validation
        ↓
Targeted and blind molecular docking
        ↓
Cross-method pose and ranking evaluation
        ↓
Mammalian-tubulin counter-screen
        ↓
Corrected 100 ns molecular dynamics
        ↓
Structural and interaction analyses
        ↓
ADMET and toxicity profiling
        ↓
MM-GBSA/MM-PBSA and experimental validation
```

---

## FtsZ Molecular Docking

### Target structure

```text
Target: Staphylococcus aureus FtsZ
PDB structure: 3VOA
Docking region: GTP/GDP-binding region
Lead ligand: Nigellidine
```

### Nigellidine docking results

| Method | Nigellidine result | Interpretation |
|---|---:|---|
| AutoDock Vina | −8.37 kcal/mol | Favorable predicted score |
| AutoDock4 | −7.25 kcal/mol | Lead ranking reproduced within this workflow |
| GNINA | −8.25 to −8.63 kcal/mol | CNN-assisted scoring supported favorable predicted binding |
| DiffDock-L | Consistent predicted pose | Independent pose prediction supported the consensus region |

Absolute values from different docking engines are not compared as though they share one energy scale. Each method uses a different search algorithm and scoring function. Cross-method agreement is therefore evaluated mainly through compound ranking and predicted-pose consistency.

### Original AutoDock Vina screening results

| Compound | Vina score |
|---|---:|
| GDP reference | −9.55 kcal/mol |
| **Nigellidine** | **−8.37 kcal/mol** |
| Nigellicine | −6.70 kcal/mol |
| Nigellimine | −6.14 kcal/mol |

Nigellidine ranked first among the three evaluated alkaloids.

The table reports the original screening values rounded to two decimal places. A later reproducibility run generated −8.4 kcal/mol for Nigellidine and approximately −9.5 kcal/mol for recreated GDP. The reruns support the rounded presentation values but do not replace the more precise original results.

Ligand-efficiency values are intentionally omitted from this README until the exact formula, heavy-atom counts, and calculation file are deposited.

---

## FtsZ Docking Validation

The FtsZ docking workflow was validated by redocking native GDP into its crystallographic binding region.

```text
Native ligand: GDP
Redocking RMSD: 0.307 Å
Acceptance threshold: <2.0 Å
Validation status: PASS
```

The low RMSD indicates that the validated setup reproduced the experimentally observed GDP pose accurately.

A later reconstructed GDP run produced a Mode 1 score of approximately −9.5 kcal/mol. This reconstructed run is not treated as an exact reproduction of the original −9.545 kcal/mol result because the original prepared receptor file was unavailable and the GDP ligand was recreated.

> Docking scores are screening estimates, not experimentally measured binding free energies.

---

## Mammalian-Tubulin Counter-Screen

Because FtsZ and tubulin are structural homologs, Nigellidine was counter-screened against the equivalent nucleotide-binding region of mammalian tubulin.

Two workflows were evaluated separately:

1. An initial 1JFF workflow using GNINA and AutoDock Vina
2. A subsequent higher-resolution 4I55 workflow using AutoDock Vina

The workflows used different structures, receptor preparations, and validated computational methods. Their scores are therefore reported separately rather than merged into one selectivity estimate.

---

## 1JFF Tubulin Workflow

### Native-ligand redocking

| Method | Redocking RMSD | Status |
|---|---:|---|
| AutoDock Vina | 2.68 Å | Failed the predefined <2.0 Å criterion |
| GNINA | 0.991 Å | Passed |

AutoDock Vina was excluded from the final 1JFF affinity comparison because native-ligand redocking failed the predefined validation criterion. GNINA passed and was therefore retained for the corresponding FtsZ-versus-tubulin comparison.

### GNINA result under reconciliation

The current project records contain two different reported tubulin GNINA scores:

```text
Workflow record:       −5.48 kcal/mol
Presentation Slide 2:  −6.33 kcal/mol
```

The presentation pairs −6.33 kcal/mol for tubulin with −8.63 kcal/mol for FtsZ, producing a 2.30 kcal/mol gap. The workflow record pairs −5.48 kcal/mol with an FtsZ range of −8.25 to −8.63 kcal/mol, producing a 2.77 to 3.15 kcal/mol gap.

The original GNINA output files must be reconciled before either tubulin value is designated as authoritative. Both records predict a less favorable tubulin score than the FtsZ score, but the precise GNINA score gap remains under verification.

> No single exact GNINA selectivity gap is treated as final in this repository until the original run provenance and output files are matched.

---

## 4I55 Tubulin Workflow

PDB 4I55 contains bovine tubulin and is used here as a mammalian-tubulin structural model. It is not described as a human tubulin structure.

### Targeted AutoDock Vina comparison

| Target | Nigellidine Mode 1 score |
|---|---:|
| FtsZ | −8.4 kcal/mol |
| 4I55 tubulin | −7.3 kcal/mol |
| Absolute score gap | 1.1 kcal/mol |

```text
|−8.4 − (−7.3)| = 1.1 kcal/mol
```

The 1.1 kcal/mol difference is close to the approximate uncertainty commonly associated with docking scores. Consequently, the targeted Vina comparison alone does not provide strong affinity-based evidence of selectivity.

### 4I55 redocking validation

The project record reports:

```text
Documented 4I55 GDP-redocking RMSD: 0.235 Å
Acceptance threshold: <2.0 Å
Recorded validation status: PASS
```

The corresponding input, output, and log files are included or planned for inclusion. The 0.235 Å value remains labelled **documented** until independently recalculated from the deposited crystal GDP and redocked GDP coordinates.

---

## Blind-Docking Reproducibility

Two independent blind-docking runs were compared for each target. Only the top-ranked Mode 1 pose from each independent run was used for the inter-run comparison.

### Calculation definitions

```text
Centroid separation:
Distance between the geometric centers of two Mode 1 ligand poses.

Direct heavy-atom RMSD:
Atom-by-atom RMSD in the unchanged receptor coordinate system.

Fitted heavy-atom RMSD:
RMSD after optimal translation and rotation of one pose onto the other.
```

Hydrogen atoms were excluded from the primary calculations. The same 22 Nigellidine heavy atoms were matched by atom order in each comparison.

### Verified results

| Target | Run 1 score | Run 2 score | Inter-run result |
|---|---:|---:|---|
| FtsZ | −8.4 kcal/mol | −8.4 kcal/mol | Direct heavy-atom RMSD: **0.006 Å** |
| 4I55 tubulin | −7.8 kcal/mol | −8.0 kcal/mol | Mode 1 centroid separation: **59.90 Å** |

### FtsZ Mode 1 comparison

```text
Run 1 centroid:
X = 3.740182 Å
Y = −7.473409 Å
Z = 19.799591 Å

Run 2 centroid:
X = 3.742227 Å
Y = −7.478091 Å
Z = 19.800500 Å

Centroid separation:      0.005189 Å
Direct heavy-atom RMSD:   0.006453 Å
Fitted heavy-atom RMSD:   0.001108 Å
```

The independently generated FtsZ Mode 1 poses were effectively identical. A previously recorded value of 0.015 Å was not reproduced from the deposited Mode 1 coordinates. The direct coordinate calculation supports **0.006 Å** as the inter-run heavy-atom RMSD.

### Tubulin Mode 1 comparison

```text
Run 1 centroid:
X = 4.325409 Å
Y = 44.384727 Å
Z = 15.580182 Å

Run 2 centroid:
X = 30.730500 Å
Y = 3.497545 Å
Z = −19.329318 Å

Centroid separation:      59.897109 Å
Direct heavy-atom RMSD:   59.971850 Å
Fitted heavy-atom RMSD:    0.149337 Å
```

The low fitted RMSD indicates that Nigellidine adopted a similar internal conformation after superposition. However, the approximately 59.90 Å centroid separation shows that the two top-ranked poses occupied completely different receptor locations.

### Interpretation

The independent FtsZ blind runs reproduced essentially the same predicted position and score. The independent 4I55 tubulin runs generated similarly scored top poses at widely separated positions.

This supports:

- Stronger blind-pose spatial reproducibility for FtsZ in the evaluated runs
- Poor top-pose spatial reproducibility across the two evaluated 4I55 tubulin runs

This result does not prove that Nigellidine cannot bind tubulin, nor does it prove the absence of all possible tubulin-binding sites. It shows only that these two independent blind runs did not converge on one top-ranked tubulin location.

---

## Overall Selectivity Interpretation

### Evidence supporting predicted FtsZ preference

- The retained GNINA records both report less favorable scores against tubulin than against FtsZ, although the exact tubulin value remains under reconciliation.
- Independent FtsZ blind runs reproduced the same Mode 1 pose with a direct heavy-atom RMSD of 0.006 Å.
- Independent 4I55 tubulin blind runs produced Mode 1 centroids approximately 59.90 Å apart.

### Evidence limiting the claim

- The targeted 4I55 Vina score gap was only 1.1 kcal/mol.
- A 1.1 kcal/mol gap is close to typical docking-score uncertainty.
- Different structures and methods produced different apparent selectivity magnitudes.
- The exact 1JFF GNINA tubulin score has not yet been reconciled from the original outputs.
- No experimental FtsZ or tubulin binding assay has been performed.

### Current conclusion

The combined computational results support stronger predicted binding-site reproducibility for FtsZ than for the evaluated mammalian-tubulin models. The validated GNINA records also favor FtsZ, but the exact GNINA score difference remains under verification.

The evidence does not establish experimental affinity, biological selectivity, clinical efficacy, or safety.

---

## Molecular Dynamics

### Identification and correction of a preparation error

The first production setup inadvertently retained co-crystallized GDP alongside Nigellidine. This did not represent a clean GDP-free FtsZ–Nigellidine system because GDP remained present in the nucleotide-binding region.

The problem was traced to an approximately 28 Å ligand-coordinate offset caused by using an unposed CGenFF ligand structure instead of the validated docked Nigellidine coordinates.

The correction involved:

1. Recovering the validated docked Nigellidine pose
2. Performing rigid-body Kabsch alignment
3. Removing GDP from the receptor system
4. Rebuilding the GDP-free FtsZ–Nigellidine complex
5. Repeating system preparation and equilibration
6. Repeating the complete 100 ns production simulation
7. Performing the reported analyses on the corrected trajectory

The corrected system is described as **GDP-free**, not apo, because Nigellidine remained present in complex with FtsZ.

---

## Corrected 100 ns MD Results

| Metric | Finding |
|---|---|
| Protein backbone RMSD | Mean approximately 0.196 nm during the first 10 ns and 0.267 nm during the final 10 ns; remained below approximately 0.3 nm |
| Radius of gyration | Mean 1.985 nm; observed range 1.952–2.029 nm; first-versus-final 10 ns difference approximately 0.004 nm |
| Ligand positional behavior | Initial adjustment at approximately 0–15 ns; first plateau at approximately 15–45 ns; transition at approximately 45–50 ns; second plateau at approximately 50–95 ns; additional movement near 95–100 ns |
| Ligand-to-pocket distance | After approximately 15 ns, generally remained around 0.4–0.6 nm for approximately 85 ns |
| Ligand per-atom RMSF | Most atoms remained below 0.04 nm; terminal methyl hydrogens reached approximately 0.10–0.11 nm |
| Phe183 contact occupancy | 94.50% |
| Gly22 contact occupancy | 85.92% |
| Gly104 contact occupancy | 82.31% |
| Gly21 contact occupancy | 80.11% |
| Arg29 contact occupancy | 73.58% |
| Hydrogen bonding | Mean 0.15 hydrogen bonds per frame |

### Protein stability

The backbone RMSD increased from an average of approximately 0.196 nm during the first 10 ns to approximately 0.267 nm during the final 10 ns. Together with the nearly constant radius of gyration, this supports overall structural stability without a large sustained change indicative of global structural disruption.

RMSD alone is not treated as proof that every local region remained unchanged.

### Ligand positional behavior

Nigellidine showed an initial adjustment during approximately 0–15 ns, followed by two main positional plateaus:

- **Plateau 1:** approximately 15–45 ns
- **Transition:** approximately 45–50 ns
- **Plateau 2:** approximately 50–95 ns
- **Final interval:** additional movement during approximately 95–100 ns

Because additional movement occurred during the final approximately 5 ns, the second positional state is not described as stable through the absolute end of the trajectory.

### Ligand-to-pocket distance

After the initial approximately 15 ns adjustment, the ligand-to-pocket-center distance generally remained around 0.4–0.6 nm for approximately 85 ns. This supports continued occupation near the selected pocket during most of the trajectory.

Distance to the pocket center confirms spatial retention near the selected site but does not, by itself, prove one unchanged atom-level binding orientation.

### Ligand internal flexibility

Most ligand atoms remained below approximately 0.04 nm RMSF, while terminal methyl hydrogens reached approximately 0.10–0.11 nm. This pattern indicates limited internal deformation of the ligand core with greater local mobility at terminal hydrogen atoms.

### Contact occupancy

Contact occupancy was calculated using a 0.4 nm cutoff. The strongest recorded contacts were:

```text
Phe183: 94.50%
Gly22:  85.92%
Gly104: 82.31%
Gly21:  80.11%
Arg29:  73.58%
```

These residues represent simulation contacts with Nigellidine. They should not all be interpreted automatically as crystallographic GDP-contact residues. Residue identities, particularly residue 105 in the presentation record, must be verified against the final topology and residue-number mapping before publication.

### Hydrogen bonding

The mean hydrogen-bond count of 0.15 per frame indicates that persistent hydrogen bonding was uncommon. High contact occupancies show sustained close-range contacts, but interaction-energy decomposition or MM-GBSA/MM-PBSA is required before assigning energetic dominance specifically to hydrophobic or van der Waals forces.

> The positional behavior is currently supported by one 100 ns trajectory. Independent MD replicates are needed to test whether the observed transitions are reproducible.

---

## ADMET and Toxicity Profiling

| Compound | Predicted LD50 | Toxicity class | Carcinogenicity | Mutagenicity | Bioavailability score |
|---|---:|---:|---|---|---:|
| **Nigellidine** | 1000 mg/kg | 4 | Active, probability 0.52 | Inactive | 0.55 |
| Nigellicine | 1300 mg/kg | 4 | Active, probability 0.50 | Inactive | 0.85 |
| Nigellimine | 1300 mg/kg | **3** | Inactive | **Active, probability 0.78** | 0.55 |

All three compounds were recorded as:

- Passing the Lipinski filter
- Passing the Ghose filter
- Passing the Veber filter
- Passing the Egan filter
- Passing the Muegge filter
- Producing zero violations in the evaluated drug-likeness rules
- Showing high predicted gastrointestinal absorption

Nigellimine remains a reserve rather than a co-lead because of its predicted Class 3 toxicity and strong predicted mutagenicity signal.

The borderline carcinogenicity predictions for Nigellidine and Nigellicine are treated as screening alerts, not confirmed biological outcomes.

> ADMET and toxicity-server outputs are model predictions. Experimental pharmacokinetic, cytotoxicity, genotoxicity, and toxicological testing remain necessary.

---

## Current Evidence

The current computational evidence supports:

- Nigellidine as the highest-ranked alkaloid among the three screened compounds in the original Vina workflow
- Favorable predicted FtsZ docking across multiple methods
- Successful native-ligand redocking in the trusted workflows
- Highly reproducible FtsZ blind-docking Mode 1 poses
- Poor top-pose reproducibility across the two evaluated 4I55 tubulin blind runs
- Overall structural stability of the corrected FtsZ–Nigellidine system during the 100 ns trajectory
- Spatial retention of Nigellidine near the selected pocket for most of the trajectory after the initial adjustment period
- Generally favorable predicted drug-likeness
- No predicted Nigellidine mutagenicity signal in the evaluated model

The evidence supports candidate prioritization. It does not constitute experimental proof of FtsZ inhibition, antibacterial activity, mammalian selectivity, clinical efficacy, or therapeutic safety.

---

## Open Work

- [ ] Reconcile the −5.48 and −6.33 kcal/mol tubulin GNINA records using the original output files
- [ ] Independently reproduce the documented 4I55 GDP-redocking RMSD of 0.235 Å
- [ ] Verify residue names against the final MD topology, especially residue 105
- [ ] MM-GBSA or MM-PBSA binding free-energy calculation
- [ ] Independent MD replicates
- [ ] Statistical comparison across replicate trajectories
- [ ] Final protein–ligand interaction map
- [ ] FtsZ polymerization assay
- [ ] FtsZ GTPase assay
- [ ] *S. aureus* or MRSA MIC determination
- [ ] Mammalian-cell cytotoxicity testing
- [ ] Experimental tubulin counter-assay
- [ ] Ligand-based machine-learning component, pending supervisor discussion
- [ ] Manuscript Results and Discussion sections

---

## Repository Structure

```text
.
├── structures/
│   ├── ftsz/
│   ├── tubulin/
│   └── ligands/
├── docking/
│   ├── ftsz/
│   │   ├── targeted/
│   │   ├── blind/
│   │   ├── validation/
│   │   └── autodock4/
│   ├── tubulin/
│   │   ├── targeted/
│   │   ├── blind/
│   │   ├── validation/
│   │   └── autodock4_excluded/
│   └── gnina/
├── analysis/
│   ├── selectivity/
│   ├── md/
│   ├── interactions/
│   └── admet/
├── scripts/
├── figures/
├── presentation/
├── documentation/
├── README.md
├── LICENSE
├── CITATION.cff
└── .gitignore
```

---

## Repository Contents

The repository is intended to include:

- Prepared receptor and ligand structures
- Docking configuration files
- Complete docking logs
- Ranked docking outputs
- Native-ligand redocking outputs
- Blind-docking reproducibility calculations
- GROMACS parameter files
- Compact MD analysis outputs
- ADMET and toxicity data
- Analysis scripts
- Figures and presentation materials
- Methodological and limitation records

Only files actually deposited in the repository should be represented as available.

---

## Large-File Policy

Large production simulation files are not stored directly in this repository:

```text
*.xtc
*.trr
*.tpr
*.edr
*.cpt
```

A 100 ns production trajectory may require several gigabytes and is not suitable for a normal source-code repository.

Large simulation data may be deposited separately through Zenodo, Figshare, the Open Science Framework, or an institutional repository. A persistent DOI or archive link will be added if such a deposition is made.

---

## Software Stack

### Molecular docking and pose prediction

- AutoDock Vina
- AutoDock4
- GNINA
- DiffDock-L
- AutoDockTools/MGLTools
- Open Babel

### Molecular dynamics and visualization

- GROMACS
- CHARMM36 force field
- TIP3P water model
- VMD
- UCSF ChimeraX

### ADMET and toxicity

- SwissADME
- ProTox-3.0

Exact software versions should be recorded in:

```text
environment/software_versions.txt
```

---

## Reproducibility

For each docking experiment, the repository should record:

- Receptor input
- Ligand input
- Search-box center
- Search-box dimensions
- Exhaustiveness
- Number of requested modes
- Random seed where available
- Complete docking log
- Ranked output poses
- Validation outcome
- Method-specific exclusions
- Known limitations

### Primary targeted Vina parameters

```text
FtsZ box center:
X = 5.144
Y = −9.937
Z = 26.791

Box dimensions:
25 × 25 × 25 Å

Exhaustiveness:
32

Number of modes:
9
```

### Blind-docking coordinate analysis

The deposited analysis script should:

1. Extract Mode 1 from each PDBQT file
2. Exclude hydrogen atoms
3. Match corresponding atoms
4. Calculate heavy-atom centroids
5. Calculate centroid separation
6. Calculate direct heavy-atom RMSD
7. Calculate fitted RMSD after optimal superposition
8. Export the results to CSV

---

## Method Exclusions and Limitations

### 1JFF AutoDock Vina

The 1JFF Vina workflow was excluded from the corresponding affinity comparison because the GDP-redocking RMSD was 2.68 Å, exceeding the predefined 2.0 Å threshold.

### 4I55 AutoDock4

The 4I55 AutoDock4 workflow was excluded from the final tubulin comparison after GDP redocking failed with an RMSD of approximately 8.07 Å.

A separate EPDB evaluation indicated that the scoring function could assign a favorable energy to the crystal pose. The failure was therefore interpreted primarily as a sampling or search limitation for the deeply buried, highly charged nucleotide pocket rather than definitive proof of a defective scoring function.

Excluded outputs are retained for transparency but are not used as primary evidence.

### Cross-method comparisons

Scores from AutoDock Vina, AutoDock4, and GNINA are not treated as directly interchangeable binding free energies. Comparisons are made within a validated method and structure wherever possible.

---

## Responsible Interpretation

This repository reports an ongoing computational drug-discovery project. Docking scores, molecular-dynamics behavior, ADMET predictions, and toxicity classifications are hypothesis-generating evidence.

This repository does not claim that Nigellidine is:

- A confirmed FtsZ inhibitor
- Experimentally antibacterial
- Selective in humans
- Clinically effective
- Therapeutically safe
- Ready for human or animal use

These conclusions require controlled biochemical, microbiological, cellular, pharmacokinetic, and toxicological validation.

---

## Project Status

```text
Compound prioritization:       Complete
FtsZ molecular docking:        Complete
FtsZ redocking validation:     Complete
1JFF tubulin counter-screen:   Complete; GNINA score reconciliation pending
4I55 tubulin counter-screen:   Complete
Blind-docking comparison:      Complete
Corrected 100 ns MD:           Complete
Core MD analysis:              Complete
ADMET profiling:               Complete
MM-GBSA/MM-PBSA:               Pending
MD replicates:                 Pending
Experimental validation:      Pending
Manuscript preparation:       In progress
```

---

## Citation

If this repository contributes to academic work, cite:

1. This repository
2. The original 3VOA, 1JFF, and 4I55 structural entries
3. AutoDock Vina
4. AutoDock4
5. GNINA
6. DiffDock-L
7. GROMACS
8. CHARMM36
9. SwissADME
10. ProTox-3.0

Repository citation metadata should be provided in:

```text
CITATION.cff
```

---

## Use and Governance

**Research and academic use only.**

Project materials are shared for research and academic documentation. Repository publication status, redistribution, and reuse remain subject to applicable institutional requirements, software and database licences, and project-supervisor requirements.
