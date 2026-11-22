# Module 03: Koopman Operator Theory & Dynamic Mode Decomposition (DMD)

An operator-theoretic framework for linearizing nonlinear dynamical systems and extracting coherent spatio-temporal modes, cyclical frequencies, and regime-shift precursors across 45 liquid S&P 500 equities.

Continuing the **white-box pipeline**, this module shifts from static/lagged graph topology (**Module 02**) to continuous and discrete dynamical systems theory—representing complex market evolution as a linear infinite-dimensional **Koopman operator** acting on observables.

---

## 🧠 Mathematical Framework

Consider a nonlinear discrete-time dynamical system $x_{t+1} = F(x_t)$. Instead of modeling trajectories directly in state space, the **Koopman operator** $\mathcal{K}$ advances scalar observable functions $g(x)$ linearly forward in time:
$$(\mathcal{K}g)(x_t) = g(F(x_t)) = g(x_{t+1})$$

### 1. Extended Dynamic Mode Decomposition (EDMD)
By lifting state variables into a higher-dimensional dictionary of nonlinear observables $\Psi(x) = [\psi_1(x), \dots, \psi_p(x)]^T$ (such as polynomial basis functions), we obtain a finite-dimensional matrix approximation of the Koopman operator via least squares:
$$K = \Psi(X_{\text{next}}) \Psi(X)^{\dagger}$$
This allows nonlinear limit cycles and phase trajectories to be forecasted via pure linear matrix iteration.

### 2. Takens Delay Embedding & Exact Hankel-DMD
For high-dimensional financial time series where latent state variables are unobserved, we construct a block **Hankel matrix** $H$ with $d$ time-delay embeddings (Takens' theorem) and compute the reduced Koopman operator $\tilde{A} = U_r^T X_2 V_r \Sigma_r^{-1}$. Solving $\tilde{A} W = W \Lambda$ yields:
* **DMD Modes ($\Phi$):** Coherent spatial structures across equities.
* **Eigenvalues ($\lambda_k = e^{\omega_k \Delta t}$):** Governing growth/decay rates ($\text{Re}(\omega_k)$) and physical oscillation periods ($T_k = 2\pi / |\text{Im}(\omega_k)|$).

### 3. Rolling Koopman Stability & Mode Coherence
Tracking the spectral properties of the Koopman operator on stationary log-returns over a 120-day rolling window reveals two critical physical diagnostics:
* **Spectral Radius ($\max |\lambda_k|$):** Measures system dissipation vs. memory persistence (*critical slowing down*).
* **Top-3 Mode Energy Concentration (Coherence):** Measures the fraction of total dynamical energy captured by the leading Koopman modes. A sharp surge in coherence signals **phase synchronization**, where independent sector dynamics collapse into a single systemic market mode—a classic physical precursor to market sell-offs and liquidity shocks.

---

## 🧪 Research Blocks & Experiments

This module is structured into three sequential analytical blocks:

1. **Synthetic Stress-Test: Nonlinear Limit Cycle Linearization (Stuart–Landau Oscillator)**
   * Simulates a nonlinear Stuart–Landau oscillator converging to a limit cycle.
   * Lifts trajectories into a 3rd-order polynomial observable space and demonstrates multi-step linear forecasting via the EDMD Koopman operator.
2. **Exact Hankel-DMD on S&P 500 Detrended Log-Prices**
   * Reconstructs the market's latent phase space using a 15-day Hankel delay embedding across 45 S&P 500 stocks.
   * Extracts conjugate eigenvalue pairs on the complex unit circle, revealing underlying quarterly (~74d), semi-annual (~125d), and annual (~293d) market cycles.
3. **Rolling-Window Koopman Stability & Crash Precursor Detection**
   * Evaluates spectral radius $\max |\lambda|$ and Top-3 mode energy concentration over a 120-day sliding window on log-returns.
   * Empirically captures abrupt phase transitions where mode coherence spikes sharply at the onset of systemic market drawdowns.

---

## 📊 Key Takeaways & Market Interpretation

* **Conjugate Eigenvalue Pairs on the Unit Circle:** Confirm that collective equity movements contain persistent, low-frequency oscillatory modes rather than pure random walk noise.
* **Coherence Spikes as Systemic Stress Indicators:** During normal regimes, dynamical energy is dispersed across many modes (~15–20% in Top-3). During market crashes, cross-asset correlations lock together and Top-3 mode coherence surges (>35%), providing an interpretable, parameter-free regime alarm.

---

## 🛠 Dependencies

To run the experimental blocks in this module:
```bash
pip install numpy pandas scipy yfinance matplotlib
```
