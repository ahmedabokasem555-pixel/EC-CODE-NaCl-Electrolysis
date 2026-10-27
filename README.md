# EC-CODE (Pilot Version 2.5.1)

Open-source Python notebook (NumPy / SciPy) for calibrating the current efficiency of chlorine production (x1) in membrane-free NaCl electrolysis cells from electrical, thermal and DPD data.

**Status:** pilot / software-verification release. The 69 automated tests verify the code (internal consistency, conservation checks, input validation). They are not an experimental validation. No real laboratory dataset is bundled yet.

*This repository was previously described under the working name "LAMP" (5-ODE, JAX, dashboard, ESP32, 93 tests). Those descriptions did not match the code and have been withdrawn. Dashboard and ESP32 firmware are not part of this release.*

## What it does
- Reads `runs.csv`, `calibration.csv` and 1 Hz traces (`traces/<run>.csv`).
- Solves one lumped thermal ODE: `C_tot dT/dt = I(V - E_tn) - K_dry(T - T_air) - Q_evap`.
- Infers x1 (current efficiency) and the loss factor eps with **grid-based Bayesian inference** (x1 grid 1e-4..0.35; eps grid 0.001..0.60; eps prior Beta(1.2, 4.9)).
- Cross-checks the result with GUM propagation, Monte Carlo (n = 10,000) and OAT sensitivities.
- Reports six physical modules: mass transfer (derived delta_eff), thermal ODE, conductivity residual, acid-base (effective C_T), gas volumes (H2, O2), limiting current (I_lim).

## What it needs (it does NOT work from I, V, T alone)
- **DPD free-chlorine readings** (photometer; dilute so the reading is inside the instrument range, the code multiplies the raw reading by dilution).
- Initial/final conductivity and time, a conductivity standard for the cell constant.
- Current, voltage and temperature logged at 1 Hz.

## Run
1. Open `EC-CODE_v2.5.1_PILOT_NaCl.ipynb` in Google Colab.
2. Run all cells from the top (definitions, self-tests), then upload `runs.csv`, `calibration.csv` and the `traces/` files when asked, then run the REAL-mode analysis cell.
3. Expected: 69 tests (68 pass, 0 fail, 1 check "K25 realistic", see LIM-6).

Dependencies: Python >= 3.10, numpy, scipy, pandas, matplotlib (standard Colab runtime).

## Known limitations
- **LIM-1:** x1 is a lower bound only if eps is measured without current in C runs. Without C runs (Pilot), eps is marginalised over its prior, so x1 is a prior-conditional estimate.
- **LIM-4:** x1 is obtained from condition B only.
- **LIM-6:** The thermal parameter K25 absorbs errors in K_dry and C_tot; it is not a physical constant.
- **LIM-7:** I_lim is estimated from three voltage steps only.
- **LIM-8:** The C2 consistency check uses n = 2.
- **LIM-9:** T_CL = 0.51 is the KCl literature value; NaCl is about 0.60 (about +24% effect on delta_eff).
- **No experimental validation yet;** results on real data are the subject of future work.

## Citation / licence
MIT licence. Please cite the Zenodo record: https://doi.org/10.5281/zenodo.23558695
## Known Issues in v2.5.1 (Addressed in Next Release)
- **Test Failures Display:** Running "Run all" initially shows 2 test failures. A subsequent `PATCH 2` cell redefines and resolves these (Pass: 68, Fail: 0). The next release will integrate these fixes directly into the main definitions.
- **C_CL Comment Typo:** The inline comment for `C_CL = 6.74` incorrectly states "(= 5.6 mmol/L)". The correct value is 6.74 mmol/L.
- **Module Numbering:** Output labels (e.g., `2_mass_transfer`, `3_thermal`) do not perfectly align with the 1-6 numbering in the manuscript table.
- **K25 Sensitivity:** The K25 check shows high sensitivity to K_dry perturbations (rel_err = 73.8% at +15% K_dry), as noted in LIM-6.