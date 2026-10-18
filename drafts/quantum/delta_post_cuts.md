# Cuts from the delta post — possibly useful in a later post

Removed from *From Kronecker Delta to Dirac Delta* on 2026-10-18 during
review, to keep that post shorter. Two closing remarks of the section
*The price*, plus the figure `figures/cells.png` and two reference
entries that only they used.

- The first remark is a natural opening for the Born-rule post (QM-3):
  probability density, probability of a cell = density × width,
  amplitude carries √Δx.
- The second (separability of L², step functions dense) belongs with
  the discrete/continuous/mixed spectra thread, or with a Hilbert-space
  aside in QM-3.

---

*A remark on the physics, and an advance on a later post.* Once
squared amplitudes are read as probabilities — the Born rule, which
the last post took on credit and a later post of the road derives — $|c_i|^2 = |a(\xi_i)|^2\, \Delta x$ says that $|a(x)|^2$
is a probability **density** — probability per unit length — and the
probability of landing in a cell is the density times the width.

![Cut the line into cells: the probability of a cell is the density times its width, so the amplitude of the cell state carries a square root of the width](figures/cells.png)

*A second remark, for readers who want the functional
analysis behind "discretization can approximate every state".*
Taken over all grids at once, the cell states form a countable family
whose linear combinations, the step functions, are dense in $L^2$:
that density is the separability of $L^2$ the last post promised, and
it is why discretization can approximate every state — see Rudin's
*Real and Complex Analysis*, Theorem 3.13, and Kolmogorov–Fomin,
chapter VIII, §51–52, in the references.


## Reference entries that went with them

- W. Rudin. *Real and Complex Analysis*, 3rd ed. McGraw-Hill, 1987 —
  Theorem 3.13: simple functions are dense in $L^p$.
- A. N. Kolmogorov, S. V. Fomin. *Elements of the Theory of Functions
  and Functional Analysis*, vol. 2. Graylock, 1961 (Russian original:
  А. Н. Колмогоров, С. В. Фомин, *Элементы теории функций и
  функционального анализа*) — chapter VIII, §51 (dense subsets of
  $L^2$) and §52 (the separability of $L^2$); together with Sergeev's
  Theorem 20 (lecture V), separability is equivalent to the existence
  of a countable orthonormal basis.
