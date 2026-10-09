# Percolation on Random Networks: An Interactive Derivation

An interactive web companion to Sang Hoon Lee's lecture notes on percolation in random networks, prepared for the **[21st KIAS–APCTP Winter School on Statistical Physics](https://events.kias.re.kr/h/winter2024/)**.

The web demo was created by **Claude Opus 5.5** (Anthropic) from the handwritten lecture notes.

**Live demo:** https://lshlj82.github.io/percolation-by-generating-function/ (once GitHub Pages is enabled; see below)

## Lecture notes

- [ER_percolation.pdf](ER_percolation.pdf): percolation in the Erdős–Rényi random graph, critical exponents, and the correspondence with the Bethe lattice (sections 1–3 of the demo).
- [CM_percolation.pdf](CM_percolation.pdf): percolation in the configuration model via generating functions, the Erdős–Rényi case revisited, and power-law degree distributions (sections 4–5 of the demo).

## Repository contents

| File | Description |
| --- | --- |
| `index.html` | The interactive demo (single self-contained page) |
| `ER_percolation.pdf` | Lecture notes: Erdős–Rényi percolation |
| `CM_percolation.pdf` | Lecture notes: configuration-model percolation |
| `README.md` | This file |

## What it covers

1. **The giant component, live.** A sampled Erdős–Rényi graph $G_{n,p}$ with $p = c/(n-1)$. Dragging the mean degree $c$ adds edges in a fixed order, and a force layout shows the largest component forming once $c$ passes 1. A toggle colors every component with two or more nodes, not just the largest.
2. **Erdős–Rényi self-consistency.** From $u = (1 - p + pu)^{n-1} \to e^{-c(1-u)}$ to $S = 1 - e^{-cS}$, with the graphical solution, $S(c)$, and optional ensemble simulations at $n = 500$, $2000$ or $10000$.
3. **Critical exponents.** Expansion near $S = 0$ gives $S = 2(c-1)/c^2$ ($\beta = 1$), and $\langle s\rangle = 1/(1 - c + cS)$ gives $\gamma = 1$ from both sides. Includes log–log plots, effective exponents computed from the exact solution, and a comparison with finite-dimensional percolation (Christensen & Moloney, Table 1.2).
4. **Bethe lattice dictionary.** Bond percolation with $A = 1 - (1-pA)^{z-1}$ and $P_\infty = 1 - (1-pA)^z$, mapped onto ER via $u \leftrightarrow 1 - A$, $n - 1 \leftrightarrow z - 1$. The Bethe curve approaches the ER curve as $z$ grows. A sampled finite Cayley tree (radial drawing, root cluster highlighted) shows bond occupation directly, and a Monte Carlo estimator grows $10^4$ trees of depth 50 as a branching process to measure the probability that the root's cluster reaches the boundary, compared with the exact finite-depth recursion and $P_\infty$.
5. **Configuration model.** The generating-function recipe $g_0 \to g_1 \to u = g_1(u) \to S = 1 - g_0(u)$, with a cobweb plot of the fixed-point iteration and a Poisson / power-law toggle. A sampled configuration-model network (stub matching, degrees truncated at $k = n - 1$, self-loops discarded) is drawn alongside, with its largest component compared against $S$; a button averages the largest component over ten networks with $n = 10^4$.
6. **Power-law degrees.** $p_k = k^{-\gamma}/\zeta(\gamma)$ for $k \ge 1$: $S = 1$ for $\gamma \le 2$, a giant component for all $2 < \gamma \le 3$, and a threshold at $\zeta(\gamma - 2) = 2\zeta(\gamma - 1)$, i.e. $\gamma_c \approx 3.4788$ (solved numerically in the browser). Also plots $\langle k\rangle = \zeta(\gamma-1)/\zeta(\gamma)$, and can overlay $S(\gamma)$ measured in sampled configuration models with $n = 10^4$.

## Running it

It is a single self-contained file. Open `index.html` in any modern browser, or serve it with GitHub Pages:

1. Put `index.html`, the two PDFs and this README at the root of the repository, keeping the PDF file names exactly as above (the page links to them by relative path).
2. Go to **Settings → Pages**, choose **Deploy from a branch**, and select the branch and `/ (root)`.
3. The demo will be available at https://lshlj82.github.io/percolation-by-generating-function/.

An internet connection is needed only for web fonts (Google Fonts) and equation rendering (MathJax 3.2.2 from jsDelivr). All numerics run locally.

## Features

- Light and dark themes, following the system setting by default, with a toggle button in the top right (the choice is remembered in the browser).
- Responsive layout for phones and desktops.
- No build step and no dependencies beyond the two CDN resources above.

## Numerical methods

| Quantity | Method |
| --- | --- |
| $S = 1 - e^{-cS}$ | Newton's method from $S = 1$ (monotone convergence to the nontrivial root) |
| Fixed points $u = g_1(u)$, Bethe $A$, $\gamma_c$ | Bisection |
| $\zeta(s)$, $\mathrm{Li}_s(u)$ | Direct sum to $k = 400$ plus Euler–Maclaurin tail (Simpson quadrature for $u < 1$) |
| ER simulations | Geometric edge skipping (Batagelj–Brandes) and union–find |
| Bethe-lattice estimate | Branching process with binomial offspring, depth 50 |
| Configuration-model samples | Inverse-CDF degree sampling, uniform stub matching, union–find |

Checks: $\zeta(2)$ and $\mathrm{Li}_2(1/2)$ agree with exact values to about $10^{-15}$; $\gamma_c = 3.47875$ matches Newman's 3.4788; the $z = 3$ Bethe solution matches $1 - ((1-p)/p)^3$.

## References

- M. E. J. Newman, *Networks*, 2nd ed. (Oxford University Press, 2018), Secs. 11.5–11.6 and 12.5.
- K. Christensen and N. R. Moloney, *Complexity and Criticality* (Imperial College Press, 2005), Table 1.2.
- S.-W. Son, G. Bizhani, C. Christensen, P. Grassberger, and M. Paczuski, EPL **97**, 16006 (2012).
- Bethe-lattice equations as reproduced in the lecture notes from Prof. Young-Sul Cho's lecture slides; the notes also refer to Prof. S.-C. Park's lecture for the same graphical argument.

## Credits

Lecture notes: Sang Hoon Lee. Web demo: created by Claude Opus 5.5 (Anthropic).
