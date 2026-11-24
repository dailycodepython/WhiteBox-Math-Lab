# Module 05: Tensor Networks (Matrix Product States & Tensor Train)

> **"Capturing high-order nonlinear interactions without the curse of dimensionality or black-box neural overparameterization."**

---

## 1. Analytical Foundations

Standard linear models and pairwise correlation matrices fail when system dynamics are governed by **multi-body nonlinear interactions** (e.g., 3rd- or 4th-order cross-asset dependencies). Mapping $N$ scalar features into a tensor product Hilbert space of local dimension $d$ creates an exponential parameter space $\mathcal{O}(d^N)$.

### Matrix Product States (MPS / Tensor Train)
We compress the global weight tensor $\mathcal{W} \in \mathbb{R}^{d \times d \times \dots \times d}$ into a 1D chain of 3rd-order core tensors $\{G^{(k)}\}_{k=1}^N$ of shape $(r_{k-1}, d, r_k)$, bounded by a controllable **bond dimension** $\chi$:

$$f(\mathbf{x}) = \langle \mathcal{W}, \Phi(\mathbf{x}) \rangle = \text{Tr}\Big( M^{(1)}(x_1) M^{(2)}(x_2) \cdots M^{(N)}(x_N) \Big)$$

where $\phi(x_k) = \big[1, \cos(\pi x_k), \sin(\pi x_k)\big]^\top$ embeds each quantile-normalized feature into a local trigonometric basis ($d=3$), and $M^{(k)}(x_k) = \sum_{s=1}^d G^{(k)}_{:, s, :} \phi_s(x_k)$.

### White-Box Diagnostics
* **TT-SVD Compression (Oseledets, 2011):** Right-to-left QR orthogonalization followed by left-to-right truncated SVD guarantees optimal low-rank approximation with exact spectral control.
* **Von Neumann Entanglement Entropy:** At each bond cut $(k \mid k+1)$, normalized squared singular values $p_i = \sigma_i^2 / \sum_j \sigma_j^2$ yield the exact information flow across the feature chain:
  $$S_k = -\sum_{i=1}^{\chi} p_i \ln p_i$$

---

## 2. Synthetic Stress-Testing

To verify structural recovery, we construct an $N=8$ synthetic system containing 5 pure noise distractors and a hidden non-separable 2-body/3-body entangled state between distant nodes ($x_1$ and $x_6$, exact theoretical TT-rank $= 2$):

$$y = \sin(\pi x_1)\cos(\pi x_6) + \cos(\pi x_1)\sin(\pi x_6) + \epsilon$$

| Model Architecture | Bond Dimension ($\chi$) | Out-of-Sample $R^2$ | Structural Interpretation |
| :--- | :---: | :---: | :--- |
| **Unentangled Product State** | $\chi = 1$ | $0.5649$ | Captures marginal projections only; fails on cross-terms |
| **Entangled Tensor Train (JAX)** | $\chi = 3$ | **$0.9946$** | Recovers exact hidden interaction across 4 noise nodes |

* **Entanglement Plateau:** Von Neumann entropy drops to near-zero on outer noise boundaries ($S_{0|1} = 0.076$, $S_{6|7} = 0.022$) and forms a flat **1-ebit plateau** ($S \approx \ln 2 \approx 0.693$) strictly across the active information channel $x_1 \dots x_6$.
* **TT-Cross Scalability (`tntorch`):** On a 10-dimensional grid of $32^{10} \approx 1.13 \times 10^{15}$ elements, cross-approximation reconstructs the surface with relative error **$3.49 \times 10^{-7}$** using only **$10,184$** oracle evaluations ($9.05 \times 10^{-12}$ of full tensor size).

---

## 3. Real-World Validation: S&P 500 Spectral Chain ($N=45$)

We apply the pure-JAX Tensor Train pipeline to **45 S&P 500 equities** to forecast 5-day realized basket volatility and map nonlinear cross-sector risk transmission.

1. **Spectral Ordering (Link to Module 02):** Tickers are ordered via the **Fiedler vector** of the correlation graph Laplacian—naturally aligning the 1D chain from defensive/healthcare stocks (`VZ`, `MRK`, `JNJ`) through energy/industrials (`XOM`, `CVX`, `BRK-B`, `LIN`) to mega-cap tech and semiconductors (`MSFT`, `AAPL`, `AVGO`, `NVDA`, `AMD`).
2. **Inter-Sector Entanglement Bridge:** Entanglement entropy peaks right at the structural hinge between defensive/commodity sectors and financial/industrial cores (`BRK-B | LIN` reaching the 1-ebit threshold $S \approx 0.692$), while collapsing to near-zero inside tightly collinear semiconductor pairs (`NVDA | AMD`, $S \approx 0.01$).

![Von Neumann Entanglement Entropy Across Spectral Asset Chain](<img width="1446" height="489" alt="image" src="https://github.com/user-attachments/assets/d4fa56a4-3ac2-4d7f-9215-618f52c16879" />


---

## References
1. Oseledets, I. V. (2011). *Tensor-Train Decomposition*. SIAM Journal on Scientific Computing, 33(5), 2295–2317.
2. Oseledets, I. V., & Tyrtyshnikov, E. E. (2010). *TT-cross approximation for multidimensional arrays*. Linear Algebra and its Applications, 432(1), 70–88.
3. Stoudenmire, E., & Schwab, D. J. (2016). *Supervised Learning with Tensor Networks*. Advances in Neural Information Processing Systems (NeurIPS).
