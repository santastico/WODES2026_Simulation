# Traffic Light Control Simulation using Tropical Algebra

This repository contains the source code for the simulation and validation of the **Global Just-in-Time (JIT) Controller** for urban traffic networks, as presented in the paper:

> **"Global Just-in-Time Control Synthesis for Urban Traffic Networks: An Approach Based on Tropical Algebra"**
> *Gabriel S. Pereira, C. A. Maia et al.*

## 🎯 Objective

The primary goal of this project is to validate a unified algebraic framework for traffic signal control. Traditional methods often treat safety (mutual exclusion) and efficiency (synchronization/Green Waves) as separate control layers. Our approach unifies these constraints into a single Max-Plus Linear System model.

Specifically, this simulation demonstrates:
1.  **Unified Modeling:** How restrictive (safety) and cooperative (synchronization) constraints are mapped into Max-Plus matrices ($A_0, A_1, L_0, L_1$).
2.  **JIT Synthesis:** The calculation of a global control law that guarantees the network operates at its maximum natural periodicity (eigenvalue $\lambda$).
3.  **Robustness Analysis:** A comparison of system behavior under nominal conditions versus failure scenarios (e.g., a signal stuck in Red due to a 1200s delay), highlighting the resilience of the Global JIT controller compared to rigid local logic.

## 🛠️ Prerequisites

To run this simulation, you need:
*   **ScicosLab 4.4.1** (or compatible version).
*   **Max-Plus Algebra Toolbox** for ScicosLab (usually included in standard distributions or available as a separate loader).

## 🚀 How to Run

1.  **Download the Code:** Clone this repository or download the `traffic_control_simulation.sce` file.
2.  **Open ScicosLab:** Launch the ScicosLab environment.
3.  **Load the Toolbox:** Ensure the Max-Plus toolbox is loaded. If not, execute the loader script (usually `exec('PATH_TO_TOOLBOX/loader.sce')`).
4.  **Execute the Script:**
    *   Open the file in the ScicosLab editor.
    *   Run the script by clicking "Execute" or typing `exec('traffic_control_simulation.sce', -1)` in the console.

## ⚙️ Configuration & Parameters

You can modify key parameters directly in the script header to test different scenarios described in the paper:

*   **`p` (Number of Signals):** Default is 5 (matching the paper's case study).
*   **`M_rst` & `M_cop`:** Matrices defining the restrictive (exclusion) and cooperative (synchronization) topology.
*   **`k` (Simulation Horizon):** Number of event cycles to simulate (e.g., `k=6` for short tests, `k=50` for long-run analysis).
*   **`k_fl` & `fl` (Failure Injection):**
    *   Set `k_fl = 0` for **Nominal Operation** (Golden Run).
    *   Set `k_fl > 0` (e.g., `2`) to inject a delay at the $k$-th cycle.
    *   `fl` defines which transition suffers the delay (e.g., Transition 7 corresponds to the Red-to-Green change of Signal 3).

## 📊 Expected Results

Upon execution, the script generates:

1.  **Terminal Output:**
    *   Matrices dimensions and calculated Eigenvalue ($\lambda$), representing the network cycle time.
    *   A tabular view of firing times for Red, Green, and Yellow phases for each traffic light.
    *   Execution time metrics.

2.  **Graphical Plots:**
    *   **Step Response Graphs:** Visualizing the state (Red/Green/Yellow) over time.
    *   **Failure Analysis:** If a failure is injected, you will observe the propagation of the delay. The Global JIT controller (represented by `Fmax`) will demonstrate how unaffected signals (like $S_4$ in the paper's restrictive pair example) extend their Green phases to optimize flow, contrasting with the rigid behavior of local controllers.

> **Note:** These results correspond directly to **Section V (Example)** and the **Robustness Analysis** figures presented in the article.

## 📝 Citation

If you use this code or methodology in your research, please cite our paper:

```bibtex
@article{Pereira2026GlobalJIT,
  title={Global Just-in-Time Control Synthesis for Urban Traffic Networks: An Approach Based on Tropical Algebra},
  author={Pereira, Gabriel S. and Maia, C. A.},
  journal={Proceedings of the IEEE/Conference Name},
  year={2026}
}
