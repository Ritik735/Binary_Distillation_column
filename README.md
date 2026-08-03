# Binary Distillation Column Design and Parametric Analysis of an Ethanol-Water Mixture

Design and parametric study of a continuous binary distillation column separating an equimolar ethanol-water feed, simulated in **DWSIM** with the **ChemSep** rigorous column unit operation.

Deepanshu Kumar (Roll No. 124CH0061)
Department of Chemical Engineering, National Institute of Technology Rourkela

---

## Overview

An equimolar ethanol-water feed is separated in a rigorous equilibrium-stage column with a total condenser and a partial reboiler.
The bottoms composition is fixed by specification at 0.05 mole fraction ethanol, so the distillate purity carries the entire response to each design variable.
Three parameters were varied one at a time from a common base case:

| Study | Variable | Range | Held constant |
|---|---|---|---|
| Reflux ratio | R | 2 to 5 | 12 stages, feed stage 7, feed at 25 °C |
| Number of stages | N | 8 to 20 | R = 2, feed at 25 °C, feed stage scaled with N |
| Feed temperature | T_F | 25 to 78 °C | 12 stages, feed stage 7, R = 2 |

Common to every run: feed 112.353 kmol/h, 0.50/0.50 ethanol/water, 1 atm, NRTL activity-coefficient model for the liquid phase.

## Key results

**Reflux ratio is the strongest lever.** Raising R from 2 to 5 lifts distillate purity from 0.9170 to 0.9779 mole fraction ethanol, at the cost of a proportionally larger internal vapour rate and condenser duty.

**Stage count is comparably effective but saturates.** Going from 8 to 20 stages at fixed R = 2 raises purity from 0.7738 to 0.9883, with the gain per added stage shrinking as the column approaches the pinch.

**Feed temperature barely matters.** Preheating the feed from 25 °C to 78 °C *lowers* purity slightly, from 0.9058 to 0.8974, because the sub-cooled feed condenses rising vapour and augments internal reflux, an effect lost as the feed approaches its bubble point.

Bottom temperature stays at 90.90 °C in every run, which is the direct consequence of the fixed bottoms specification.

Note that the highest purities reached (0.9779 and 0.9883) sit at or above the ethanol-water minimum-boiling azeotrope at roughly 0.894 mole fraction.
Beyond that composition, simple distillation cannot separate the mixture further, so those cases represent the model pressed against its thermodynamic limit rather than an achievable design point.
This is discussed in the report.

## Repository layout

```
data/         Input matrices for the three parametric studies (.xlsx)
results/      Converged DWSIM/ChemSep results for each case (.xlsx)
graphs/       Eight parametric plots generated from results/ (.png)
images/       Column flowsheet and McCabe-Thiele constructions
simulation/   DWSIM flowsheet, Binary_Distillation.dwxmz
report/       Binary_Distillation_Column_Report.docx
```

### Files

| Study | Input | Results | Plots |
|---|---|---|---|
| Reflux ratio | `data/Reflux_Ratio_Study.xlsx` | `results/Reflux_Ratio_Results.xlsx` | purity, top temperature, top flow |
| Stages | `data/Stage_Study.xlsx` | `results/Stage_Study_Results.xlsx` | purity, top temperature, top flow |
| Feed temperature | `data/Feed_Temperature_Study.xlsx` | `results/Feed_Temperature_Results.xlsx` | purity, top flow |

`images/McCabe_Thiele_RR2.jpeg` and `images/McCabe_Thiele_RR5.jpeg` are the graphical stage constructions at the two extremes of the reflux study.

## Reproducing the simulation

1. Install [DWSIM](https://dwsim.org/) (v8 or later) and the bundled ChemSep CAPE-OPEN column.
2. Open `simulation/Binary_Distillation.dwxmz`.
3. Confirm the property package is set to NRTL and the feed stream matches the conditions in the table above.
4. For each case in the relevant `data/*.xlsx` file, set the varied parameter on the ChemSep column and run the flowsheet.
5. Read the condenser and reboiler product streams; these are the columns tabulated in `results/`.

## Report

`report/Binary_Distillation_Column_Report.docx` contains the full write-up: theory, methodology, all eleven figures, all tabulated data, discussion, conclusions and references.

## Data notes

Two inconsistencies in the raw spreadsheets are worth flagging, both left as generated rather than silently corrected:

- `results/Stage_Study_Results.xlsx` carries a "Reflux Ratio" column reading 2, 3, 4, 5. The corresponding input file specifies R = 2 for all five cases, and the 12-stage row reproduces the R = 2 reflux-study row exactly, so R = 2 is the value actually simulated. The row for Case 5 is also shifted one cell to the left.
- The base case (12 stages, R = 2, feed at 25 °C) appears in both the reflux study and the feed-temperature study, but returns 0.9170 in one and 0.9058 in the other, a difference of 0.0112.


