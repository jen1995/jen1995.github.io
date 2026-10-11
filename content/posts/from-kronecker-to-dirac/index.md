---
title: "From Kronecker Delta to Dirac Delta"
date: 2026-09-27
draft: true
author: ["Ivan Petrov", "Eugenia Elistratova"]
tags: ["quantum", "math"]
summary: "The last post wrote a state as an integral over position kets and left two symbols on credit: what is |x⟩, and what is ⟨x|y⟩? A guest post pays the debt by discretizing honestly — and watching the Kronecker delta of an orthonormal grid turn, in the only sense available, into the Dirac delta."
math: true
weight: 49
---

*A guest post by Ivan Petrov, edited together for the quantum road — the
first of, we hope, many.*

[Last time](/posts/states-are-vectors/#when-the-menu-is-infinite) the
quantum road reached the continuous menu. A particle on a line has a
position, every real number is a possible reading, and the state had
to be written as an integral over position kets:

$$
|\psi\rangle = \int \psi(x)\, |x\rangle\, dx.
$$

That line was written on credit twice over. What exactly is the ket
$|x\rangle$ — and what is $\langle x | y \rangle$, the inner product of
two of them? For a discrete orthonormal basis the answer was the
Kronecker delta, $\langle E_i | E_j \rangle = \delta_{ij}$. For the
continuous basis it *cannot* be, and finding out what replaces it is
this post's whole job. The answer is an old friend of this blog: the
**Dirac delta**, which the Fourier road's
[Part 1](/posts/fourier-series-to-spectrogram-part-1/#an-honest-model-of-a-discrete-signal)
built as the limit of a shrinking averaging window. Today it will
arrive by a completely different road — as the limit of an
orthonormal grid — and the two roads will meet at the same object.

![Two roads to one object: the shrinking window of Part 1 and the refining grid of this post both end at the Dirac delta](two_roads.png)

The Dirac delta is usually handed to you as-is: a "function" that is
zero everywhere except at a single point, where it is infinitely
tall, and which somehow integrates to one. What actually defines it is
the **sifting property**,

$$
\int_{-\infty}^{\infty} f(y)\, \delta(x - y)\, dy = f(x),
$$

which says that integrating any function against $\delta(x - y)$
plucks out its value at $y = x$. Very useful — but where does such a
thing come from? We will derive it from the Kronecker delta, by
discretizing the continuous inner product and refusing to cheat at any
step.

## The Kronecker delta

In finite dimensions an orthonormal basis $\{ |E_i\rangle \}$ satisfies

$$
\langle E_i | E_j \rangle = \delta_{ij} = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases}
$$

— the Kronecker delta of the last post. Expand two vectors,
$|\psi\rangle = \sum_i a_i |E_i\rangle$ and
$|\varphi\rangle = \sum_j b_j |E_j\rangle$, and the inner product
collapses:

$$
\langle \psi | \varphi \rangle = \sum_i \sum_j a_i^* \, b_j \, \langle E_i | E_j \rangle = \sum_i \sum_j a_i^* \, b_j \, \delta_{ij} = \sum_i a_i^* \, b_i.
$$

The $\delta_{ij}$ acts as a **diagonal selector**: it removes every
term of the double sum except those on the diagonal $i = j$.

Now move to the continuous setting — a particle on the real line, where
the "basis" is indexed by a continuous label $x \in \mathbb R$ rather
than an integer $i$. We would like an analogue of the Kronecker delta:
some object $\langle x | y \rangle$ that selects the diagonal $x = y$
inside an *integral* instead of a sum. The rest of the post shows that
this object is forced to be the Dirac delta $\delta(x - y)$, and says
precisely in what sense.

## The inner product of two continuous superpositions

Start where the last post left off: with honest vectors. A state
with $n$ possible outcomes was a vector with $n$ coordinates,

$$
|\psi\rangle = \sum_{i=1}^{n} a_i\, |E_i\rangle, \qquad a_i = \langle E_i | \psi \rangle,
$$

and the list $(a_1, \dots, a_n)$ is all there is to know about it. Look
at that list as a *function*: it assigns a number to each index, so a
vector in $\mathbb C^n$ is a function $\{1, \dots, n\} \to \mathbb C$,
and the expansion above just says "coordinates times unit vectors".
Now let the menu grow. More outcomes — a longer list, still one
coordinate per index. A continuum of outcomes — one index per real
number $x$ — and the list of coordinates *is* a function on the line.
That is the whole insight: **a vector with a continuum of coordinates
is a function**, and the function is what the last post called the
wavefunction, $a(x) = \langle x | \psi \rangle$.

![A vector is a list of coordinates indexed by i; as the index runs over the real line, the list becomes a function — the wavefunction](coords_to_function.png)

With that in mind, take two states written the way the last post
wrote them,

$$
|\psi\rangle = \int a(x)\, |x\rangle\, dx, \qquad |\varphi\rangle = \int b(y)\, |y\rangle\, dy
$$

(we write $a$ and $b$ rather than $\psi$ and $\varphi$ to keep the two
states apart). Each formula is the same statement as the finite one,
"coordinates times unit vectors", with the sum over indices turned
into an integral; the state and its wavefunction are one object. We
assume $a$ and $b$ continuous and square-integrable,
$\int |a(x)|^2\, dx \lt \infty$. Square-integrable functions on the
line, with the inner product $\langle a | b \rangle = \int a(x)^* b(x)\, dx$,
form the Hilbert space $L^2(\mathbb R)$ that the
[last post](/posts/states-are-vectors/#when-the-menu-is-infinite)
introduced as the state space of a particle on a line; so the
assumption just says that $a$ and $b$ are honest states, and it
guarantees that $\int a^* b\, dx$ converges (by the
[Cauchy–Schwarz inequality](https://en.wikipedia.org/wiki/Cauchy%E2%80%93Schwarz_inequality))
and that every sum below is finite.

What *is* exotic in these formulas is the unit vectors. The ket
$|x\rangle$ — "a $1$ at index $x$ and $0$ everywhere else" — is not a
function on the line at all, as the rest of the post will show, and
$\langle x | y \rangle$, the inner product of two such objects, is
exactly what we are after. The plan: compute
$\langle \psi | \varphi \rangle$ by discretizing each integral into a
Riemann sum, and take the limit at the very end.

So we discretize. Lay down a **grid** on the line: sample points
$x_1, x_2, \dots$ a fixed spacing $\Delta x$ apart — and keep only the
kets $|x_i\rangle$ at the grid points. On any bounded stretch of the
line these are finitely many, and we *declare* them to be the axes.
Replacing the integral by its Riemann sum over this grid gives the
**discretized states**

$$
|\psi_\Delta\rangle = \sum_i a(x_i)\, |x_i\rangle\, \Delta x, \qquad |\varphi_\Delta\rangle = \sum_j b(y_j)\, |y_j\rangle\, \Delta y
$$

— finite linear combinations of kets, so everything we do with them is
the finite-dimensional linear algebra of the last post. Every limit
$\Delta x \to 0$ in this post will be a limit of *numbers* computed
from these finite sums, never a limit of kets.

![The position kets form a continuum, one per real number; a grid keeps finitely many of them and declares them the axes; the Riemann sum of the integrand over the grid is the discretized state](continuum_grid.png)

Compute the inner product of the two finite sums. By linearity in the
second slot and anti-linearity in the first — the two properties from
the last post — the sums come out of the bracket and the scalars come
out of the slots, the first-slot ones conjugated:

$$
\begin{aligned}
\langle \psi_\Delta | \varphi_\Delta \rangle &= \Big\langle \sum_i a(x_i)\, |x_i\rangle\, \Delta x \;\Big|\; \sum_j b(y_j)\, |y_j\rangle\, \Delta y \Big\rangle \\
&= \sum_i \sum_j a(x_i)^* \, b(y_j)\, \langle x_i | y_j \rangle\, \Delta x\, \Delta y.
\end{aligned}
$$

The kets $|x_i\rangle$ and $|y_j\rangle$ have fused into a single
scalar, $\langle x_i | y_j \rangle$. Call it the **kernel** of the
double sum,

$$
K_\Delta(x_i, y_j) := \langle x_i | y_j \rangle,
$$

and the main question of the post is: what is the kernel?

## A dead end: the naive Kronecker guess

It is tempting to say the kernel is just the Kronecker delta,
$\langle x_i | y_j \rangle \overset{?}{=} \delta_{ij}$ — the grid
kets are orthonormal, as any decent basis should be. Let us see where
that leads. The $\delta_{ij}$ collapses the $j$-sum:

$$
\sum_i \sum_j a(x_i)^* \, b(y_j)\, \delta_{ij}\, \Delta x\, \Delta y = \sum_i a(x_i)^* \, b(x_i)\, \Delta x\, \Delta y.
$$

We are free to choose the grids, so take the same grid for both
states, $\Delta y = \Delta x$ with the same sample points. Then:

$$
\sum_i a(x_i)^* \, b(x_i)\, \Delta x\, \Delta x = \left( \sum_i a(x_i)^* \, b(x_i)\, \Delta x \right) \cdot \Delta x.
$$

<details>
<summary>Why one grid for both states is not a restriction</summary>

It is a choice of how we write the states, not an assumption about
them: $x$ and $y$ are two names for the same line, the kets
$|x_i\rangle$ and $|y_j\rangle$ are one and the same family, and
using one grid for both is the continuous counterpart of expanding
both vectors in the *same* orthonormal basis — which the last post's
coordinate formula $\langle \psi | \varphi \rangle = \sum_i a_i^* b_i$
required too. Nothing would break with two different grids, either:
take their *common refinement* — the grid whose cut points are all
the cut points of both (when the spacings are commensurable, simply
the grid of which both are multiples). Every cell of either original
grid is a union of cells of the refined one, so both Riemann sums can
be rewritten over the single refined grid, and we are back to the
case in the text — with a Riemann integral as the limit either way,
since the limit does not depend on the grid that produced it.

![Two grids of different spacing and a common refinement of which both are multiples: every cell of either grid is a union of refined cells](common_refinement.png)

</details>

Two factors remain: a Riemann sum, and a leftover $\Delta x$. As
$\Delta x \to 0$ the Riemann sum approaches the finite number
$\int a(x)^* \, b(x)\, dx$ — but it is multiplied by that extra
$\Delta x$, which goes to zero. The whole expression converges to
zero:

$$
\left( \sum_i a(x_i)^* \, b(x_i)\, \Delta x \right) \cdot \Delta x \;\xrightarrow{\;\Delta x \to 0\;}\; 0.
$$

The naive guess is a dead end: with $\langle x_i | y_j \rangle = \delta_{ij}$,
*every* pair of states has inner product zero in the limit — including
a state with itself, so every state has length zero. Here is the same
dead end numerically, next to the fix we are about to find:

![The inner product of two discretized states as the grid is refined: with the kernel δ_ij it decays to zero, with δ_ij/Δx it converges to the integral](two_kernels.png)

<details>
<summary>A fully rigorous Riemann sum</summary>

Above we treated $\sum_i a(x_i)^* \, b(x_i)\, \Delta x$ as a Riemann
sum over the whole line. Strictly, a Riemann sum lives on a *bounded*
interval: pick a finite window, partition it into cells, sample the
function in each cell. Let us redo the computation exactly that way,
with every step an explicit estimate.

Work on the window $[-A, A]$ split into $2N$ equal cells, so the
spacing is $\Delta x = A / N$ and the sample points are
$x_i = i \, \Delta x$ for $i = -N, \dots, N$. The kets are taken
genuinely orthonormal, $\langle x_i | x_j \rangle = \delta_{ij}$.
Since $a, b$ are continuous they are bounded on the window:
$|a(x)|, |b(x)| \leq M$ for some constant $M$. Each coefficient
carries one factor of the spacing,

$$
|\psi_\Delta\rangle = \frac{A}{N} \sum_{i=-N}^{N} a(x_i)\, |x_i\rangle, \qquad |\varphi_\Delta\rangle = \frac{A}{N} \sum_{j=-N}^{N} b(y_j)\, |y_j\rangle,
$$

and the inner product is

$$
\begin{aligned}
\langle \psi_\Delta | \varphi_\Delta \rangle &= \frac{A^2}{N^2} \sum_{i=-N}^{N} \sum_{j=-N}^{N} a(x_i)^* \, b(y_j)\, \delta_{ij} \\
&= \frac{A^2}{N^2} \sum_{i=-N}^{N} a(x_i)^* \, b(x_i) =: S_N.
\end{aligned}
$$

Bound $S_N$ term by term: each of the $2N + 1$ terms is at most $M^2$
in absolute value, so

$$
|S_N| \leq \frac{A^2}{N^2} \cdot (2N + 1) \cdot M^2 \;\xrightarrow{\; N \to \infty \;}\; 0.
$$

About $2N$ bounded terms against a $1/N^2$ prefactor: the sum goes to
zero. $\square$

</details>

## Normalizing the basis

The dead end is not a failure of the limit machinery. The limit worked
flawlessly and reported, correctly, that the state we built converges
to zero. We did not compute the right state wrongly — we
**discretized the wrong state**.

Which discrete state is the right one? The failed guess showed that
we do not actually know the inner products of the original kets:
assuming $\langle x_i | x_j \rangle = \delta_{ij}$ led to zero. So let
us build the state from a basis we *define* to be orthonormal, and let
the physics fix the coefficients. Introduce a new symbol: let
$|\hat x_i\rangle$ be the orthonormal **cell states**,
$\langle \hat x_i | \hat x_j \rangle = \delta_{ij}$, where
$|\hat x_i\rangle$ means "the particle is somewhere in cell $i$" — a
cell of width $\Delta x$ around $x_i$. As a wavefunction this is the
flat bump on the cell, scaled to unit norm:

$$
\hat x_i(x) = \begin{cases} 1/\sqrt{\Delta x} & |x - x_i| \leq \Delta x / 2 \\ 0 & \text{otherwise} \end{cases}
$$

Orthonormality is read off directly: different cells have disjoint
supports, so the product of two different cell states vanishes
everywhere and $\langle \hat x_i | \hat x_j \rangle = 0$ for
$i \neq j$, while
$\langle \hat x_i | \hat x_i \rangle = \int |\hat x_i|^2\, dx = \Delta x \cdot \frac{1}{\Delta x} = 1$.
(This way of building a continuous basis from a lattice of cells is
how Shankar's *Principles of Quantum Mechanics* introduces
infinite-dimensional state spaces, §1.10; see the references.)

![The cell states as wavefunctions: flat bumps of height 1/√Δx on disjoint cells — orthonormal by inspection; a state written in them has amplitudes a(x_i)√Δx](cell_states.png)

<details>
<summary>Which $L^2$, and who lives in it</summary>

There is only one space in play. The state
space of a particle on a line is $L^2(\mathbb R)$ — complex-valued
functions $\psi$ on the line with $\int |\psi(x)|^2\, dx \lt \infty$,
with the inner product $\int \psi^* \varphi\, dx$ of the last post. Strictly
speaking the state space is an abstract Hilbert space $\mathcal H$,
and the **position representation** is the unitary map
$\mathcal H \to L^2(\mathbb R)$, $|\psi\rangle \mapsto \psi(x) = \langle x | \psi \rangle$,
which sends each ket to its wavefunction; as everyone does, we
*identify* a ket with its image. So "the ket $|\psi\rangle$ lies in
$L^2$" means "its wavefunction $\psi$ is square-integrable on the
line", and a ket and its wavefunction are one element written two
ways.

So, in the formula $|\psi\rangle = \int \psi(x)\, |x\rangle\, dx$, who
lives in $L^2$? The state $|\psi\rangle$, i.e. the function $\psi$ —
nothing else. The cell states $|\hat x_i\rangle$ live there too: their
wavefunction $\hat x_i(x)$ is defined on the whole line — $1/\sqrt{\Delta x}$
on the cell, zero everywhere else — a step function with finite
support, and the computation above gives it norm one. The grid kets
$|x_i\rangle = |\hat x_i\rangle / \sqrt{\Delta x}$ still do, but
barely: their wavefunction is the spike of height $1/\Delta x$ on the
cell — the very kernel $K_\Delta$ of this post — and its squared norm
is $\Delta x \cdot (1/\Delta x)^2 = 1/\Delta x$, which grows without
bound as the grid is refined. And the limiting ket $|x\rangle$ is not
in $L^2$ at all: its wavefunction would have to be
$\langle y | x \rangle = \delta(y - x)$ as a function of $y$, and that
is not a function — as the rest of the post shows, it is defined only
by what it does inside integrals.

</details>

Write the discretized state as

$$
|\psi_\Delta\rangle = \sum_i c_i\, |\hat x_i\rangle,
$$

so that, by the last post's Born rule, $|c_i|^2$ is the probability of
finding the particle in cell $i$. (Note that, unlike $|x\rangle$, the
cell states are honest elements of $L^2$ — a cell state is the
indicator function of its cell, normalized — and the grid is not a
"countable subset of the continuous basis" but a replacement for it.
Taken over all grids at once, the cell states form a countable family
whose linear combinations, the step functions, are dense in $L^2$:
that density is the separability of $L^2$ the last post promised, and
it is why discretization can approximate every state — see Rudin's
*Real and Complex Analysis*, Theorem 3.13, and Kolmogorov–Fomin,
chapter VIII, §51–52, in the references.) Now the physics: the squared
wavefunction $|a(x)|^2$ is a probability **density** — probability per
unit length — so the probability of landing in a cell of width
$\Delta x$ is the density times the width:

$$
|c_i|^2 = |a(x_i)|^2\, \Delta x \quad \Longrightarrow \quad c_i = a(x_i)\, \sqrt{\Delta x}.
$$

![Cut the line into cells: the probability of a cell is the density times its width, so the amplitude of the cell state carries a square root of the width](cells.png)

(This also diagnoses the dead end. The naive coefficients
$c_i = a(x_i)\, \Delta x$ correspond to cell probabilities
$|a(x_i)|^2\, \Delta x^2$, and the total probability
$\sum_i |a(x_i)|^2\, \Delta x^2 = \Delta x \sum_i |a(x_i)|^2\, \Delta x$
goes to zero with $\Delta x$: the naive state was not normalized, and
its norm was draining away with the grid.)

Now we can finally say what the $|x_i\rangle$ of the original Riemann
sum is. We have two expressions for the same discretized state: the
Riemann-sum notation $\sum_i a(x_i)\, |x_i\rangle\, \Delta x$ we
adopted at the start, with the normalization of $|x_i\rangle$ left
open, and the expansion $\sum_i a(x_i)\, \sqrt{\Delta x}\; |\hat x_i\rangle$
we just derived. Both run over the same cells, so for them to describe
the same state the terms must agree cell by cell:

$$
a(x_i)\, |x_i\rangle\, \Delta x = a(x_i)\, \sqrt{\Delta x}\; |\hat x_i\rangle \quad \Longrightarrow \quad |x_i\rangle = \frac{1}{\sqrt{\Delta x}}\, |\hat x_i\rangle.
$$

So $|x_i\rangle$ was never an independent object that got rescaled. It
is *determined* by this equation: the unique ket that makes the
Riemann-sum notation — and its limit $\int a(x)\, |x\rangle\, dx$ —
describe the correctly normalized state. With this identification the
kernel becomes

$$
\langle x_i | y_j \rangle = \frac{1}{\Delta x}\, \langle \hat x_i | \hat x_j \rangle = \frac{\delta_{ij}}{\Delta x},
$$

carrying a factor $1/\Delta x$ that cancels the leftover $\Delta x$ of
the dead end. This is the correctly normalized kernel:

$$
\boxed{\; \langle x_i | y_j \rangle = \frac{\delta_{ij}}{\Delta x} \;}
$$

One consequence deserves to be said out loud now, because the rest of
the road will keep meeting it. The norm of a grid ket is
$\lVert\, |x_i\rangle \,\rVert = 1 / \sqrt{\Delta x}$, and it
**diverges** as $\Delta x \to 0$. Whatever the limiting objects
$|x\rangle$ are, they are not unit vectors, not normalizable vectors,
not elements of the Hilbert space at all. That is why "basis" has been
in scare quotes since the first paragraph.

Does this contradict the last post, where the space of states was
declared a Hilbert space? No — and the distinction is worth stating
carefully, because it will recur. The space of states is still the
Hilbert space $L^2$ of square-integrable wavefunctions: every physical
state $|\psi\rangle$, every honest superposition, lives there. But
$|x\rangle$ is **not a state** — and, in particular, no state
$|\psi\rangle$ can be equal to a single $|x_0\rangle$. Suppose it
were: its wavefunction would be $\psi(x) = \langle x | x_0 \rangle = \delta(x - x_0)$,
and $\langle \psi | \psi \rangle = \int |\delta(x - x_0)|^2\, dx$ is
not even a divergent integral, it is an undefined expression — the
delta cannot be squared. What *can* be prepared is a state
concentrated *near* $x_0$: a narrow bump of width $\sigma$, say a
Gaussian, which is an honest element of $L^2$ for every $\sigma \gt 0$.
But as $\sigma \to 0$ these states converge to nothing in $L^2$ — the
normalized bumps have no limit in the norm — so "exactly at $x_0$" is
not a rare state but a nonexistent one, approachable to any precision
and never reached. This is a genuine difference from the discrete
menus of the first two posts, where every outcome had a state of its
own ($|u\rangle$, $|d\rangle$): for a continuous menu, a definite
outcome has no state, only approximations. Mathematically, then,
$|x\rangle$ is a *generalized vector*, an object of the same kind as the delta itself:
it exists only through what it does to honest states. The bra
$\langle x |$ is the functional "evaluate the wavefunction at $x$",
$\langle x | \psi \rangle = \psi(x)$, and this functional is *not* the
inner product with any element of $L^2$ — the last post's Riesz
theorem does not apply to it, because evaluation at a point is not a
bounded functional on $L^2$. So the "continuous basis" is a basis in a
generalized sense: every honest state has an expansion
$\int \psi(x)\, |x\rangle\, dx$ along it, while the "basis vectors"
themselves stand just outside the space. The rigorous home for this
arrangement is a *rigged Hilbert space* — a triple
$\Phi \subset \mathcal H \subset \Phi^*$ of nice test states, the
Hilbert space, and the generalized vectors, with $|x\rangle \in \Phi^*$
— which we name and do not build. The construction, and the theorem
that every honest state expands along generalized eigenvectors, are
due to Gelfand and Vilenkin (*Generalized Functions*, vol. 4); the
gentlest entry is de la Madrid's article on the role of the rigged
Hilbert space in quantum mechanics, which works it all out on one
solvable example — both are in the references.

This is also the first appearance of a theme the road will return to:
position is a measurable quantity whose menu of outcomes is a
continuum, and such quantities have "eigenvectors" that live just
outside the space of states. (The functional-analysis name for a menu
of this kind is a *continuous spectrum*; the box, the tunnel and the
hydrogen atom will show all three kinds — discrete, continuous, and
mixed.)

## Taking the limit

Substitute the normalized kernel into the double sum:

$$
\langle \psi_\Delta | \varphi_\Delta \rangle = \sum_i \sum_j a(x_i)^* \, b(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta x\, \Delta y.
$$

There are two ways to take the limit, and the difference between them
is the whole subtlety of the Dirac delta.

**Option A.** Do the $j$-sum with $\delta_{ij}$ first, on the grid
$\Delta y = \Delta x$:

$$
\sum_i \sum_j a(x_i)^* \, b(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta x\, \Delta y = \sum_i a(x_i)^* \, b(x_i)\, \Delta x \;\xrightarrow{\;\Delta x \to 0\;}\; \int a(x)^* \, b(x)\, dx.
$$

The $1/\Delta x$ cancelled exactly one of the two spacings, leaving a
single honest Riemann sum. This is the inner product of $L^2$ from the
last post — recovered, this time, from the kets.

**Option B.** Keep the double structure and take the limit of the
whole double sum as a *number*:

$$
L := \lim_{\substack{\Delta x \to 0 \\ \Delta y = \Delta x}} \; \sum_i \sum_j a(x_i)^* \, b(y_j)\, \underbrace{\frac{\delta_{ij}}{\Delta x}}_{K_\Delta(x_i,\, y_j)}\, \Delta x\, \Delta y.
$$

This limit exists — it is the limit of the very same double sum, so it
equals $\int a(x)^* \, b(x)\, dx$. But the summand has exactly the
shape of a double Riemann sum with kernel $K_\Delta$, so we would
*like* to write $L$ as a double integral against some limiting kernel:

$$
L \overset{?}{=} \iint a(x)^* \, b(y)\, K(x, y)\, dx\, dy.
$$

Comparing with Option A, such a $K$ would have to satisfy

$$
\iint a(x)^* \, b(y)\, K(x, y)\, dx\, dy = \int a(x)^* \, b(x)\, dx,
$$

for all $a$ and $b$ — it would have to select the diagonal of a double
integral, exactly as $\delta_{ij}$ selects the diagonal of a double
sum. Whether any object $K$ does this, and what *kind* of object it
would have to be, is the rest of the post.

## The limiting kernel is not a function

Fix the index $i$ — so the spike's location $x_i$ is fixed; call it
$x$ — and look at $K_\Delta(x_i, y_j) = \delta_{ij} / \Delta x$ as a
function of $y_j$: it equals $1/\Delta x$ at $y_j = x_i$ and $0$ at
every other grid point. A single spike of **width** $\Delta x$ and
**height** $1/\Delta x$, hence of **area**

$$
\text{width} \times \text{height} = \Delta x \cdot \frac{1}{\Delta x} = 1.
$$

As $\Delta x \to 0$ the width shrinks to zero, the height diverges,
and the area stays pinned at one. This is exactly the picture people
draw for the Dirac delta.

![The discrete kernel at a fixed x as the grid is refined: thinner, taller, area one](spikes.png)

So it is tempting to take the limit of $K_\Delta$ directly and call
the result $K(x, y)$. That does not work, and it is worth seeing why.
A pointwise limit would be a "function" that is $0$ everywhere except
at the single point $y = x$, where it is infinite. There is **no
ordinary function** like that: a function that is zero everywhere
except at one point has integral $0$, not $1$, because a single point
has no width and contributes no area. Taken literally, the spike is
not a legitimate function, and the naive pointwise limit does not
exist.

This is the key obstacle. The object we are reaching for is not a
function, so we cannot define $K(x, y)$ by its values. We fall back on
the definition from the introduction instead: the Dirac delta is
defined not by its values but by **what it does inside an integral** —
the sifting property. To identify $K$ with $\delta$ we will not take a
pointwise limit at all; we will show that $K$ *sifts*.

## Identifying the kernel: the sifting property, earned

The strategy: test the discrete kernel $K_\Delta$ against an arbitrary
continuous function $f$, evaluate as an honest finite sum, and take
the limit only at the end.

Fix a target point $x$ once and for all, and let $i$ be the index of
the grid cell containing $x$, so that $x_i$ is the grid point nearest
the target, $|x_i - x| \leq \Delta x$. The discrete analogue of
"integrating $f$ against $K$" is $f$ summed against $K_\Delta$ with
the spacing $\Delta y$; on our grid $\Delta y = \Delta x$, so the
$1/\Delta x$ and the $\Delta x$ cancel exactly, and the Kronecker
delta keeps only the $j = i$ term:

$$
\sum_j f(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta x = \sum_j f(y_j)\, \delta_{ij} = f(x_i).
$$

Now let $\Delta x \to 0$. The grid point $x_i$ is squeezed onto the
target, $|x_i - x| \leq \Delta x \to 0$, so by continuity of $f$ we
get $f(x_i) \to f(x)$:

$$
\lim_{\Delta x \to 0} \; \sum_j f(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta y = f(x).
$$

This holds for **every** continuous function $f$. It is exactly the
sifting property, stated in the only rigorous form available to us: as
a limit of numbers. We therefore *define* the notation
$\int f(y)\, K(x, y)\, dy$ to mean this limit, and with that reading

$$
\int f(y)\, K(x, y)\, dy = f(x) \qquad \text{for every continuous } f.
$$

An object satisfying the sifting property for all $f$ is, by
definition, the Dirac delta. We have therefore *earned* the
identification

$$
\boxed{\; K(x, y) = \delta(x - y) \;}
$$

and the spike features from before now follow as *consequences* of
sifting, not assumptions:

- **unit area** — set $f \equiv 1$, giving $\int \delta(x - y)\, dy = 1$;
- **concentration at $y = x$** — for any $f$ vanishing at $x$ the
  integral returns $f(x) = 0$, so $\delta$ feels nothing away from the
  diagonal.

This also closes Option B. Sifting in the $y$ variable collapses the
double integral into the single one,

$$
\iint a(x)^* \, b(y)\, \delta(x - y)\, dx\, dy = \int a(x)^* \, b(x)\, dx,
$$

which is exactly the condition we required of $K$. And it pays the
last post's second debt in the same breath: for the position kets,

$$
\langle x | y \rangle = \delta(x - y)
$$

— the continuous orthonormality relation, the thing that replaces
$\langle E_i | E_j \rangle = \delta_{ij}$ when the label of the basis
becomes a real number.

Note what we did **not** do: we never claimed the spikes converge as
functions. We tested against $f$, produced a limit of numbers, and
identified $K$ by its action. That is the only sense in which the
identification holds, and it has a name.

## Weak convergence

It is tempting to write

$$
\frac{\delta_{ij}}{\Delta x} \longrightarrow \delta(x - y),
$$

but read as an ordinary limit of functions this is wrong: the
pointwise limit of the spikes does not exist, and $\delta(x - y)$ is
not a function anyway. It is a **distribution** — an object defined
only by its action inside integrals. The correct statement is called
**weak convergence**: for every continuous function $f$, the *numbers*
$\sum_j f(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta y$ converge to
$f(x)$. That is the same tested sum, with the same conventions and the
same limit, as in the previous section. The arrow above is universally
used as shorthand for this statement, and now we know what it
abbreviates. It also has a classical name: in Gelfand and Shilov's
*Generalized Functions*, vol. 1, a sequence of functions $f_\nu$ is
called **delta-like** if its integrals over any interval stay bounded
and $\int_a^b f_\nu \to 1$ when $a \lt 0 \lt b$ and $\to 0$ otherwise —
and every delta-like sequence converges weakly to $\delta$ (chapter I,
§2.5). Our spikes, read as step functions of width $\Delta x$ and
height $1/\Delta x$ centered at $x$, satisfy both conditions on sight,
so the identification above is a special case of that theorem.

<details>
<summary>The physicist's version of the same construction: a very large box</summary>

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
normalization $\langle k | k' \rangle = \delta(k - k')$. It is this
post's construction with the roles of position and momentum
exchanged: the box plays the grid, $2\pi / L$ plays $\Delta x$, and
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

</details>

<details>
<summary>The same delta, the other way round — Part 1's road</summary>

The Fourier road's Part 1 met the delta as the limit of a shrinking
averaging window: a rectangle $\frac{1}{\tau} r_\tau(t)$ of width
$\tau$ and height $1/\tau$, area one, tested against a continuous
signal, with the sifting property proved by a mean-value argument as
$\tau \to 0$. Compare with today's spike: width $\Delta x$, height
$1/\Delta x$, area one, tested against a continuous $f$, sifting
proved by continuity as $\Delta x \to 0$. The two constructions are
the same construction with different motivation — one came from
*measuring* a signal through an instrument of finite resolution, the
other from *normalizing* a basis of finite resolution — and the same
fine print applies to both: the delta is not a function, and the
limits are weak. Analysis calls such families
[approximate identities](https://en.wikipedia.org/wiki/Mollifier);
the systematic theory of objects like $\delta$ is
[distribution theory](https://en.wikipedia.org/wiki/Distribution_(mathematics)),
which we name and do not rebuild.

</details>

## Summary

The Kronecker delta $\delta_{ij}$ and the Dirac delta $\delta(x - y)$
are one idea in two settings. The first selects the diagonal of a
double sum,

$$
\sum_i \sum_j a_i^* \, b_j\, \delta_{ij} = \sum_i a_i^* \, b_i;
$$

the second selects the diagonal of a double integral,

$$
\iint a(x)^* \, b(y)\, \delta(x - y)\, dx\, dy = \int a(x)^* \, b(x)\, dx.
$$

To get from the first to the second, the discrete kernel must be
rescaled by $1/\Delta x$, because that is the normalization a
continuous basis forces — the probability of a cell is a density times
a width, so the amplitude of a cell carries a square root of the
width — and the resulting spikes converge to $\delta(x - y)$ only in
the weak sense: not point by point, but through what they do to every
function they are integrated against. In short: the Dirac delta is
what the Kronecker delta becomes when a sum becomes an integral.

## Onward

Both debts of the last post are paid: $|x\rangle$ is the limit of the
normalized cell states, and $\langle x | y \rangle = \delta(x - y)$.
The road can now use the position basis with a clear conscience. Next
stop: measurable quantities finally get objects of their own —
observables as operators, eigenvalues as the menu of outcomes — and
the Born rule, taken on credit twice by now, is earned rather than
postulated.

## References

- G. Stefanucci, R. van Leeuwen. *Nonequilibrium Many-Body Theory of
  Quantum Systems*. Cambridge University Press, 2013 — chapter 1 makes
  the same passage from a discrete to a continuous basis, with the
  $1/\sqrt{\Delta x}$ normalization; and a
  [Physics Forums discussion](https://www.physicsforums.com/threads/going-from-kronecker-deltas-to-dirac-deltas.1064459/)
  of exactly that passage.
- N. Wheeler, [*Simplified production of Dirac delta function
  identities*](https://www.reed.edu/physics/faculty/wheeler/documents/Miscellaneous%20Math/Delta%20Functions/Simplified%20Dirac%20Delta.pdf)
  — the delta calculus, done by a physicist who minds the fine print.
- [*What exactly is Dirac's delta function?*](https://www.physicsforums.com/insights/what-exactly-is-diracs-delta-function/),
  a Physics Forums Insights article on the distributional definition.
- The same $1/\sqrt{\Delta x}$ trick in the wild, in four unrelated
  corners of physics:
  [Heisenberg–Langevin formalism for open circuit-QED systems](https://arxiv.org/abs/1711.05699)
  (appendix A.2),
  [exact asymptotic solutions to nonlinear Hawkes processes](https://arxiv.org/abs/2110.01523)
  (appendix A),
  [derivation of the four-wave kinetic equation in action-angle variables](https://arxiv.org/abs/1911.13057),
  and [discretized light-cone quantization](https://arxiv.org/abs/hep-ph/9910203).
- I. M. Gelfand, G. E. Shilov. *Generalized Functions, vol. 1:
  Properties and Operations*. Academic Press, 1964 (Russian original:
  И. М. Гельфанд, Г. Е. Шилов, *Обобщённые функции и действия над
  ними*, Физматгиз, 1959) — chapter I, §1.8 (weak convergence of
  generalized functions) and §2.5 (delta-like sequences).
- I. M. Gelfand, N. Ya. Vilenkin. *Generalized Functions, vol. 4:
  Applications of Harmonic Analysis*. Academic Press, 1964 (Russian
  original: И. М. Гельфанд, Н. Я. Виленкин, *Обобщённые функции, вып. 4:
  Некоторые применения гармонического анализа. Оснащённые гильбертовы
  пространства*, Физматгиз, 1961) — chapter I, §4 (pp. 133–161):
  generalized eigenvectors (§4.1), rigged Hilbert spaces (§4.2), and
  Theorem 5′ (§4.5, p. 161): a self-adjoint operator in a rigged
  Hilbert space has a complete system of generalized eigenvectors —
  the theorem behind $\int \psi(x)\, |x\rangle\, dx$.
- R. de la Madrid. [The role of the rigged Hilbert space in quantum
  mechanics](https://arxiv.org/abs/quant-ph/0502053). *European Journal
  of Physics* 26 (2005), 287–312 — a pedestrian introduction on one
  exactly solvable example; the place to see why $|x\rangle$ lives
  outside the Hilbert space and how Dirac's formalism is made rigorous.
- R. Shankar. *Principles of Quantum Mechanics*, 2nd ed. Plenum, 1994 —
  §1.10, "Generalization to infinite dimensions": a continuous basis
  built from a lattice of cells, with the Dirac delta emerging in the
  limit.
- W. Rudin. *Real and Complex Analysis*, 3rd ed. McGraw-Hill, 1987 —
  Theorem 3.13: simple functions are dense in $L^p$.
- A. N. Kolmogorov, S. V. Fomin. *Elements of the Theory of Functions
  and Functional Analysis*, vol. 2. Graylock, 1961 (Russian original:
  А. Н. Колмогоров, С. В. Фомин, *Элементы теории функций и
  функционального анализа*) — chapter VIII, §51 (dense subsets of
  $L^2$) and §52 (the separability of $L^2$); together with Sergeev's
  Theorem 20 (lecture V), separability is equivalent to the existence
  of a countable orthonormal basis.
- This blog's own first meeting with the delta:
  [Part 1 of the Fourier road](/posts/fourier-series-to-spectrogram-part-1/#an-honest-model-of-a-discrete-signal).
