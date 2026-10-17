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
into an integral; the state and its wavefunction are one object.

### What the coordinate objects must do

In the finite case the coordinates come out of the basis by a one-line
computation, which the
[last post](/posts/states-are-vectors/#coordinates-and-a-formula-for-the-identity-operator)
did: hit the expansion with a basis bra, and orthonormality collapses
the sum,

$$
\langle E_k | \psi \rangle = \sum_i a_i\, \langle E_k | E_i \rangle = \sum_i a_i\, \delta_{ki} = a_k.
$$

"Coordinates are inner products", and the Kronecker delta is what
makes it work. The continuum version of this is the one property we
ask of the position kets: that they return the coordinates of every
state the same way,

$$
\langle x | \psi \rangle = a(x) \qquad \text{for every state } |\psi\rangle.
$$

Expand $|\psi\rangle$ inside the bracket, and the requirement becomes a
statement about the unknown $\langle x | y \rangle$:

$$
a(x) = \int \langle x | y \rangle\, a(y)\, dy.
$$

Read it as the continuous twin of the Kronecker line above:
$\langle x | y \rangle$, as a function of $y$, must do inside an
integral what $\delta_{ki}$ does inside a sum — kill every contribution
except the one at $y = x$ and return the coordinate there. The sifting
property from the opening of the post is therefore not a definition
handed down from above; it is the *requirement* that the position kets
be a basis in the sense of the last post. We will call a ket with this
property a **coordinate object** for the point $x$.

### The inner product, assuming the coordinate objects exist

Suppose for a moment that such objects exist. Then the inner product
of our two states follows in one line. Expand only the bra, pull the
integral out of the first slot — anti-linearity, which conjugates $a$
— and apply the requirement to what remains:

$$
\langle \psi | \varphi \rangle = \Big\langle \int a(x)\, |x\rangle\, dx \;\Big|\; \varphi \Big\rangle = \int a(x)^*\, \langle x | \varphi \rangle\, dx = \int a(x)^*\, b(x)\, dx.
$$

This is the inner product of the
[space of square-integrable wavefunctions](/posts/states-are-vectors/#when-the-menu-is-infinite),
$L^2(\mathbb R)$, which the last post wrote down as
$\langle f | g \rangle = \int f^* g\, dx$ — now derived from the
requirement rather than declared. With $\varphi = \psi$ it gives the
norm, $\lVert a \rVert^2 = \int |a(x)|^2\, dx$, so a state must be
**square-integrable**, $\int |a(x)|^2\, dx \lt \infty$ (for a state the
length is in fact $1$: total probability one). Square-integrability
also guarantees that $\int a^* b\, dx$ converges (by the
[Cauchy–Schwarz inequality](https://en.wikipedia.org/wiki/Cauchy%E2%80%93Schwarz_inequality))
and that every sum below is finite. We assume $a$ and $b$ continuous
as well, which is what the Riemann sums need.

One step of the derivation was taken on trust. The last post allowed
a finite sum to come out of a bracket; here we let an *integral* of
kets come out. Nothing so far says that this is legitimate. The
construction below will make it so: it only ever takes integrals over
kets as limits of finite sums, and the finite sums come out of a
bracket by the last post's rule.

### Why the coordinate objects cannot be functions

What *is* exotic in all this is the unit vectors. Try to
write the ket $|x_0\rangle$ as a function of the index, the way we
just wrote states: "a $1$ at $x_0$ and $0$ everywhere else". That
function exists, but it is useless — its squared length
$\int |f|^2\, dx$ is zero, so in $L^2$ it is the zero vector, orthogonal
to everything, and no unit vector.

![The unit-vector problem: a 1 at one index is a unit vector in ℂ⁵; on the line the same recipe has zero length; what does the job is a spike of unit area, narrower and taller without a function as its limit](unit_vector_problem.png)

Nor does a repaired candidate help — a narrow bump of unit norm, say.
Any attempt of this kind fails for the same reason, and the reason is
general: no function whatsoever can satisfy the requirement. Recall
what it asks of $\langle x | y \rangle$:

$$
a(x) = \int \langle x | y \rangle\, a(y)\, dy \qquad \text{for every state } a.
$$

Suppose $\langle x | y \rangle$ were an ordinary function of two
variables, $K(x, y)$. The requirement would then read

$$
a(x) = \int K(x, y)\, a(y)\, dy \qquad \text{for every continuous } a,
$$

and this is impossible. Fix $x$ and take two continuous functions
$a_1$ and $a_2$ that are equal everywhere except on a tiny interval
of width $\varepsilon$ around $y = x$, where $a_2$ rises above $a_1$
by a narrow bump of height $1$.

![Two continuous test functions a₁ and a₂, equal outside a tiny interval of width ε around x, where a₂ rises by a bump of height 1; their difference is a tent of height 1 and width ε, with area at most ε](two_test_functions.png)

The left-hand sides differ by
$a_2(x) - a_1(x) = 1$. The right-hand sides differ by

$$
\int K(x, y)\, \big(a_2(y) - a_1(y)\big)\, dy,
$$

an integral over an interval of width $\varepsilon$ of a function
bounded by $\max |K|$ — at most $\varepsilon \cdot \max |K|$, which
goes to zero as the bump narrows. One side of the equation differs by $1$, the other by as little as we
like — and all we used about $K$ was that, being a function, it
assigns one finite value to every point of its domain, $y = x$
included, so it is bounded there. No function $K$ can satisfy the
requirement: returning $a(x)$ would take being "infinite with unit
area" at that single point, which a function by definition cannot be.

The object that actually does a
coordinate object's job is not a function at all, as the rest of the
post will show. Readers of the Fourier road
have met this exact predicament: in
[Part 1](/posts/fourier-series-to-spectrogram-part-1/#an-honest-model-of-a-discrete-signal)
the "perfect instrument" that reads off a signal's value at one
instant could not be a function either, and the Dirac delta had to
be built as a limit of averaging windows. Here the same object will
arrive from the opposite side.

### Building the coordinate objects from the finite-dimensional side

That opposite side is the finite-dimensional linear algebra of the
last post, where everything is a sum and nothing is exotic. The plan:
replace both integrals by Riemann sums, so that
$\langle \psi | \varphi \rangle$ becomes a finite computation and the
unknown becomes a finite table of numbers $\langle x_i | y_j \rangle$;
find which table satisfies the requirement in the limit; and read the
Dirac delta off that table's limit. Lay down a **grid** on the line: sample points
$x_1, x_2, \dots$ a fixed spacing $\Delta x$ apart — and keep only the
kets $|x_i\rangle$ at the grid points. On any bounded stretch of the
line these are finitely many, and we *declare* them to be the axes.
Replacing the integral by its Riemann sum over this grid gives the
**discretized states**

$$
|\psi_\Delta\rangle = \sum_i a(x_i)\, |x_i\rangle\, \Delta x, \qquad |\varphi_\Delta\rangle = \sum_j b(y_j)\, |y_j\rangle\, \Delta y
$$

We use the same grid for both states — the points $y_j$ are the
points $x_j$ and $\Delta y = \Delta x$; the second letter only keeps
the two sums apart. These are finite linear combinations of kets, so
everything we do with them is the finite-dimensional linear algebra of
the last post.

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
kets are orthonormal, as any decent basis should be. Nothing forbids
the guess: we showed above that no *function* $K(x, y)$ on the line
can be the kernel, but on the grid the kernel is a finite table of
numbers, and any table is a legitimate candidate. The test is what its
limit does.

Test the guess against the requirement: hit the discretized state
with a grid bra. The $\delta_{ij}$ keeps one term of the sum,

$$
\langle x_i | \psi_\Delta \rangle = \sum_j a(y_j)\, \delta_{ij}\, \Delta y = a(x_i)\, \Delta x \;\xrightarrow{\;\Delta x \to 0\;}\; 0,
$$

and the kets return coordinates that vanish as the grid is refined,
instead of $a(x_i)$. The inner product fares the same way: in the
double sum the $\delta_{ij}$ collapses the $j$-sum, and what remains is

$$
\langle \psi_\Delta | \varphi_\Delta \rangle = \left( \sum_i a(x_i)^* \, b(x_i)\, \Delta x \right) \cdot \Delta x \;\xrightarrow{\;\Delta x \to 0\;}\; 0
$$

— a Riemann sum, which tends to the finite number $\int a^* b\, dx$,
times a leftover $\Delta x$, which tends to zero. With
$\langle x_i | y_j \rangle = \delta_{ij}$, *every* pair of states has
inner product zero in the limit — including a state with itself, so
every state has length zero.

This is the unit-vector problem from the previous section, seen from
the grid. Read the table $\delta_{ij}$ as a function of $y$ for fixed
$x_i$: it is $1$ on the one cell containing $x_i$ and $0$ elsewhere,
and as the grid is refined it settles into exactly the function "$1$
at $y = x$, $0$ everywhere else" — the zero vector of $L^2$ from the
figure above. The guess failed because its limit is a function, and
we already knew that a function cannot do the job. Here is the same
dead end numerically, next to the fix we are about to find:

![The inner product of two discretized states as the grid is refined: with the kernel δ_ij it decays to zero, with δ_ij/Δx it converges to the integral](two_kernels.png)

## The right basis: cell states

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

Note that, unlike $|x\rangle$, the
cell states are honest elements of $L^2$ — a cell state is the
indicator function of its cell, normalized. This corrects a picture
the word "grid" may have suggested: the grid kets we are about to
build are not the kets $|x\rangle$ of the continuum picked out at the
grid points and declared orthonormal — that was the dead end, and
the function "$1$ at a point" behind it is the zero vector of $L^2$ —
but states spread over a whole cell of width $\Delta x$, which stand
in for the points only as $\Delta x \to 0$.

Write the discretized state in the cell states,

$$
|\psi_\Delta\rangle = \sum_i c_i\, |\hat x_i\rangle,
$$

where the coefficients $c_i$ are, as always in an orthonormal basis,
inner products — here the inner product of $L^2$:

$$
\begin{aligned}
c_i = \langle \hat x_i | \psi \rangle &= \int \hat x_i(y)^*\, a(y)\, dy \\
&= \frac{1}{\sqrt{\Delta x}} \int_{\text{cell } i} a(y)\, dy \\
&= a(\xi_i)\, \sqrt{\Delta x},
\end{aligned}
$$

the last step by the
[mean value theorem for integrals](https://en.wikipedia.org/wiki/Mean_value_theorem#Mean_value_theorems_for_definite_integrals):
for continuous $a$ the integral over the cell equals $a(\xi_i)\, \Delta x$
for some point $\xi_i$ of the cell. So the coordinate of a state along
a cell state is a sample of $a$ in the cell times $\sqrt{\Delta x}$.

This fixes the grid ket $|x_i\rangle$ of the original Riemann sum,
$|\psi_\Delta\rangle = \sum_i a(x_i)\, |x_i\rangle\, \Delta x$, whose
normalization was left open. Sample that sum at the points $\xi_i$
instead of $x_i$ — a Riemann sum may sample each cell anywhere — and
compare it with the expansion in cell states,
$|\psi_\Delta\rangle = \sum_i c_i\, |\hat x_i\rangle$ with
$c_i = a(\xi_i)\sqrt{\Delta x}$. Both describe the same state, so the
terms must agree cell by cell:

$$
\underbrace{a(\xi_i)\, \Delta x}_{\text{Riemann sum}}\; |x_i\rangle = \underbrace{a(\xi_i)\, \sqrt{\Delta x}}_{c_i}\; |\hat x_i\rangle \quad \Longrightarrow \quad |x_i\rangle = \frac{1}{\sqrt{\Delta x}}\, |\hat x_i\rangle.
$$

So the kernel is

$$
\langle x_i | y_j \rangle = \frac{1}{\Delta x}\, \langle \hat x_i | \hat x_j \rangle = \frac{\delta_{ij}}{\Delta x},
$$

with a factor $1/\Delta x$ that cancels the leftover $\Delta x$ of
the dead end:

$$
\boxed{\; \langle x_i | y_j \rangle = \frac{\delta_{ij}}{\Delta x} \;}
$$

Check it against the requirement first. Hit the discretized state with a
grid bra, as in the dead end:

$$
\langle x_i | \psi_\Delta \rangle = \sum_j a(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta y = a(x_i).
$$

The $1/\Delta x$ cancels the $\Delta y = \Delta x$ of the sum, and the
grid ket returns the sample of $a$ in its cell — $a(x_i)$ here, or
$a(\xi_i)$ with the other sampling — with no stray factor of
$\Delta x$ to drain it away as the grid is refined. Fix a target point
$x$ and let $\Delta x \to 0$: the cell containing $x$ shrinks onto it,
and the sample tends to $a(x)$ by continuity. That is the requirement,
$\langle x | \psi \rangle = a(x)$, met in the limit — and the
inner-product formula must now follow; the next section watches it
do so.

With the construction done, its physical reading: once squared amplitudes are read as
probabilities, $|c_i|^2 = |a(\xi_i)|^2\, \Delta x$ says that $|a(x)|^2$
is a probability **density** — probability per unit length — and the
probability of landing in a cell is the density times the width.

![Cut the line into cells: the probability of a cell is the density times its width, so the amplitude of the cell state carries a square root of the width](cells.png)

One consequence deserves to be said out loud now, because the rest of
the road will keep meeting it. The norm of a grid ket is
$\lVert\, |x_i\rangle \,\rVert = 1 / \sqrt{\Delta x}$, and it
**diverges** as $\Delta x \to 0$. Whatever the limiting objects
$|x\rangle$ are, they are not unit vectors, not normalizable vectors,
not elements of the Hilbert space at all. That is why "basis" has been
in scare quotes since the first paragraph.

Which space is meant here, and who exactly is in it, deserves a
precise statement before the physics of it:

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

*A remark to close the section, for readers who want the functional
analysis behind "discretization can approximate every state".*
Taken over all grids at once, the cell states form a countable family
whose linear combinations, the step functions, are dense in $L^2$:
that density is the separability of $L^2$ the last post promised, and
it is why discretization can approximate every state — see Rudin's
*Real and Complex Analysis*, Theorem 3.13, and Kolmogorov–Fomin,
chapter VIII, §51–52, in the references.

## Taking the limit

Before taking any, one rule governs everything that follows. When the
grid is refined, $\Delta x \to 0$, the only things we ask to converge
are *numbers* computed from the finite sums — the inner product
$\langle \psi_\Delta | \varphi_\Delta \rangle$, and later the sums that
test the kernel against a function. We never claim that the
discretized state $|\psi_\Delta\rangle$ converges to $|\psi\rangle$
as a vector: that would need a norm to converge in, and we have just
seen that the kets $|x_i\rangle$ cannot supply one — their norm
$1/\sqrt{\Delta x}$ runs away.

Substitute the normalized kernel into the double sum and do the
$j$-sum with $\delta_{ij}$ first:

$$
\langle \psi_\Delta | \varphi_\Delta \rangle = \sum_i \sum_j a(x_i)^* \, b(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta x\, \Delta y = \sum_i a(x_i)^* \, b(x_i)\, \Delta x \;\xrightarrow{\;\Delta x \to 0\;}\; \int a(x)^* \, b(x)\, dx.
$$

The $1/\Delta x$ cancelled exactly one of the two spacings, leaving a
single honest Riemann sum. This is the inner-product formula that the
requirement produced at the start — now reproduced by the kets, as it
had to be once the requirement held on the grid.

That settles the inner product, but not the kernel itself. We would
like to say what $K_\Delta = \delta_{ij} / \Delta x$ *converges to*,
and call that $\langle x | y \rangle$. Fix the index $i$ — so the
spike's location $x_i$ is fixed; call it $x$ — and look at
$K_\Delta(x_i, y_j)$ as a function of $y_j$: it equals $1/\Delta x$
at $y_j = x_i$ and $0$ at every other grid point. A single spike of
**width** $\Delta x$ and **height** $1/\Delta x$, hence of **area**

$$
\text{width} \times \text{height} = \Delta x \cdot \frac{1}{\Delta x} = 1.
$$

As $\Delta x \to 0$ the width shrinks to zero, the height diverges,
and the area stays pinned at one. This is exactly the picture people
draw for the Dirac delta.

![The discrete kernel at a fixed x as the grid is refined: thinner, taller, area one](spikes.png)

So it is tempting to take the limit of $K_\Delta$ pointwise and call
the result $K(x, y)$. But that limit would be "$0$ everywhere except
at the single point $y = x$, infinite there" — and the section on the
coordinate objects showed that no function can play this part: a
function has one finite value at $y = x$, and a single point has no
width to contribute an area. The object we are reaching for is not a
function, so we cannot define $K(x, y)$ by its values. We fall back on
the definition from the introduction instead: the Dirac delta is
defined not by its values but by **what it does inside an integral** —
the sifting property. To identify $K$ with $\delta$ we will not take a
pointwise limit at all; we will show that $K$ *sifts*.

## Identifying the kernel: the sifting property, earned

The strategy: test the discrete kernel $K_\Delta$ against an arbitrary
continuous function $f$, evaluate as an honest finite sum, and take
the limit only at the end. This is the check we ran on every grid
after building the cell states — $\langle x_i | \psi_\Delta \rangle = a(x_i)$ — with
the coordinate $a$ replaced by an arbitrary continuous $f$, and with
the limit taken at the end.

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

Sifting in the $y$ variable also collapses a double integral into a
single one,

$$
\iint a(x)^* \, b(y)\, \delta(x - y)\, dx\, dy = \int a(x)^* \, b(x)\, dx,
$$

— the diagonal of a double integral selected exactly as $\delta_{ij}$
selects the diagonal of a double sum. And it pays the
last post's second debt in the same breath: for the position kets,

$$
\langle x | y \rangle = \delta(x - y)
$$

— the continuous orthonormality relation, the thing that replaces
$\langle E_i | E_j \rangle = \delta_{ij}$ when the label of the basis
becomes a real number. And the kets we built are the **coordinate
objects** the section on the inner product asked for: with the
integral read as the limit above,
$\langle x | \psi \rangle = \int \langle x | y \rangle\, \psi(y)\, dy = \psi(x)$
for every state — the requirement we started from, now met.

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
other from *building* a basis of finite resolution — and the same
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
continuous basis forces — the coordinate of a state along a unit cell
state is an inner product over the cell, $a(x_i)\sqrt{\Delta x}$, so
the amplitude of a cell carries a square root of the width;
physically, the probability of a cell is a density times a width — and the resulting spikes converge to $\delta(x - y)$ only in
the weak sense: not point by point, but through what they do to every
function they are integrated against. In short: the Dirac delta is
what the Kronecker delta becomes when a sum becomes an integral.

The logic of the post hangs on one requirement: that the position kets
return coordinates, $\langle x | \psi \rangle = \psi(x)$, exactly as
an orthonormal basis does through $\delta_{ki}$. The $L^2$ inner
product followed from that requirement in one line; the grid
construction then built kets that satisfy it in the limit, and the
price of satisfying it — the $1/\Delta x$ — is what turned the
Kronecker delta into the Dirac delta.

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
