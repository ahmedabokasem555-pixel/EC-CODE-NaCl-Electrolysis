# EC-CODE (Pilot Version 2.5.1)

**EC-CODE** is an open-source Python tool (Numpy/SciPy) designed to model and calibrate chlorine production in membrane-free NaCl electrolysis.

### Current Capabilities
*   **Physical Model:** Integrates a single thermal ODE equation (C_tot.dT/dt) with 6 physical events.
*   **Validation:** Validated through 69 automated software tests (68 passed, 1 warning).
*   **Inference:** Utilizes a Grid-based inference approach to estimate x1.
*   **Dependencies:** Requires initial DPD measurements for calibration.
*   **Environment:** Runs in Google Colab.

### Limitations
*   The estimated x1 is a lower bound, conditional on prior assumptions.
*   Thermal parameter (K25) is absorbed into dry heat loss (LIM-6).
*   T_CL = 0.51 is a legacy value (KCl vs NaCl ~0.60) (LIM-9).
*   C_CL in the repository (5.6) is outdated compared to actual (6.74) (LIM-5).

### Repository Contents
*   `EC-CODE_v2.5.1_PILOT_NaCl.ipynb`: The Jupyter Notebook containing the code and tests.
*   `LICENSE`: MIT License.
