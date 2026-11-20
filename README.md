# WhiteBox-Math-Lab
Physics-informed data analysis without black boxes. Exploring Random Matrix Theory, Spectral Graph Theory, Hodge Decomposition, Koopman Operators, and Information Geometry.
# WhiteBox-Math-Lab

> **Philosophy:** *Math over brute compute.* Exploring transparent, physics-informed, and geometric methods for complex data analysis — strictly without black-box neural networks or gradient boosting.

---

### Core Thesis
Modern machine learning relies heavily on high-parameter black boxes that trade interpretability and stability for raw compute. This repository serves as an open research log exploring an alternative paradigm: **uncovering the underlying geometry, symmetries, and field equations of data** using pure linear algebra, statistical physics, and differential topology.

Every module in this lab follows a strict **white-box pipeline**:
1. **Analytical Foundations:** Deriving exact operators, invariants, and boundary conditions.
2. **Synthetic Stress-Testing:** Validating behavior on controlled manifolds with known ground truth.
3. **Real-World Validation:** Applying the mathematical core to high-dimensional financial, transactional, or dynamic systems.

---

### Research Roadmap & Modules

| # | Module | Mathematical Core | Primary Objective | Status |
| :--- | :--- | :--- | :--- | :--- |
| **01** | **[Random Matrix Theory](./01_random_matrix_theory)** | Marchenko–Pastur Law, Tracy–Widom Edge, Stieltjes Resolvent (RIE), IPR, Absorption Ratio ($\Delta\text{AR}$) | Separating true systemic structure from finite-sample noise and detecting early-stage market turbulence. | **Completed** |
| **02** | **Spectral Graphs & Hodge Theory** | Graph Laplacians ($L_0, L_1$), Discrete Exterior Calculus (DEC), Helmholtz–Hodge Decomposition | Decomposing directed network flows into gradient hierarchies (leaders vs. followers), local curls, and harmonic cycles. | *In Progress* |
| **03** | **Koopman Operator & DMD** | Spectral Theory of Dynamical Systems, Dynamic Mode Decomposition | Linearizing nonlinear time-series evolution into pure oscillating and decaying physical modes. | *Planned* |
| **04** | **Information Geometry** | Riemannian Statistical Manifolds, Fisher Information Metric, Bregman Divergences | Detecting regime shifts and phase transitions via geodesic distances on probability spaces. | *Planned* |
| **05** | **Tensor Networks (MPS)** | Matrix Product States / Tensor Train Decompositions | Capturing high-order nonlinear feature interactions on tabular data using quantum many-body formalism. | *Planned* |
| **06** | **Conformal Prediction** | Exchangeability, Non-Conformity Quantiles | Wrapping geometric models with distribution-free, mathematically guaranteed uncertainty bounds. | *Planned* |

---

### Tech Stack
* **Core Compute:** `NumPy`, `SciPy`, `JAX` (pure linear algebra & spectral solvers)
* **Verification:** Synthetic manifold generators & real-world empirical benchmarks
* **No Black Boxes:** Zero deep learning frameworks, zero tree-based ensembles.
