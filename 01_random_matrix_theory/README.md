# 01. Random Matrix Theory: Spectral Denoising & Market Seismograph

> **Core Principle:** Math over brute compute. Pure linear algebra and statistical physics without black-box ML.

### Overview
An experimental framework for filtering finite-sample noise from high-dimensional correlation matrices ($N$ assets $\times$ $T$ observations) and detecting systemic regime shifts in real time.

### Mathematical Pipeline
1. **Marchenko–Pastur Law & Tracy–Widom Edge Correction:** Analytical separation of the "noise bulk" $[\lambda_-, \lambda_+]$ from true structural eigenvalues ($\lambda_k > \lambda_+ + \mathcal{O}(N^{-2/3})$) using a median-calibrated noise variance estimator $\hat{\sigma}^2$.
2. **Stieltjes Transform & Resolvent Renormalization (RIE):** Removing self-energy pole artifacts in $(zI - C)^{-1}$ to compare eigenvalue clipping against non-linear shrinkage.
3. **Inverse Participation Ratio (IPR):** Projecting surviving eigenmodes back onto asset space to isolate the structural backbone of the market (revealing financial institutions as the primary topological core over high-cap tech).
4. **Dynamic RMT Absorption Ratio ($\Delta \text{AR}$):** Rolling-window tracking of variance absorption across top modes to detect loss of degrees of freedom and early-stage market turbulence.

### Key Empirical Findings (S&P 500, $T=1000$ days)
* **73% Noise Reduction:** Out of 45 liquid stocks, 33 eigenvalues fall strictly inside the Marchenko–Pastur bulk ($\hat{\sigma}^2 \approx 0.52$).
* **Blind Sector Discovery:** Orthogonal eigenvectors $v_2, v_3, v_4$ automatically separate *Growth/AI vs. Defensive*, *Energy vs. Retail*, and *Banking vs. Software* with zero metadata.
* **Turbulence Detection:** Standardized shifts ($\Delta \text{AR} > 1.5\sigma$) accurately pinpoint structural compression ahead of and during major market drawdowns.
<img width="1250" height="323" alt="image" src="https://github.com/user-attachments/assets/b566046a-fdee-4a51-8581-dcf30d37151a" />
