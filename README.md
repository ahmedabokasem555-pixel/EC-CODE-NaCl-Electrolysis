# EC-CODE (Pilot Version)

**EC-CODE** is an open-source Python-based tool (Numpy/SciPy) designed to model and calibrate chlorine production in membrane-free NaCl electrolysis.

### Current Capabilities (Pilot Version V2.5.1)
*   **Physical Events:** Integrates **6** physical events.
*   **Validation:** Validated through **69** automated tests.
*   **Inference:** Utilizes a **Grid-based inference** approach.
*   **Sensitivity:** Uses One-At-A-Time (OAT) sensitivity analysis.
*   **Environment:** Runs in Google Colab using Numpy and SciPy.

### Important Limitations
*   The model requires initial DPD measurements to calibrate the current efficiency (x1).
*   The estimated x1 represents a lower bound due to prior assumptions.
*   Thermal parameter (K25) is absorbed into dry heat loss due to unmeasured variables.

### Repository Contents
*   `EC-CODE_v2.5.1_PILOT_NaCl.ipynb`: The main Jupyter Notebook containing the code, model, and tests.
*   `LICENSE`: MIT License.