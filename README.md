# Design and Evaluation of an Autonomous Comparison Method for Feature Ranking for Machine Prognostics

<div align="center">

[![Degree](https://img.shields.io/badge/Degree-Master_of_Science-1e40af?style=for-the-badge)](thesis.pdf)
[![Institution](https://img.shields.io/badge/University-TU_Ilmenau-c026d3?style=for-the-badge)](https://www.tu-ilmenau.de/)
[![Field](https://img.shields.io/badge/Field-Predictive_Maintenance-15803d?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

**Department of Electrical Engineering and Information Technology • Technische Universität Ilmenau**  
*Author: Sayan Bhattacharya | Advisors: Prof. Dr. rer. nat. Jochen Seitz, Prof. Dr.-Ing. Patrick Mäder, M.Sc. Umut Onus, M.Sc. Dominik Walther*

</div>

---

## 📌 Executive Summary & Motivation

Predictive Maintenance (PdM) relies on sensor-driven Machine Prognostics to anticipate failures before they occur. With the growing demand for edge AI deployments on resource-constrained embedded platforms (microcontrollers and digital signal processors), reducing feature dimensionality while preserving Remaining Useful Life (RUL) estimation accuracy is paramount.

This thesis introduces an **Autonomous Comparison Framework for Feature Ranking (FR)** algorithms. It evaluates filter, wrapper, and embedded selection strategies across high-dimensional time, frequency, and time-frequency domains, establishing a Pareto-optimal trade-off between computational complexity and prognostics fidelity.

---

## 🏗️ System Architecture & Prognostics Pipeline

```mermaid
graph TD
    classDef data fill:#eff6ff,stroke:#1e40af,stroke-width:2px;
    classDef feat fill:#f0fdf4,stroke:#15803d,stroke-width:2px;
    classDef rank fill:#fefce8,stroke:#a16207,stroke-width:2px;
    classDef edge fill:#fdf2f8,stroke:#be185d,stroke-width:2px;

    subgraph Phase1 ["📡 Phase 1: High-Frequency Sensor Acquisition"]
        D1[PRONOSTIA Bearing Platform<br/>Accelerometers 25.6 kHz] 
        D2[IMMS GmbH Industrial Fan Dataset<br/>Run-to-failure vibration & current]
    end

    subgraph Phase2 ["🔬 Phase 2: Multi-Domain Feature Extraction"]
        F1[Time Domain<br/>RMS, Kurtosis, Crest Factor, Shape Factor]
        F2[Frequency Domain<br/>Spectral Energy, Spectral Centroid, Harmonics]
        F3[Time-Frequency Wavelets<br/>Wavelet Packet Transform Decomposition]
    end

    subgraph Phase3 ["⚖️ Phase 3: Autonomous Comparison & Ranking Engine"]
        R1[Filter Methods<br/>ReliefF, Fisher Score, Mutual Info]
        R2[Wrapper / Embedded<br/>Random Forest, LASSO, Genetic Search]
        R3[Autonomous Ranking Evaluator<br/>Monotonicity, Trendability, Prognostic Metric]
    end

    subgraph Phase4 ["⚡ Phase 4: Embedded Resource-Constrained Deployment"]
        E1[Complexity Reduction<br/>Memory Footprint & FLOPs Pareto Curve]
        E2[Edge RUL Estimation<br/>Embedded Microcontroller Deployment]
    end

    D1 & D2 --> F1 & F2 & F3
    F1 & F2 & F3 --> R1 & R2 & R3
    R1 & R2 & R3 --> E1
    E1 --> E2

    class D1,D2 data;
    class F1,F2,F3 feat;
    class R1,R2,R3 rank;
    class E1,E2 edge;
```

---

## 📐 Mathematical Formulation

The autonomous comparison score assesses feature subsets across three diagnostic indicators:

1. **Monotonicity ($Mon$)**: Captures the continuous degradation trajectory of machine wear:
   $$	ext{Mon}(F) = rac{1}{K(K-1)} \sum_{k=1}^K |	ext{corr}(F, t_k)|$$

2. **Trendability ($Tre$)**: Measures the correlation between degradation trajectories across diverse operating regimes:
   $$	ext{Tre}(F) = \min_{i, j} |	ext{corr}(F^{(i)}, F^{(j)})|$$

3. **Complexity Penalty ($\mathcal{C}_{comp}$)**: Quantifies memory overhead and arithmetic operations on target DSPs:
   $$\mathcal{S}_{autonomous} = w_1 \cdot 	ext{Mon}(F) + w_2 \cdot 	ext{Tre}(F) - w_3 \cdot rac{\mathcal{C}_{comp}}{\mathcal{C}_{budget}}$$

---

## 📊 Experimental Evaluation & Benchmark Datasets

| Dataset | Operating Conditions | Sensor Inputs | Target Output |
| :--- | :--- | :--- | :--- |
| **PRONOSTIA (FEMTO-ST)** | 1800 rpm (4 kN), 1650 rpm (4.2 kN), 1500 rpm (5 kN) | Radial vibration accelerometers ($X, Y$) | Bearing Remaining Useful Life (RUL) |
| **IMMS GmbH Fan Testbed** | Variable thermal & mechanical aerodynamic loads | Multi-axis vibration, Current sensors | Fault classification & Early degradation detection |

---

## 📑 Repository Structure

```
├── thesis.pdf           # Full Master's thesis document (TU Ilmenau)
├── LICENSE              # MIT License
└── README.md            # Architectural documentation & project overview
```

---

## 🚀 Citation & Contact

If you find this research useful in your work on predictive maintenance, edge prognostics, or feature ranking, please consider citing:

```bibtex
@mastersthesis{bhattacharya2024autonomous,
  author       = {Sayan Bhattacharya},
  title        = {Design and Evaluation of an Autonomous Comparison Method for Feature Ranking for Machine Prognostics},
  school       = {Technische Universit{"a}t Ilmenau},
  year         = {2024},
  address      = {Ilmenau, Germany},
  department   = {Department of Electrical Engineering and Information Technology}
}
```

- **Author**: Sayan Bhattacharya
- **Email**: [sayanpm17@gmail.com](mailto:sayanpm17@gmail.com)
- **LinkedIn**: [linkedin.com/in/snbhattacharya5](https://www.linkedin.com/in/snbhattacharya5/)
