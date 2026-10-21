# LAMP: Laboratory Advanced Modeling Platform

**Author:** Ahmed Kasem (Independent Researcher, Egypt)  
**Associated Paper:** *LAMP: An Open-Source Platform for Bayesian Modeling of Chlorine Production in Membrane-Free NaCl Electrolysis* (To be submitted to SoftwareX).

---

## 📌 Overview
LAMP is an open-source Python framework designed to model the complex electrochemical behavior of chlorine production in membrane-free NaCl cells. It couples a 5-ODE physical system with Bayesian inference to estimate the current efficiency (\(x_1\)) of chlorine generation using only current, voltage, and temperature data.

## ✨ Key Features
*   **5-ODE System:** Models thermal dynamics, water mass, and dissolved/deposited salt.
*   **Bayesian Inference:** Uses MAP estimation with Laplace approximation for robust parameter estimation.
*   **93 Automated Tests:** Rigorous verification of conservation laws, numerical accuracy (GCI = 4.255), and cross-platform consistency.
*   **Interactive Dashboard:** A 34-tab HTML/JS interface for real-time visualization.
*   **Hardware Integration:** Includes ESP32 firmware for real-time deployment.

## ⚙️ Requirements
*   Python 3.10+
*   `JAX`, `NumPy`, `SciPy`, `Pandas`

## 🚀 How to Run
The core engine is provided as a Google Colab Notebook (`EC-CODE_v2.5.1_PILOT_NaCl.ipynb`).
1.  Upload the `.ipynb` file to Google Colab.
2.  Run **Cell 1** to initialize the physical constants and 5-ODE solver.
3.  Upload your lab data (`runs.csv`, `traces/`, `calibration.csv`).
4.  Run **Cell 15** to execute the Bayesian analysis.

## 📜 License
This project is licensed under the **MIT License**.
