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


---

# The box (cut 2026-10-18)

Removed from the delta post as a whole optional section. Natural home:
the observables post (QM-3) or the dynamics post, next to the
discussion of eigenbases of operators — it answers "why does practice
always talk in terms of a large box and discrete momenta, rather than
in deltas as we did here".

## The physicist's version: a very large box

Physicists rarely discretize position. They discretize *momentum*
instead, and the device is a box. Put the particle in a box of length
$L$ with periodic boundary conditions. Plane waves $e^{ikx}$ then fit
only for wave numbers $k_n = 2\pi n / L$, $n \in \mathbb Z$ — a
discrete, countable menu — and, normalized as
$\frac{1}{\sqrt L}\, e^{i k_n x}$, they are honestly orthonormal on
$[0, L]$: $\langle k_n | k_m \rangle = \delta_{nm}$, a Kronecker delta
again, with sums over $n$ and nothing exotic anywhere. Now let
$L \to \infty$. The spacing $2\pi / L$ of the menu shrinks, sums over
$n$ turn into integrals, $\sum_n \to \frac{L}{2\pi} \int dk$, and the
normalized plane waves, rescaled by $\sqrt{L / 2\pi}$ — exactly as our
cell states were rescaled by $1/\sqrt{\Delta x}$ — acquire the delta
normalization $\langle k | k' \rangle = \delta(k - k')$. Note that on the infinite line the plane wave $e^{ikx}$ itself is
the momentum twin of the position ket, with the same disease in the
other direction: $|e^{ikx}|^2 = 1$ everywhere, so its length
$\int 1\, dx$ is infinite, and it is a unit vector living just outside
$L^2$, exactly as $|x\rangle$ is. It is this post's construction with
the roles of position and momentum exchanged: the box plays the grid, $2\pi / L$ plays $\Delta x$, and
"the box is large enough not to matter" is the physicist's phrase for
"the limit is taken only in numbers". Working in a huge box and never
sending $L$ to infinity is, in practice, what a physicist means by a
Hilbert space: a discrete orthonormal basis, with the continuum kept
as a convenient shorthand. We chose the grid rather than the box for
two reasons: it keeps the Kronecker delta literally in view, and it
needs no Fourier transform — which the road has not yet earned in the
quantum setting. The box returns twice: in the dynamics post, where
momentum gets its own basis, and in the particle-in-a-box post, where
the walls are real.

