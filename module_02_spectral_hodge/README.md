# Module 02: Spectral Graph Theory & HodgeRank on Financial Networks

An empirical exploration of hidden market hierarchies, lead-lag information flows, and cyclic arbitrage structures across 45 liquid S&P 500 equities. 

Building directly upon **Module 01 (Random Matrix Theory)**, this module models the stock market as a directed weighted graph and applies **combinatorial Hodge theory** alongside **spectral graph embeddings** to separate directional market leadership from cyclical noise.

---

## 🧠 Mathematical Framework

Given daily log-returns of $N=45$ major S&P 500 stocks across 5 sectors (*Tech, Finance, Healthcare, Consumer, Energy & Industrials*), we construct an asymmetric 1-day lag cross-correlation flow matrix:
$$Y = C_{\text{lag}} - C_{\text{lag}}^T$$
where $Y_{ij} > 0$ indicates that asset $i$ statistically leads asset $j$.

### 1. Combinatorial Hodge Decomposition (HodgeRank)
Any edge flow $y$ on a graph can be orthogonally decomposed into three distinct topological components:
$$y = y_{\text{grad}} + y_{\text{curl}} + y_{\text{harmonic}}$$

* **Gradient Flow ($y_{\text{grad}} = B_0 s$):** Captures the global hierarchy of the market. Solving $\min_s \|B_0 s - y\|_2$ yields a scalar potential $s_i$ for each stock, ranking assets from **market leaders** (information sources) to **laggards** (information sinks).
* **Curl / Rotational Flow ($y_{\text{curl}} = B_1 w$):** Captures local cyclic flows around triangular motifs ($i \to j \to k \to i$), representing short-term statistical arbitrage and localized capital rotation.
* **Harmonic Flow ($y_{\text{harmonic}}$):** Represents global, non-contractible cycles and irreducible topological noise.

### 2. RMT Denoising Synthesis (Marchenko–Pastur SVD)
Connecting back to **Module 01**, instead of relying on arbitrary correlation cutoffs, we apply Singular Value Decomposition (SVD) to the non-symmetric lag matrix $C_{\text{lag}}$ and filter out noise using the theoretical upper bound of the Marchenko–Pastur / quarter-circle law:
$$\sigma_+ = 1 + \sqrt{\frac{N}{T_{\text{eff}}}}$$

### 3. Normalized Graph Laplacian & Spectral Embedding
Using the symmetric affinity matrix $W = |Y|$, we construct the normalized graph Laplacian:
$$L_{\text{norm}} = I - D^{-1/2} W D^{-1/2}$$
Its lowest non-trivial eigenvectors ($v_2$ — the **Fiedler vector**, and $v_3$) reveal structural sector clustering (e.g., *Growth / Big Tech* vs. *Value / Defensive*) and measure the algebraic connectivity ($\lambda_2$) of the lead-lag network.

---

## 🧪 Research Blocks & Experiments

This module is organized into four sequential analytical blocks:

1. **Full 3-Component Hodge Decomposition & Fiedler Clustering**
   * Computes the exact energy distribution across Gradient, Curl, and Harmonic subspaces.
   * Extracts the algebraic connectivity ($\lambda_2$) and identifies opposing structural market poles via the Fiedler vector ($v_2$).
2. **Rolling-Window Market Regime Analysis**
   * Tracks the **Gradient Energy Ratio** over a 120-day rolling window (step = 5 days) to observe how market hierarchy evolves across different macroeconomic regimes.
   * Identifies the most persistent historical market leaders.
3. **RMT + HodgeRank Synthesis**
   * Compares naive hard-thresholding against parameter-free SVD spectral filtering ($\sigma > \sigma_+$) on both static (1000-day) and rolling (120-day) horizons.
4. **2D Spectral Market Map**
   * Projects the S&P 500 lead-lag graph onto the $(v_2, v_3)$ Laplacian eigenplane while encoding each node's **Hodge Leadership Potential** via color and scale.

---

## 📊 Key Takeaways & Market Interpretation

* **High Gradient Energy Ratio:** Indicates a strongly hierarchical, trend-driven regime where information propagates cleanly from dominant sector leaders to the broader market.
* **Elevated Curl & Harmonic Energy:** Signals market fragmentation, range-bound consolidation, or rapid cross-sector rotation where linear lead-lag signals break down.
* **RMT Filtering:** Eliminates false-positive edges caused by finite-sample noise ($N/T$ ratio), stabilizing the extracted leadership hierarchy over time.


```


