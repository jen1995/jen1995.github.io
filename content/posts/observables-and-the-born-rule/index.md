---
title: "Observables, and Where the Probabilities Come From"
date: 2026-10-18
draft: true
tags: ["quantum", "math"]
summary: "The measurable quantities of the first post finally get mathematical objects of their own: operators, whose eigenvalues are the menu of outcomes. Along the way the Born rule — probabilities are squared amplitudes — is derived rather than postulated, and two of the three Pauli matrices fall out of the spin experiments."
math: true
weight: 50
---

The [first post](/posts/the-apparatus-and-the-arrow/#the-wishlist) of
the quantum road ended with a wishlist. Items 1 and 2 — a state
object, and a way to blend outcomes into states — were paid in the
[second post](/posts/states-are-vectors/): states are unit vectors in
a Hilbert space, blends are superpositions. Item 3 has been waiting
since: *measurable quantities as actors, not numbers*. "Spin along
$\hat n$" is not a number attached to the electron; it is a question
with its own menu of answers, and the wishlist asked for a
mathematical object per question. Item 4, *measurement as an
operation on states*, is waiting with it.

There is also a debt. The second post took the
[Born rule](/posts/states-are-vectors/#what-the-geometry-means-physically)
on credit — "the probability of an outcome is the squared magnitude of
its amplitude" — and promised a derivation. The
[last post](/posts/from-kronecker-to-dirac/) borrowed it again in
passing. Today both are settled: the objects behind the questions are
**operators**, and the Born rule is forced, not chosen, by one
requirement — that probabilities must not depend on which basis we
happen to write a state in.

As in the second post, the spin of the first post does the explaining
first, and the general definitions follow it. The arrangement of the
principles, and the construction of the spin operators from the
experiments, follow lecture 3 of Susskind and Friedman's *Quantum
Mechanics: The Theoretical Minimum* (see the references); the
derivation of the Born rule follows the *Maths of Quantum Mechanics*
series by Quantum Sense.

## Where we stand

Three facts from the earlier posts are used throughout.

- A measurement along an axis has two outcomes, $+1$ and $-1$, and
  two **definite states** — the states that the measurement prepares
  and then confirms on every repetition. For the $z$ axis they are
  $|u\rangle$ and $|d\rangle$; for the $x$ axis, $|r\rangle$ and
  $|l\rangle$, which the
  [second post built](/posts/states-are-vectors/#the-machinery-earns-its-keep-right-and-left)
  from the experiments:

  $$
  |r\rangle = \tfrac{1}{\sqrt 2}\,|u\rangle + \tfrac{1}{\sqrt 2}\,|d\rangle, \qquad |l\rangle = \tfrac{1}{\sqrt 2}\,|u\rangle - \tfrac{1}{\sqrt 2}\,|d\rangle.
  $$

- Each axis donates an **orthonormal basis**: its two definite states
  are perfectly distinguishable by the apparatus, hence orthogonal,
  and normalized to length one. Any state expands in any of these
  bases, with coordinates that are inner products,
  $c_i = \langle E_i | \psi \rangle$.
- The outer product $|E_i\rangle\langle E_i|$ is a
  [projector](/posts/states-are-vectors/#coordinates-and-a-formula-for-the-identity-operator)
  onto the $i$-th basis direction, and the projectors of a basis add
  up to the identity: $\sum_i |E_i\rangle\langle E_i| = \hat I$.

What is missing is an object for the *question itself* — for "spin
along $z$" as opposed to its two answers.

## A question becomes an operator

Take the $z$ measurement. We know its menu of answers,
$+1$ and $-1$, and we know which state goes with which answer:
$|u\rangle$ with $+1$, $|d\rangle$ with $-1$. Encode this table
in a single machine $\sigma_z$ that takes a state and returns a
state, by declaring what it does to the two definite states —

$$
\sigma_z\, |u\rangle = (+1)\, |u\rangle, \qquad \sigma_z\, |d\rangle = (-1)\, |d\rangle
$$

— and extending to every other state by linearity:
$\sigma_z\,(\alpha |u\rangle + \beta |d\rangle) = \alpha |u\rangle - \beta |d\rangle$.
The machine multiplies each definite state by the number the window
would show, and acts on sums term by term.

![The operator σ_z as a machine: it returns |u⟩ unchanged, flips the sign of |d⟩, and sends the superposition |r⟩ to |l⟩ — a different state, not a measurement outcome](operator_machine.png)

In the language of linear algebra: a **linear operator** on a
vector space $V$ is a linear map $\hat A : V \to V$ — it sends vectors
to vectors and respects sums and scalar multiples,
$\hat A(\alpha |\psi\rangle + \beta |\varphi\rangle) = \alpha \hat A|\psi\rangle + \beta \hat A|\varphi\rangle$.
A nonzero vector $|v\rangle$ is an
[**eigenvector**](https://en.wikipedia.org/wiki/Eigenvalues_and_eigenvectors)
of $\hat A$ if the operator merely rescales it,

$$
\hat A\, |v\rangle = \lambda\, |v\rangle,
$$

and the number $\lambda$ is the corresponding **eigenvalue**. The set
of all eigenvalues of an operator is called its **spectrum**; for
continuous menus the word will mean more than a list of numbers. In this language the
definite states $|u\rangle, |d\rangle$ are the eigenvectors of
$\sigma_z$, and the outcomes $\pm 1$ are its eigenvalues.

That is the general recipe, and in quantum mechanics it is a
postulate — Susskind's principles 1 and 2:

> **Measurable quantities are operators.** To every measurable
> quantity $E$ corresponds a linear operator $\hat E$ on the space of
> states. The possible outcomes of measuring $E$ are the eigenvalues
> of $\hat E$; a state in which the outcome is certain to be $E_i$ is
> an eigenvector of $\hat E$ with eigenvalue $E_i$ — a **definite
> state** of $E$.

This is not a discovery but a *codification* of the
[first post's experiments](/posts/the-apparatus-and-the-arrow/#what-we-saw):
the menu of outcomes is fixed and discrete — the eigenvalues; a
measurement leaves the system in a state that repeats its answer — an
eigenvector; and a superposition of definite states is a state with
no certain answer — a vector that is not an eigenvector. From now on
the word **observable** is used both for the measurable quantity and
for its operator, written with a hat: $\hat E$ for energy, $\sigma_z$ for the
spin along $z$.

### Applying the operator is not measuring

The notation invites a confusion, so it is addressed before
anything else. Applying $\sigma_z$ to a state is a *mathematical*
operation that returns a state; a measurement is a *physical*
operation that returns a number and changes the state. They are not
the same thing.

Apply $\sigma_z$ to the $x$-definite state $|r\rangle$:

$$
\sigma_z\, |r\rangle = \tfrac{1}{\sqrt 2}\, \sigma_z |u\rangle + \tfrac{1}{\sqrt 2}\, \sigma_z |d\rangle = \tfrac{1}{\sqrt 2}\, |u\rangle - \tfrac{1}{\sqrt 2}\, |d\rangle = |l\rangle.
$$

The operator turned *right* into *left*. No $z$ measurement of an
electron prepared along $x$ ever produces an electron pointing left
along $x$: it produces $|u\rangle$ or $|d\rangle$, at random. So
$\sigma_z|r\rangle$ is not the state after a measurement. It is a *code*: written in the eigenbasis of $\sigma_z$, the input
$|r\rangle = \frac{1}{\sqrt 2}|u\rangle + \frac{1}{\sqrt 2}|d\rangle$
lists the possible answers as its basis directions, and the operator
has tagged each direction with the answer's value. How the
coefficients encode the *probabilities* of those answers is the next
section's whole subject. (Susskind and Friedman devote their §3.5, "A
common misconception", to this point.)

## What the operator of an observable must satisfy

Not every linear operator can stand for a measurable quantity. The
experiments impose three conditions, each with a one-line reason.

1. **The eigenvalues are real.** The window shows real numbers.
2. **The eigenvectors span the whole space.** Every state must expand
   as $|\psi\rangle = \sum_i c_i |E_i\rangle$ in the definite states
   of $E$. If some state had no such expansion, then measuring $E$ in
   that state would have no possible outcome at all — but the
   $|E_i\rangle$ were declared to cover every outcome there is.
3. **Distinct definite states are orthogonal.** $\langle E_i | E_j \rangle = 0$
   for $i \neq j$: the apparatus distinguishes them perfectly, and the
   second post identified perfect distinguishability with
   orthogonality.

Conditions 2 and 3 together, with the eigenvectors normalized to
length one, say in one phrase: **the definite states of an observable
form an orthonormal basis of the state space.** This is why every
measurement axis of the first post donated a basis — $\sigma_z$ owns
$\{|u\rangle, |d\rangle\}$, $\sigma_x$ owns $\{|r\rangle, |l\rangle\}$ —
and the rest of the post depends on it.

Two refinements. An eigenvalue may belong to more than one
independent eigenvector; the eigenvalue is then called
**degenerate**, and the measurement does not determine the state
uniquely — only the subspace it lands in. The hydrogen atom will
make this concrete: several orbitals share one energy. And in
infinite dimensions the spectrum of an operator need not be a list of
eigenvalues with eigenvectors inside the space. The position operator
of the last post is the first example — its "eigenvectors" $|x\rangle$
are the generalized vectors that live just outside $L^2$, and its
spectrum is the whole real line, a **continuous spectrum**. The
problems ahead show all three kinds: the particle in a box has a
purely discrete spectrum, the tunneling problem a purely continuous
one, and hydrogen both at once.

## The Born rule, earned

Expand a state in the definite states of an observable,

$$
|\psi\rangle = \sum_i c_i\, |E_i\rangle, \qquad c_i = \langle E_i | \psi \rangle,
$$

and ask the question the second post postponed: what is the
probability $P_i$ of observing the outcome $E_i$? The coefficient
$c_i$ measures how much of $|E_i\rangle$ is in $|\psi\rangle$, so
$P_i$ should be some function of it, $P_i = f(c_i)$ — the same
function for every outcome and every observable, since nothing in the
formalism singles one out. The task is to find $f$.

### The obvious guess fails

Take real coefficients first, in two dimensions, and try the simplest
guess: the probability is the magnitude, $P_i = |c_i|$, so that
$|c_1| + |c_2| = 1$. For the fifty-fifty state this gives
$c_1 = c_2 = \frac12$. Now write the *same* state in another
orthonormal basis — one obtained by rotating the first, which is what
a different measurement axis does. In the rotated basis the
coordinates of the vector $(\frac12, \frac12)$ are, say,
$(\frac{1}{\sqrt{10}}, -\frac{2}{\sqrt{10}})$, and the sum of
magnitudes is no longer one:

$$
\tfrac{1}{\sqrt{10}} + \tfrac{2}{\sqrt{10}} = \tfrac{3}{\sqrt{10}} \approx 0.95.
$$

The coefficients in the new basis no longer add up to a probability
distribution, and the vector would have to be rescaled by hand every
time the basis changes. But the state is the same physical state
whichever apparatus we point at it; a rule that needs a
rescaling depending on the basis cannot be a law about the state.

![The same state vector in two orthonormal bases: the sum of the magnitudes of its coordinates changes with the basis, while the sum of their squares — the squared length — does not](born_counterexample.png)

What *is* the same in every orthonormal basis is the length of the
vector. The second post normalized states to length one, and in any
orthonormal basis that reads $\sum_i c_i^2 = 1$ (real case). Whatever
$f$ is, it has to produce a probability distribution on every unit
vector, in every orthonormal basis, using only the coordinates.

### Three conditions and a differential equation

Write down what we know about $f$, for real coefficients.

1. **Normalization.** $\sum_i f(c_i) = 1$ for every unit vector, i.e.
   whenever $\sum_i c_i^2 = 1$.
2. **A single function.** The same $f$ serves every coordinate, every
   basis, every observable.
3. **Sign does not matter.** $f(-c) = f(c)$: the state $-|\psi\rangle$
   is the same physical state as $|\psi\rangle$ (the second post:
   a unit scalar factor changes no measurement), so flipping the sign
   of one coordinate cannot change a probability.

Condition 1 is a constraint on $n$ numbers tied by one equation. Solve
the tie for the last coordinate, $c_n = \sqrt{1 - \sum_{i \lt n} c_i^2}$
(condition 3 lets us take the positive root), and condition 1 becomes
an identity in the $n - 1$ *independent* variables $c_1, \dots, c_{n-1}$:

$$
\sum_{i=1}^{n-1} f(c_i) + f\!\left(\sqrt{1 - \textstyle\sum_{i=1}^{n-1} c_i^2}\right) = 1.
$$

An identity in independent variables can be differentiated with
respect to any of them. Differentiate with respect to $c_1$ (assume
$f$ differentiable; this is the argument's technical assumption):

$$
f'(c_1) - f'(c_n)\, \frac{c_1}{c_n} = 0 \qquad\Longrightarrow\qquad \frac{f'(c_1)}{c_1} = \frac{f'(c_n)}{c_n}.
$$

Differentiating with respect to $c_2$ instead gives the same
right-hand side, so

$$
\frac{f'(c_1)}{c_1} = \frac{f'(c_2)}{c_2}
$$

for all admissible values of two independent variables. A function of
$c_1$ alone that equals a function of $c_2$ alone is a constant:

$$
\frac{f'(c)}{c} = \lambda \qquad\Longrightarrow\qquad f(c) = \frac{\lambda}{2}\, c^2 + \mu.
$$

Two physical boundary conditions fix the constants. A state with
$c_i = 0$ has no component along $|E_i\rangle$ at all — it is
orthogonal to it, hence perfectly distinguishable from it — so the
outcome $E_i$ never occurs: $f(0) = 0$, and $\mu = 0$. A state with
$c_i = 1$ *is* $|E_i\rangle$, the definite state, and the first post's
experiment one says its outcome is certain: $f(1) = 1$, so
$\lambda = 2$. Therefore

$$
f(c) = c^2 .
$$

### Complex coefficients

The coefficients are complex in general, and the argument above was
for real ones. One observation extends it. The definite state
$|E_i\rangle$ is fixed by the physics only up to a unit factor: the
vector $e^{i\theta}|E_i\rangle$ is the same physical state, is still
an eigenvector with the same eigenvalue, and still has length one. So
$\{e^{i\theta_i}|E_i\rangle\}$ is just as good an eigenbasis of the
same observable, and in it the coordinates of $|\psi\rangle$ are
$e^{-i\theta_i} c_i$. The probabilities cannot know which of these
bases was used; hence $f$ depends on $c_i$ only through its magnitude
$|c_i|$. Apply the real result to the nonnegative numbers $|c_i|$,
which satisfy $\sum_i |c_i|^2 = 1$, and:

> **The Born rule.** If $|\psi\rangle = \sum_i c_i |E_i\rangle$ in the
> orthonormal eigenbasis of an observable, the probability that a
> measurement of that observable returns $E_i$ is
> $$P(E_i) = |c_i|^2 = |\langle E_i | \psi \rangle|^2 .$$

Squared magnitudes, because the squared length is the quantity that
does not change between orthonormal bases. The rule is the only assignment of probabilities to coordinates that
does not depend on the basis the coordinates are taken in. The
argument assumed a differentiable $f$ that is the same for every
coordinate; the theorem that removes those assumptions — for state
spaces of dimension three and more, any probability assignment that is
additive over orthonormal bases is of this form — is
[Gleason's theorem](https://en.wikipedia.org/wiki/Gleason%27s_theorem)
(1957), in the references.

### The continuous menu

For a particle on a line the definite states of position are the kets
$|x\rangle$ of the last post, the expansion is
$|\psi\rangle = \int \psi(x)\,|x\rangle\,dx$, and the "coordinates"
$\psi(x) = \langle x | \psi \rangle$ are a function. The Born rule
carries over with one change of wording, which the last post's grid
makes exact. Cut the line into cells of width $\Delta x$; the cell
states $|\hat x_i\rangle$ are an orthonormal basis of $L^2$, and the
coordinate of $|\psi\rangle$ along the cell containing $x_i$ is
$c_i = \psi(\xi_i)\sqrt{\Delta x}$ for a point $\xi_i$ of the cell. By
the Born rule the probability of finding the particle in that cell is

$$
|c_i|^2 = |\psi(\xi_i)|^2\, \Delta x ,
$$

a density times a width. So $|\psi(x)|^2$ is a **probability
density** — probability per unit length — and the probability of
finding the particle in an interval is its integral over the
interval,

$$
P(a \leq x \leq b) = \int_a^b |\psi(x)|^2\, dx,
$$

with total probability $\int |\psi|^2\,dx = 1$, the normalization of
the state.

![The Born rule on the line: |ψ(x)|² is a probability density, and the probability of a cell of width Δx is the density times the width](born_density.png)

## Expectation values

The first post wrote the average of many measurements as
$\langle \sigma \rangle$ and called it Dirac's bracket notation,
promising an explanation. With the probabilities in hand,
the statistical average of the outcomes of $E$ in the state
$|\psi\rangle$ is

$$
\langle E \rangle = \sum_i P(E_i)\, E_i = \sum_i |c_i|^2\, E_i .
$$

Now compute a different-looking quantity: sandwich the operator
between the bra and the ket of the state. Using $\hat E|E_j\rangle = E_j|E_j\rangle$
and orthonormality,

$$
\begin{aligned}
\langle \psi | \hat E | \psi \rangle &= \Big( \sum_i c_i^* \langle E_i| \Big)\, \hat E\, \Big( \sum_j c_j |E_j\rangle \Big) = \sum_{i,j} c_i^* c_j\, E_j\, \langle E_i | E_j \rangle \\
&= \sum_i |c_i|^2\, E_i .
\end{aligned}
$$

The two agree:

$$
\boxed{\; \langle E \rangle = \langle \psi | \hat E | \psi \rangle \;}
$$

The bracket of the first post is this sandwich: the operator between
the state and itself.

Check it against the number the first post measured. Prepare
$|r\rangle$ — spin $+1$ along $x$ — and measure along $z$, at $90°$ to
the preparation. The first post's cosine predicts an average of
$\cos 90° = 0$. Compute:

$$
\langle r | \sigma_z | r \rangle = \langle r | l \rangle = 0 ,
$$

using $\sigma_z|r\rangle = |l\rangle$ from above and
$\langle r | l \rangle = 0$. The formalism returns the right average
for this angle. The full $\cos\theta$, for an arbitrary angle between
the axes, needs the spin operators for arbitrary directions, which
the next post constructs.

## Hermitian operators

Which operators satisfy the three conditions — real spectrum,
orthonormal eigenbasis? The answer is a named class of operators, and it needs one new
notion: moving an operator from one side of the bracket to the other.

### The adjoint

Write $|\hat M\psi\rangle$ for the vector that $\hat M$ returns when
fed $|\psi\rangle$, so that the sandwich reads
$\langle \varphi | \hat M | \psi \rangle = \langle \varphi | \hat M \psi \rangle$:
the operator acts on the ket. We want to be able to let it act on the
*bra* instead. For an operator $\hat M$, its
[**adjoint**](https://en.wikipedia.org/wiki/Hermitian_adjoint)
(Hermitian conjugate) $\hat M^\dagger$ is the operator for which this holds:

$$
\langle \varphi | \hat M \psi \rangle = \langle \hat M^\dagger \varphi | \psi \rangle \qquad \text{for all } |\varphi\rangle, |\psi\rangle .
$$

In finite dimensions it exists and is unique (the second post's Riesz
theorem gives it: for fixed $|\varphi\rangle$ the left side is a
linear functional of $|\psi\rangle$, hence an inner product with a
unique vector, which we name $\hat M^\dagger|\varphi\rangle$). Three
rules follow from the definition:
$(\hat A^\dagger)^\dagger = \hat A$,
$(\hat A + \hat B)^\dagger = \hat A^\dagger + \hat B^\dagger$,
$(\hat A \hat B)^\dagger = \hat B^\dagger \hat A^\dagger$. For a
scalar, the adjoint is the complex conjugate: $(c\,\hat I)^\dagger = c^*\hat I$.
And the adjoint of a ket is its bra, $(|v\rangle)^\dagger = \langle v|$,
which is the second post's bra–ket correspondence.

In a matrix, with respect to an orthonormal basis, the adjoint is the
**conjugate transpose**: $(M^\dagger)_{ij} = M_{ji}^*$ — flip across
the diagonal and conjugate every entry (Panov's lectures, §4.1, in
the references).

### An observable in terms of its definite states

Let $\hat E$ be an observable with orthonormal eigenbasis
$\{|E_i\rangle\}$ and real eigenvalues $E_i$. Apply it to an arbitrary
state, expanded in that basis, and use the second post's
"coordinates are inner products":

$$
\begin{aligned}
\hat E\, |\psi\rangle &= \sum_i c_i\, \hat E |E_i\rangle = \sum_i c_i\, E_i\, |E_i\rangle \\
&= \sum_i E_i\, |E_i\rangle \langle E_i | \psi \rangle = \Big( \sum_i E_i\, |E_i\rangle\langle E_i| \Big) |\psi\rangle .
\end{aligned}
$$

Since this holds for every $|\psi\rangle$, the operator itself is

$$
\boxed{\; \hat E = \sum_i E_i\, |E_i\rangle\langle E_i| \;}
$$

— a weighted sum of the projectors onto its definite states, each
weighted by its outcome. This is the **spectral decomposition** of
the observable; set every $E_i$ to $1$ and it collapses to the
resolution of identity $\sum_i |E_i\rangle\langle E_i| = \hat I$ of
the second post. For the continuous menu the sum is an integral,
$\hat x = \int x\, |x\rangle\langle x|\, dx$, read in the sense the
last post gave such integrals.

### Observables are Hermitian

Take the adjoint of the spectral decomposition, using the three
rules: the adjoint of $E_i\,|E_i\rangle\langle E_i|$ is
$E_i^*\, (\langle E_i|)^\dagger (|E_i\rangle)^\dagger = E_i^*\, |E_i\rangle\langle E_i|$,
so

$$
\hat E^\dagger = \sum_i E_i^*\, |E_i\rangle\langle E_i| = \sum_i E_i\, |E_i\rangle\langle E_i| = \hat E ,
$$

because the eigenvalues are real. An operator equal to its own adjoint
is called **Hermitian** (or self-adjoint),

$$
\hat E^\dagger = \hat E \qquad\Longleftrightarrow\qquad \langle \varphi | \hat E \psi \rangle = \langle \hat E \varphi | \psi \rangle \;\text{ for all } \varphi, \psi,
$$

and we have shown: every observable is Hermitian. In matrix terms,
with respect to any orthonormal basis, the matrix of an observable
equals its own conjugate transpose.

The converse also holds: a Hermitian operator has the two properties
we demanded.

*Real eigenvalues.* Let $\hat E|\varphi\rangle = \lambda|\varphi\rangle$
with $|\varphi\rangle \neq 0$. Move the operator across the bracket:

$$
\lambda\, \langle \varphi | \varphi \rangle = \langle \varphi | \hat E \varphi \rangle = \langle \hat E \varphi | \varphi \rangle = \lambda^*\, \langle \varphi | \varphi \rangle ,
$$

and since $\langle \varphi | \varphi \rangle \gt 0$, $\lambda = \lambda^*$.

*Orthogonal eigenvectors.* Let $\hat E|\varphi_1\rangle = \lambda_1|\varphi_1\rangle$
and $\hat E|\varphi_2\rangle = \lambda_2|\varphi_2\rangle$ with
$\lambda_1 \neq \lambda_2$. The same move gives

$$
\lambda_2\, \langle \varphi_1 | \varphi_2 \rangle = \langle \varphi_1 | \hat E \varphi_2 \rangle = \langle \hat E \varphi_1 | \varphi_2 \rangle = \lambda_1\, \langle \varphi_1 | \varphi_2 \rangle
$$

(the eigenvalues are already known to be real), so
$(\lambda_2 - \lambda_1)\langle \varphi_1 | \varphi_2 \rangle = 0$ and
the inner product vanishes.

*An orthonormal eigenbasis exists.* In finite dimensions this is the
**spectral theorem** for self-adjoint operators: every Hermitian
operator is diagonalizable in an orthonormal basis (Panov, §4.2,
Theorem 4.2.3; its Lemmas 4.2.4 and 4.2.5 are the two facts just
proved).
Within a degenerate eigenvalue the eigenvectors are not orthogonal
automatically, and Gram–Schmidt makes them so. In infinite dimensions
the statement needs care: it holds in the same form for *compact*
self-adjoint operators (the Hilbert–Schmidt theorem — Sergeev's
lectures, Theorem 40), and for general self-adjoint operators, such
as position and momentum, the sum over eigenvectors becomes an
integral over a continuous spectrum, in the sense the last post's
Appendix A pointed at. The problems ahead meet each kind separately.

So the three physical conditions and the one algebraic condition are
the same thing:

> **An observable is a Hermitian operator.** Its eigenvalues — the
> outcomes — are real, and its eigenvectors — the definite states —
> form an orthonormal basis. Conversely, every Hermitian operator
> qualifies as an observable in the formalism.

Whether every Hermitian operator corresponds to something an
apparatus can actually measure is a question for physics, not for
the mathematics; the formalism only says it may.

## Two of the three Pauli matrices

For the spin all of this is two-by-two matrices. Work in the $z$ basis
$\{|u\rangle, |d\rangle\}$, with $|u\rangle = (1, 0)^T$ and
$|d\rangle = (0, 1)^T$ as in the second post. The spectral
decomposition of $\sigma_z$ is immediate — outcomes $\pm 1$ on the
projectors onto $|u\rangle$ and $|d\rangle$:

$$
\sigma_z = (+1)\,|u\rangle\langle u| + (-1)\,|d\rangle\langle d| = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}.
$$

Now the $x$ measurement. Its definite states are $|r\rangle$ and
$|l\rangle$, with outcomes $+1$ and $-1$, so the same recipe gives
$\sigma_x = |r\rangle\langle r| - |l\rangle\langle l|$. In the $z$
basis, $|r\rangle = \frac{1}{\sqrt 2}(1, 1)^T$ and
$|l\rangle = \frac{1}{\sqrt 2}(1, -1)^T$, and the outer products are
rank-one matrices:

$$
|r\rangle\langle r| = \tfrac12 \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}, \qquad |l\rangle\langle l| = \tfrac12 \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}.
$$

Subtract:

$$
\sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}.
$$

Both matrices are Hermitian, as they must be — real and symmetric.
Both have eigenvalues $+1$ and $-1$: for $\sigma_x$, check directly
that $\sigma_x (1, 1)^T = (1, 1)^T$ and $\sigma_x (1, -1)^T = -(1, -1)^T$.
These are two of the three
[**Pauli matrices**](https://en.wikipedia.org/wiki/Pauli_matrices),
and they were obtained from the experiments, through the definite
states the second post extracted from them, not taken from a table. The
third, $\sigma_y$, waits for the $y$-axis states $|i\rangle, |o\rangle$,
which the second post showed cannot be built with real amplitudes; the
next post builds them, and $\sigma_y$ with them.

![The z and x measurements as operators: each is the difference of the projectors onto its two definite states, and in the z basis they are the Pauli matrices σ_z and σ_x](pauli_from_bases.png)

## Measurement, completed

Wishlist item 4 asked how measurement changes the state. Everything
needed is now available.

> **Measurement.** Measuring the observable $\hat E$ in the state
> $|\psi\rangle = \sum_i c_i|E_i\rangle$ returns one of the
> eigenvalues $E_i$, with probability $|c_i|^2$; immediately after a
> measurement that returned $E_i$, the state is the definite state
> $|E_i\rangle$.

In the language of projectors: the outcome $E_i$ projects the state
onto the $i$-th definite direction and renormalizes it,

$$
|\psi\rangle \;\longmapsto\; \frac{|E_i\rangle\langle E_i | \psi \rangle}{\lVert\, |E_i\rangle\langle E_i | \psi \rangle \,\rVert} = \frac{c_i}{|c_i|}\, |E_i\rangle ,
$$

a unit factor times $|E_i\rangle$ — the same physical state. And the
probability of that outcome is the sandwich of the projector:
$\langle \psi | E_i \rangle \langle E_i | \psi \rangle = |c_i|^2$.

Read the first post's three experiments in this language.

- *Repetition confirms.* After a $z$ measurement the state is
  $|u\rangle$ or $|d\rangle$, an eigenvector of $\sigma_z$; measuring
  $\sigma_z$ again finds coefficient $1$ on that eigenvector and
  returns the same value with probability one.
- *Flipping negates.* The apparatus turned upside down measures
  $-\sigma_z$, whose definite states are the same two vectors with
  the outcomes exchanged.
- *A new axis erases the old answer.* Measure $\sigma_x$ on
  $|u\rangle = \frac{1}{\sqrt 2}|r\rangle + \frac{1}{\sqrt 2}|l\rangle$:
  the outcome is $\pm 1$ with probability $\frac12$ each, and the
  state becomes $|r\rangle$ or $|l\rangle$. Measure $\sigma_z$ once
  more: $|r\rangle$ and $|l\rangle$ are each half $|u\rangle$, half
  $|d\rangle$, so the old certainty is gone — probability $\frac12$
  for either answer. The erasure of the first post is
the statement that $\sigma_z$ and $\sigma_x$ have no eigenvector in
  common.

![Measurement as projection: a state is projected onto one of the definite directions of the observable, with probability given by the squared coordinate, and renormalized](measurement_projection.png)

## What we built

The wishlist, with two more items paid.

1. **A state object** — a unit vector in a Hilbert space. ✓ (second post)
2. **A way to blend outcomes** — superposition; probabilities are
   squared amplitudes, *derived today from basis independence*. ✓
3. **Measurable quantities as actors** — Hermitian operators, whose
   eigenvalues are the outcomes and whose eigenvectors are the
   definite states; the average of a quantity is the sandwich
   $\langle \psi | \hat E | \psi \rangle$. ✓
4. **Measurement as an operation on states** — projection onto a
   definite state, with the Born probability. ✓
5. **Geometry must enter** — still open: the dictionary between
   directions in the laboratory and operators on the two-dimensional
   state space, with the cosine of the first post as its first
   entry.

Two of the three Pauli matrices came out of the experiments; the
third, and with it the whole dictionary of item 5, is the next post.

## Onward

Next stop: the qubit and the Bloch sphere. The $y$-axis states are
built, complex amplitudes become unavoidable, $\sigma_y$ joins the
other two, and the spin operator along an arbitrary direction $\hat n$
turns out to be $\hat n \cdot \vec\sigma$ — from which the first
post's $\langle \sigma \rangle = \cos\theta$ follows in one line,
and a two-dimensional complex state space acquires the geometry of an
ordinary sphere.

## References

- Leonard Susskind, Art Friedman. *Quantum Mechanics: The Theoretical
  Minimum*. Basic Books, 2014 — lecture 3, "Principles of Quantum
  Mechanics": §3.1 (linear operators, Hermitian conjugation, Hermitian
  operators and orthonormal bases), §3.2 (the four principles followed
  here), §3.3–3.4 (the spin operators constructed from the
  experiments), §3.5 ("A common misconception": applying an operator is
  not measuring).
- [Quantum Sense](https://www.youtube.com/@quantumsensechannel), *Maths
  of Quantum Mechanics* — videos 7 ([observables as linear
  operators](https://youtu.be/ANLRQ7X6h5A)), 8 ([why the probability
  is the squared amplitude](https://youtu.be/PZUZgOUOOIU)) and 9
  ([Hermitian operators](https://youtu.be/da1rH0Hq62Q)); the Born-rule
  derivation of this post follows video 8.
- A. M. Gleason. *Measures on the closed subspaces of a Hilbert
  space.* Journal of Mathematics and Mechanics 6 (1957), 885–893 — the
  theorem that the Born rule is the only additive probability
  assignment on a Hilbert space of dimension at least three;
  [Wikipedia's account](https://en.wikipedia.org/wiki/Gleason%27s_theorem)
  is a good first reading.
- Т. Е. Панов. [*Лекции по линейной алгебре*](http://higeom.math.msu.su/people/taras/teaching/panov-linalg.pdf)
  (in Russian) — §4.1 (adjoint operators; the matrix of the adjoint
  is the conjugate transpose, p. 65) and §4.2 (self-adjoint
  operators: real eigenvalues, orthogonal eigenvectors, the
  orthonormal eigenbasis, pp. 66–67).
- А. Г. Сергеев. [*Лекции по функциональному анализу*](https://mi-ras.ru/noc/13_14/2/sergeev/funkan.pdf)
  (in Russian) — Theorem 40, the Hilbert–Schmidt theorem, p. 81.
- P. A. M. Dirac. *The Principles of Quantum Mechanics*, 4th ed.
  Oxford University Press, 1958 — chapter II, "Dynamical variables and
  observables": the original statement that observables are real
  linear operators and outcomes their eigenvalues.
- G. W. Mackey. *Mathematical Foundations of Quantum Mechanics*.
  Benjamin, 1963 — the compact axiomatic account, with the
  probability structure (and Gleason's theorem) at its center.
- 3Blue1Brown, [*Eigenvectors and eigenvalues*](https://youtu.be/PFDu9oVAE-g)
  — the geometric picture of an eigenvector, in twenty minutes.
