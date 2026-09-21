# Nigellidine–FtsZ Structure-Based Drug Discovery

**Status: In Progress** | Docking · MD · ADMET · Selectivity

Virtual screening, molecular dynamics, and ADMET profiling of *Nigella sativa* alkaloids against *S. aureus* FtsZ — a validated bacterial cell-division target — with a human-tubulin counter-screen for selectivity.

## Why FtsZ, why alkaloids

FtsZ is essential for bacterial cell division and structurally homologous to human tubulin — meaning a real drug candidate must be tested for selectivity, not just potency. *N. sativa*'s antibacterial activity is well documented, but almost entirely attributed to thymoquinone; its alkaloid fraction (nigellidine, nigellicine, nigellimine) is comparatively under-investigated. This project tests that gap directly.

Nigellidine was the lead candidate — highest docking score of the three — with nigellicine and nigellimine as pre-designated reserves.

## Docking — validated before trusting any result

| Tool | Nigellidine score |
|---|---|
| AutoDock Vina | −8.370 kcal/mol |
| AutoDock4 | −7.25 kcal/mol |
| GNINA (CNN-scored) | −8.25 to −8.63 kcal/mol |
| DiffDock-L | consistent pose, consensus with the above |

**Protocol validated via native-ligand redocking: RMSD 0.307 Å**, computed and independently cross-checked before any docked pose was trusted.

## Human-tubulin selectivity — a tested comparison, not an assumption

Docked into the equivalent nucleotide pocket of a human tubulin structure, using the same protocol, with the interpretation threshold fixed *before* any result was seen: a gap under ~1–2 kcal/mol would be noise; a larger gap would be real evidence of selectivity.

**A genuine method-dependent finding, handled honestly rather than hidden:** Vina failed its own redocking validation on the tubulin structure (2.68 Å, above the reliability threshold), while GNINA passed cleanly (0.991 Å). GNINA was therefore used as the trusted method for the actual comparison — specifically because it was the one shown to work on this structure.

**Result:** nigellidine scored **−5.48 kcal/mol** against tubulin, versus **−8.25 to −8.63 kcal/mol** against FtsZ — a gap of roughly **2.8–3.2 kcal/mol**. Under the pre-set threshold, this is genuine evidence of selectivity for the bacterial target over the human one.

## Molecular dynamics — 100 ns, apo system, fully analyzed

**A real bug was found and fixed before this result was trusted.** The first production run inadvertently included the co-crystallized GDP alongside nigellidine — not a clean test, since the ligand was competing with GDP rather than approaching the pocket freely. The error was root-caused (a ~28 Å offset traced to using an unposed CGenFF structure instead of the actual docked coordinates), corrected via rigid-body alignment (Kabsch) onto the validated docked pose, and the entire system was rebuilt apo (GDP-free) before rerunning.

**Result, from the corrected 100 ns trajectory:**

| Metric | Finding |
|---|---|
| Protein backbone RMSD | Stable, 0.20 → 0.27 nm — no unfolding |
| Radius of gyration | Flat (1.985 nm avg, 0.004 nm drift over 100 ns) |
| Ligand behavior | Two distinct stable poses, with a transition around 45–50 ns |
| Dominant contacts (>70% occupancy) | Phe183 (94.5%), Gly22 (85.9%), Gly104 (82.3%), Gly21 (80.1%), Arg29 (73.6%) |
| Hydrogen bonding | Minimal (0.15 bonds/frame) — binding is hydrophobic/van der Waals-driven |

Both stable poses occupy the same pocket; the second sits closer to the Gly20–22 edge. This is a sustained, real interaction with the intended binding site — confirmed through two independent metrics (RMSD and ligand-pocket distance) agreeing on the same transition timing.

## ADMET and toxicity — all three compounds profiled

| Compound | LD50 | Toxicity class | Carcinogenicity | Mutagenicity | Bioavailability |
|---|---|---|---|---|---|
| **Nigellidine (lead)** | 1000 mg/kg | 4 | Active (0.52, borderline) | Inactive | 0.55 |
| Nigellicine (reserve) | 1300 mg/kg | 4 | Active (0.50, borderline) | Inactive | 0.85 |
| Nigellimine (reserve) | 1300 mg/kg | **3** | Inactive | **Active (0.78)** | 0.55 |

All three pass Lipinski/Ghose/Veber/Egan/Muegge drug-likeness with zero violations and show high GI absorption. Nigellimine's Class 3 toxicity and strong mutagenicity signal are why it remains a reserve rather than a co-lead candidate.

## What's still open

- **MM-GBSA/MM-PBSA binding free energy** — not yet run
- **MD replicates** — a single 100 ns trajectory has been analyzed; independent repeats would strengthen the pose-transition finding
- **Ligand-based ML (Tier 2)** — scope pending discussion with the project supervisor
- Manuscript Results/Discussion sections in progress

## Repository contents

Docking configuration files, GROMACS `.mdp` parameter files, analysis scripts, ADMET data, and figures.

**Trajectory files (`.xtc`) are not included** — a 100 ns production trajectory is several gigabytes, well beyond what a code repository should hold. Available on request.

## Stack

AutoDock Vina, AutoDock4, GNINA, DiffDock-L · GROMACS (CHARMM36, TIP3P) · VMD · SwissADME, ProTox-3.0

**Research/academic use. Published with the approval of the project supervisor.**
