# WhiteBox-Math-Lab: Unified Geometric & Topological Market Regime Engine

A physics-informed, interpretable ("white-box") quantitative framework for real-time volatility forecasting, structural regime detection, and adaptive conformal risk bounds across multi-asset equity baskets (validated on N=45 S&P 500 equities, 2024–2026).

---

## 1. Architecture Overview

Instead of relying on black-box neural networks or fragile Gaussian assumptions, **WhiteBox-Math-Lab** models the market as an evolving high-dimensional dynamical system on a Riemannian manifold. At every rolling window W (default W = 60 trading days), the engine extracts five geometric and topological invariants before forecasting forward realized volatility:

1. **Module 01 — Random Matrix Theory (RMT) Denoising (`rmt_denoise`)**
   * Filters Marchenko–Pastur bulk noise from the empirical correlation matrix to isolate true collective market modes (\(C_{\text{clean}}\)) and computes the **Absorption Ratio (AR)**—the fraction of total variance absorbed by dominant systemic eigenvectors.
2. **Module 02 — Helmholtz–Hodge Simplicial Decomposition (`hodge_decompose`)**
   * Projects pairwise lead–lag return flows onto a complete simplicial complex (B₁, B₂), separating directional market leadership (**Gradient Norm**, \(\Vert{}f_{\text{grad}}\Vert{}\)) from non-transitive, cyclical capital churn (**Curl Energy**, \(\mathcal{E}_{\text{curl}}\)).
3. **Module 03 — Information Geometry on the SPD Manifold (`fisher_geodesic_velocity`)**
   * Measures the **Fisher–Rao Geodesic Velocity** \(v_{\text{Fisher}}(t) = d_{\text{SPD}}(C_{\text{clean}}(t), C_{\text{clean}}(t-1))\), quantifying how rapidly the market's underlying correlation structure is deforming.
4. **Module 04 — Koopman / Dynamic Mode Decomposition (`koopman_dmd_forecast`)**
   * Embeds target volatility alongside geometric invariants into a delay-coordinate Hankel space to generate linear operator forecasts (\(\hat{\sigma}_{t+1}\)) of nonlinear market dynamics.
5. **Module 05 — Tensor-Train SVD & Quantum Entanglement (`tensor_entanglement`)**
   * Constructs a 3rd-order Hermite polynomial interaction tensor across top eigenfactors and computes the **Von Neumann Entropy** \(S_{\text{vN}}(t)\) via TT-SVD to measure the effective degrees of freedom (structural diversification) of the market.
6. **Module 06 — Physics-Informed Adaptive Conformal Inference (`conformal_bounds`)**
   * Dynamically scales prediction intervals using geodesic velocity and systemic absorption shifts (Δ AR), achieving nearly **2x higher tail coverage** during high-volatility shocks (`>25%` annualized vol) compared to parametric Gaussian baselines.

---
<img width="1505" height="700" alt="image" src="https://github.com/user-attachments/assets/903a94f9-629c-4d31-8b03-6862676ba756" />

## 2. Diagnostic Guide: Interpreting Market Regimes

A core pitfall of conventional risk models is mistaking a temporary lull in price movement for the end of a crisis. By jointly tracking **Fisher–Rao Velocity $(v_{\text{Fisher}})$** and **Von Neumann Entropy $(S_{\text{vN}})$**, the engine distinguishes between four distinct structural states:

| Market Regime | Fisher–Rao Velocity $v_{\text{Fisher}}(t)$ | Von Neumann Entropy $S_{\text{vN}}(t)$ | Secondary Signals AR, $\mathcal{E}_{\text{curl}}$ | Structural Interpretation |
| :--- | :--- | :--- | :--- | :--- |
| **1. Calm / Decoupled Equilibrium** | **Low** (`< 0.45`) | **High** (`> 0.80`) | Low AR; stable Gradient norm | Sectors move independently; high degrees of freedom; standard diversification holds. |
| **2. Acute Phase Transition (Shock Onset)** | **Extreme Spike** (`> 1.50 – 2.00`) | **Sharp Drop** (`< 0.50`) | Rising AR; spiking Hodge Curl | Old correlation structure is actively breaking; rapid capital flight and cross-sector contagion. |
| **3. "Frozen" / Prolonged Crisis (Metastable)** | **Low / Sawtooth** (`0.25 – 0.45` with periodic spikes) | **Compressed / Stagnant** (`0.35 – 0.55`) | Elevated AR; erratic Curl | **False calm.** Correlation matrix has locked into a stressed state. Low velocity reflects structural rigidity, not recovery. |
| **4. Systemic Collapse (Tail Escalation)** | **Secondary Spike** (`> 2.00`) | **Collapse to Zero** (`0.00 – 0.15`) | AR approaches maximum | **Rank-1 degeneration.** All assets synchronize into a single panic factor (forced liquidations / margin calls). |

---

## 3. How to Tell If a Crisis Will Continue or End

### Indicators of Crisis Continuation or Escalation
A low reading of \(v_{\text{Fisher}}(t)\) immediately following a shock **does not** signal safety if \(S_{\text{vN}}(t)\) remains depressed:
* **The "Frozen Crisis" Trap (Continuation):** When shock days remain inside the rolling window W, day-to-day changes in \(C_{\text{clean}}(t)\) shrink, causing \(v_{\text{Fisher}}(t)\) to drop back toward `~0.25`. However, as long as \(S_{\text{vN}}(t)\) stays trapped in the `0.35–0.55` band, the market remains in a **metastable, fragile state**—highly vulnerable to secondary aftershocks from headline catalysts.
* **Sawtooth Velocity Pattern:** Repeated bursts of \(v_{\text{Fisher}}(t) > 1.0\) every 5–10 trading days without a sustained recovery in \(S_{\text{vN}}(t)\) indicate a chronic crisis regime where the market fails to digest ongoing macro or regulatory shocks.
* **Escalation to Systemic Contagion:** If a secondary spike in \(v_{\text{Fisher}}(t)\) drives \(S_{\text{vN}}(t) \to 0\), cross-asset diversification has completely broken down—signaling acute systemic stress.

### Indicators of True Crisis Resolution (Recovery)
A genuine exit from a crisis regime unfolds as a **two-step structural sequence**:
1. **Step 1 — Re-coupling & Dispersion Spike:** A moderate, constructive uptick in \(v_{\text{Fisher}}(t)\) accompanied by falling **Absorption Ratio (AR)**, signaling that the market is breaking out of its rigid, panic-driven correlation matrix as sectors begin differentiating again.
2. **Step 2 — Sustained Entropy Restoration:** **Von Neumann Entropy \(S_{\text{vN}}(t)\) climbs steadily back above `0.80`**, confirming that independent market factors have re-emerged and systemic fragility has dissipated.

> **Rule of Thumb:** Never narrow risk corridors solely because \(v_{\text{Fisher}}(t)\) has cooled down. Wait for **\(S_{\text{vN}}(t) > 0.80\)** to confirm structural recovery.

---

## 4. Empirical Validation (S&P 500, N = 45)

<img width="1000" height="706" alt="image" src="https://github.com/user-attachments/assets/1d712516-6e9f-4f0c-b967-bfdaae3530b2" />



* **Nominal Target Coverage:** `90.0%` ($\alpha = 0.10$)
* **Overall Coverage:** `88.9%` (Unified White-Box) vs. `85.5%` (Parametric Gaussian)
* **High-Volatility Stress Regime (`>25%` Ann. Vol):** **`47.4%`** (Unified White-Box) vs. **`26.3%`** (Parametric Gaussian)
* **Regime Separation:**
  * Mean $v_{\text{Fisher}}$: `0.430` (Calm) $\rightarrow$ `0.637` (High-Vol)
  * Mean $S_{\text{vN}}$: `0.652` (Calm) $\rightarrow$ `0.543` (High-Vol)

## 5. References & Theoretical Foundations

The **WhiteBox-Math-Lab (Module 07)** pipeline synthesizes foundational results across six distinct areas of statistical physics, differential topology, and distribution-free statistics into a single unified risk engine:

### Random Matrix Theory & Systemic Absorption (Module 01)
* **Laloux, L., Cizeau, P., Bouchaud, J.-P., & Potters, M. (1999).** *Noise Dressing of Financial Correlation Matrices.* Physical Review Letters, 83(7), 1467–1470. *(Marchenko–Pastur bulk denoising of empirical equity correlations).*
* **Kritzman, M., Li, Y., Page, S., & Rigobon, R. (2011).** *Principal Components as a Measure of Systemic Risk.* The Journal of Portfolio Management, 37(4), 112–126. *(Introduction of the Absorption Ratio as a leading indicator of market fragility).*

### Combinatorial Hodge Theory & Financial Flows (Module 02)
* **Jiang, X., Lim, L.-H., Yao, Y., & Ye, Y. (2011).** *Statistical Ranking and Combinatorial Hodge Theory.* Mathematical Programming, 127(1), 203–244. *(Helmholtz–Hodge decomposition on simplicial complexes into gradient hierarchies and cyclic curls).*
* **Kichikawa, Y., Iyetomi, H., Iino, T., & Inoue, H. (2019).** *Community Structure Based on Circular Flow in a Large-Scale Transaction Network.* Applied Network Science, 4(1), 92. *(Separating directional leadership from rotational capital churn in financial networks).*

### Information Geometry on the SPD Manifold (Module 03)
* **Barbaresco, F. (2012).** *Information Geometry of Covariance Matrix: Cartan–Siegel Homogeneous Bounded Domains.* Matrix Information Geometry, Springer, 199–218. *(Geodesic distances and Riemannian velocities on spaces of symmetric positive-definite matrices).*
* **Bouchard, F., et al. (2023).** *The Fisher–Rao Geometry of CES Distributions.* arXiv:2310.01032. *(Riemannian framework for tracking structural deformations in heavy-tailed financial covariance matrices).*

### Koopman Operator & Delay-Coordinate DMD (Module 04)
* **Mann, J., & Kutz, J. N. (2016).** *Dynamic Mode Decomposition for Financial Trading Strategies.* Quantitative Finance, 16(11), 1643–1655. *(Hankel-DMD operator lifting for extracting coherent dynamical modes from nonstationary equity time series).*

### Tensor Networks & Von Neumann Market Entropy (Module 05)
* **Oseledets, I. V. (2011).** *Tensor-Train Decomposition.* SIAM Journal on Scientific Computing, 33(5), 2295–2317. *(TT-SVD compression for high-order interaction tensors).*
* **Chakraborty, A., & Easwaran, S. (2021).** *Von Neumann Entropy of Financial Correlation Matrices as an Indicator of Market Crises.* Physica A: Statistical Mechanics and its Applications. *(Quantum-inspired density matrix entropy $S_{\text{vN}}$ capturing rank-1 synchronization during market panics).*

### Adaptive Conformal Inference under Distribution Shift (Module 06)
* **Gibbs, I., & Candès, E. (2021).** *Adaptive Conformal Inference Under Distribution Shift.* Advances in Neural Information Processing Systems (NeurIPS), 34, 1660–1672. *(Online $\alpha_t$ quantile recalibration for non-exchangeable time series).*
