# Search-Budget Artifacts in Continuous Causal Emergence

Replication package for

> Felipe Mora, *Search-Budget Artifacts in Continuous Causal Emergence:
> Fixed-Step Riemannian Optimization Manufactures Apparent Scale Dependence*.

Departamento de Industrias, Universidad Técnica Federico Santa María,
Valparaíso, Chile. ORCID [0009-0001-1034-5948](https://orcid.org/0009-0001-1034-5948).

## What the paper shows

Continuous causal emergence is estimated by maximizing an effective information
objective over projection matrices on the Stiefel manifold, in practice with
first-order Riemannian gradient descent at a fixed step size and a fixed
iteration budget. Both the objective and its Riemannian gradient vanish
quadratically with the norm of the whitened transition operator, and so does the
Lipschitz smoothness constant of the pullback. The certified step size of
Theorem 2.8 of Boumal, Absil and Cartis therefore grows as the inverse square of
the operator norm while the implemented step stays fixed, so the optimizer
stagnates exactly when the operator contracts. Any study sweeping a parameter
that contracts the operator confounds the physical effect with the convergence
failure of its own optimizer.

## Reproducing everything

```bash
pip install -r requirements.txt
python3 data/download_ff30.py     # the returns data are not redistributed, see data/README.md
./reproduce_paper1.sh
```

The script regenerates every table and every figure and then compiles the
manuscript. A full run takes roughly one hour on two cores.

## Layout

| Path | Contents |
| :--- | :--- |
| `code/` | Estimator: VAR(1) fitting, analytical effective information, Stiefel optimizer, SVD bound |
| `experiments/` | One runner per result, plus `plot_all_figures.py`. The `.csv` files are the outputs of the run behind the published figures |
| `evidence/` | `cefi_independent.py`, an independent reimplementation used to cross-check the estimator, and archived diagnostic tables |
| `data/` | NOAA climate indices; a download script for the industry portfolio returns |
| `figures/` | The four figures of the paper |
| `manuscript/` | Elsevier `elsarticle` source and bibliography (requires the `elsarticle` LaTeX package) |
| `formalization/` | Lean 4 proofs of the closure defect and of the Rayleigh-Ritz step |

## Formal verification

`formalization/` contains a small Lean 4 development, checked against mathlib,
with no `sorry`. It proves that the projected state is an autonomous linear
system for every initial condition **if and only if** the residual operator
`W A (I - Wᵀ W)` vanishes, and it proves the Rayleigh-Ritz step of Proposition 1
in the quadratic-form order, which is more general than the eigenvalue statement
used in the paper. The singular-value contraction half of Proposition 1 is not
formalized; `formalization/README.md` documents precisely what is and is not
proved, and why.

## Data availability

The climate indices are included. The industry portfolio returns are not: the
Kenneth R. French Data Library states that its contents are the property of Ken
French and Dimensional Fund Advisors and that use in part or whole requires
their permission. `data/download_ff30.py` retrieves them from the source and
verifies by SHA-256 that the result is byte-for-byte the file used in the paper.

## License

Code and formalization are released under the MIT License (see `LICENSE`). The
manuscript text and figures are the author's. The industry portfolio returns are
not covered by this license and are not distributed here.
