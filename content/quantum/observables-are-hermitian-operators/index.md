---
title: "Observables Are Hermitian Operators"
date: 2026-10-27
draft: true
tags: ["quantum", "math"]
summary: "The postulate most modern textbooks start from, reached as a conclusion: the basis in which an observable's table is diagonal is its eigenbasis and the outcomes are its eigenvalues; real outcomes make the operator Hermitian, and the spectral theorem makes Hermitian enough; definite states are eigenvectors, in both directions; and the spectrum can be degenerate or continuous — which is where every calculation of this road will start."
math: true
weight: 51
---

The [last post](/quantum/heisenbergs-table/) ended with an
observable as a table with two indices — an operator $\hat A$ —
and one assumption about it: that there is an orthonormal basis
$\{|a_i\rangle\}$ in which the table is diagonal, with numbers
$\lambda_1, \dots, \lambda_n$ on the diagonal. In that basis the
average of the observable in the state
$|\psi\rangle = \sum_i c_i |a_i\rangle$ came out as
$\langle A \rangle = \sum_i \lambda_i |c_i|^2$, the $\lambda_i$ were
read as the outcomes, and the weights $|c_i|^2$ were shown to be
the only admissible probabilities — the Born rule. The assumption
was also shown to be a real restriction: it selects the *normal*
tables, and a price was promised.

This post pays it, and arrives at the sentence most modern
textbooks open with — "observables are Hermitian operators" — as
the last line. Not all of them do: Landau and Lifshitz define the
operator by the mean value and derive Hermiticity from the reality
of the mean, and Dirac defines an observable as a real dynamical
variable with a complete set of eigenstates; this road follows
them.
The basis of the assumption is the eigenbasis of the operator, and
the outcomes are its eigenvalues. Readings of an apparatus are real
numbers, and that alone makes the operator Hermitian; the spectral
theorem then runs the road back, so that Hermitian is also enough
for the assumed basis to exist, and the assumption costs nothing.
The definite states of the first post turn out to be the
eigenvectors, in both directions. And the spectrum of an operator
need not be a short list of numbers: it can repeat, and in infinite
dimensions it can be a whole interval, which is where the problems
of this road — the box, the barrier, the oscillator, the hydrogen
atom — will begin. The road is Landau and Lifshitz's §3 and chapter
II of Dirac's *Principles*, as in the last post.

## Where we stand

Three facts from the earlier posts are used throughout.

- A measurement along an axis has two outcomes, $+1$ and $-1$, and
  two **definite states**, the states that the measurement prepares
  and then confirms on every repetition: $|u\rangle$ and $|d\rangle$
  for the $z$ axis, $|r\rangle$ and $|l\rangle$ for the $x$ axis.
  States an apparatus tells apart with certainty are orthogonal
  (the [second post](/quantum/states-are-vectors/#what-the-geometry-means-physically)).
- The outer product $|a_i\rangle\langle a_i|$ is a
  [projector](/quantum/states-are-vectors/#coordinates-and-a-formula-for-the-identity-operator)
  onto the direction of $|a_i\rangle$, and the projectors of an
  orthonormal basis add up to the identity.
- An observable is an operator $\hat A$; in the orthonormal basis
  $\{|a_i\rangle\}$ where its table is diagonal,
  $\langle a_i | \hat A | a_j \rangle = \lambda_i \delta_{ij}$, its
  average is $\langle \psi | \hat A | \psi \rangle = \sum_i \lambda_i |c_i|^2$,
  the $\lambda_i$ are its outcomes, and $|c_i|^2$ is the probability
  of the outcome $\lambda_i$
  (the [last post](/quantum/heisenbergs-table/)).

## From the diagonal basis to the eigenbasis

### The diagonal basis is the eigenbasis

Recall the definitions. A nonzero vector $|v\rangle$ is an
[**eigenvector**](https://en.wikipedia.org/wiki/Eigenvalues_and_eigenvectors)
of $\hat A$ if the operator merely rescales it,
$\hat A|v\rangle = \lambda|v\rangle$, and $\lambda$ is the
corresponding **eigenvalue**; the set of eigenvalues is the
**spectrum** of $\hat A$. A diagonal table says exactly this about
its basis vectors. By the column rule of
["A table for an observable"](/quantum/heisenbergs-table/#a-table-for-an-observable),
$\hat A |a_j\rangle = \sum_i A_{ij} |a_i\rangle$, and with
$A_{ij} = \lambda_i \delta_{ij}$ only one term survives:

$$
\hat A\, |a_j\rangle = \lambda_j\, |a_j\rangle .
$$

So the basis of the assumption is a basis of eigenvectors, the
numbers on the diagonal are the eigenvalues, and the possible
outcomes of an observable are the spectrum of its operator. Rewriting
the diagonal table without coordinates gives the operator as a sum
over its own definite directions,

$$
\boxed{\; \hat A = \sum_i \lambda_i\, |a_i\rangle\langle a_i| \;}
$$

— the **spectral decomposition**: each outcome times the projector
onto its eigenvector. (Apply both sides to $|\psi\rangle$ and use
$\langle a_i | \psi \rangle = c_i$ to see that it is the same
operator.) Set every $\lambda_i$ to $1$ and it collapses to the
resolution of identity of the second post; keep a single $\lambda_i$
equal to $1$ and set the rest to $0$ and it is the projector
$|a_i\rangle\langle a_i|$ whose average was the Born weight $|c_i|^2$
in the last post.

### Real outcomes make the table Hermitian

Readings of an apparatus are real numbers. So the eigenvalues
$\lambda_i$ are real, and this leaves a mark on the table in every
basis, not only in the diagonal one. The mark has a name, and the
name needs a notion.

Write $|\hat M \psi\rangle$ for the vector $\hat M$ returns when fed
$|\psi\rangle$, so that
$\langle \varphi | \hat M | \psi \rangle = \langle \varphi | \hat M \psi \rangle$.
The [**adjoint**](https://en.wikipedia.org/wiki/Hermitian_adjoint)
$\hat M^\dagger$ of $\hat M$ is the operator that lets the operator
act on the bra instead:

$$
\langle \varphi | \hat M \psi \rangle = \langle \hat M^\dagger \varphi | \psi \rangle \qquad \text{for all } |\varphi\rangle, |\psi\rangle .
$$

It exists and is unique by the second post's Riesz theorem (for fixed
$|\varphi\rangle$ the left side is a linear functional of
$|\psi\rangle$, hence an inner product with a unique vector, which we
name $\hat M^\dagger|\varphi\rangle$). In a matrix with respect to an
orthonormal basis the adjoint is the **conjugate transpose**,
$(M^\dagger)_{ij} = M_{ji}^*$ (Panov's lectures, §4.1); three rules
follow from the definition: $(\hat A^\dagger)^\dagger = \hat A$,
$(\hat A + \hat B)^\dagger = \hat A^\dagger + \hat B^\dagger$,
$(\hat A\hat B)^\dagger = \hat B^\dagger \hat A^\dagger$. The adjoint
of a ket is its bra, $(|v\rangle)^\dagger = \langle v|$ — the second
post's bra–ket correspondence in this notation — and a scalar comes
out conjugated, $(\lambda \hat A)^\dagger = \lambda^* \hat A^\dagger$.

Now take the adjoint of the spectral decomposition. By the rules,
$(|a_i\rangle\langle a_i|)^\dagger = (\langle a_i|)^\dagger (|a_i\rangle)^\dagger = |a_i\rangle\langle a_i|$,
so

$$
\hat A^\dagger = \sum_i \lambda_i^*\, |a_i\rangle\langle a_i| .
$$

With real eigenvalues, $\lambda_i^* = \lambda_i$, the right side is
$\hat A$ again. An operator equal to its own adjoint,
$\hat A^\dagger = \hat A$, is called **Hermitian** (or self-adjoint);
its matrix equals its own conjugate transpose, in every orthonormal
basis, since the definition mentions no basis. In the diagonal basis
the statement is plain — a diagonal matrix equals its conjugate
transpose exactly when its diagonal is real — and it carries over
unchanged to the $z$ basis of the spin, where the table of the $x$
observable is not diagonal at all.

> **The table of every measurable quantity is Hermitian.**

A worry at this point. A table of $n^2$ complex numbers could have
been anything, and the argument has just forced it to be Hermitian;
an experiment cannot be ordered to produce symmetric tables. It
need not be, because the experiment never hands us a table. It
hands us outcomes, which are real numbers, and definite states,
which are orthogonal; the table is assembled from these two lists by
the spectral decomposition, and anything assembled that way is
Hermitian. A table that is not Hermitian would need a complex
outcome, or a pair of definite states that are not orthogonal, and
no apparatus produces either. Tables that are not Hermitian do
appear in the theory, as *devices* rather than observables: Feynman's
apparatus matrix, a rotation of the spin, the evolution of a state
in time — these are unitary, the subject of a later post. And the
first table in history passed the test by itself. Heisenberg's
amplitudes satisfy $X(m, n) = X(n, m)^*$, because the coordinate
$x(t)$ they describe is real — the same condition that makes the
Fourier coefficients of a real signal come in conjugate pairs,
$X_{-\alpha}(n) = X_\alpha(n)^*$ in the notation of the
[classical picture](/quantum/heisenbergs-table/#the-classical-picture).

**And back.** The assumption that opened the last post was promised a
price. Suppose only what the apparatus guarantees — that the average
$\langle \psi | \hat A | \psi \rangle$ is a real number in every
state. Then $\hat A$ is Hermitian, by the
[polarization lemma](/quantum/heisenbergs-table/#polarization) of
the last post: real diagonal values make the bracket
conjugate-symmetric,
$\langle \varphi | \hat A \psi \rangle = \langle \psi | \hat A \varphi \rangle^* = \langle \hat A \varphi | \psi \rangle$
for all $|\varphi\rangle, |\psi\rangle$, and the outer equality is
the definition of $\hat A^\dagger = \hat A$. (The other direction is
a line: if $\hat A^\dagger = \hat A$, then
$\langle \psi | \hat A \psi \rangle = \langle \hat A \psi | \psi \rangle = \langle \psi | \hat A \psi \rangle^*$,
so the average equals its own conjugate.)

And a Hermitian operator has exactly the basis the assumption asked
for:

> **Spectral theorem** (finite dimensions). A Hermitian operator has
> real eigenvalues and an orthonormal basis of eigenvectors.

Two of its three claims are one line each, with the operator moved
across the bracket; the third is cited.

*Real eigenvalues.* If $\hat A|\varphi\rangle = \lambda|\varphi\rangle$
with $|\varphi\rangle \neq 0$, then

$$
\lambda\, \langle \varphi | \varphi \rangle = \langle \varphi | \hat A \varphi \rangle = \langle \hat A \varphi | \varphi \rangle = \lambda^*\, \langle \varphi | \varphi \rangle ,
$$

and $\langle \varphi | \varphi \rangle \gt 0$ gives $\lambda = \lambda^*$.

*Orthogonal eigenvectors.* If $\hat A|\varphi_1\rangle = \lambda_1|\varphi_1\rangle$,
$\hat A|\varphi_2\rangle = \lambda_2|\varphi_2\rangle$ and
$\lambda_1 \neq \lambda_2$, then

$$
\lambda_2\, \langle \varphi_1 | \varphi_2 \rangle = \langle \varphi_1 | \hat A \varphi_2 \rangle = \langle \hat A \varphi_1 | \varphi_2 \rangle = \lambda_1\, \langle \varphi_1 | \varphi_2 \rangle ,
$$

so $(\lambda_2 - \lambda_1)\langle \varphi_1 | \varphi_2 \rangle = 0$
and the inner product vanishes.

*The eigenvectors fill the space.* That there are enough of them to
form a basis is the part that needs the finite dimension and a page
of algebra: Panov, §4.2, Theorem 4.2.3 (its Lemmas 4.2.4 and 4.2.5
are the two facts just proved). Within a repeated eigenvalue the
eigenvectors are not orthogonal automatically, and Gram–Schmidt makes
them so.

So the two roads meet. "Diagonal in some orthonormal basis, with real
numbers on the diagonal" and "real average in every state" are the
same condition on a table, and both say *Hermitian*. The textbook
postulate — "observables are Hermitian operators" — is this
equivalence, stated as a definition.

### Definite states are eigenvectors

One more reading of the average formula, this time for the basis
vectors themselves. In the state $|a_i\rangle$ the coordinates are
$c_i = 1$ and $c_j = 0$ for $j \neq i$: the whole weight sits on the
single outcome $\lambda_i$, the average is $\lambda_i$, and by the
Born rule the outcome $\lambda_i$ has probability one. A state whose
outcome is certain, and which the measurement therefore confirms on
every repetition, is what the [first post](/quantum/the-apparatus-and-the-arrow/#experiment-one-the-window-shows-1--and-repetition-confirms)
called a definite state. And the second post found that states a
measurement tells apart with certainty are orthogonal — which the
eigenvectors of a Hermitian operator are.

The converse also holds: no state outside the eigenvectors has a
certain outcome. In the language of averages, a certain answer is
one with no spread — the average of the squared deviation from the
mean is zero. The squared deviation is the same observable with its
window relabeled, $\lambda_i \mapsto (\lambda_i - \langle A \rangle)^2$,
so by the average rule its mean, the **variance**, is

$$
\langle (A - \langle A \rangle)^2 \rangle = \sum_i |c_i|^2\, (\lambda_i - \langle A \rangle)^2 .
$$

Every term is nonnegative, so the sum vanishes only if every $c_i$
with $\lambda_i \neq \langle A \rangle$ is zero — that is, only if
$|\psi\rangle$ has components along eigenvectors of a single
eigenvalue, which makes it an eigenvector itself. So:

> **Definite states are eigenvectors.** A state in which the outcome
> of an observable is certain is an eigenvector of its operator, and
> the certain outcome is the eigenvalue; and every eigenvector
> $|a_i\rangle$ is such a state, with the certain outcome $\lambda_i$.

This is the statement textbooks start from — Susskind's principles 1
and 2 — and here it arrives as a consequence of the average rule.
For the spin: $|u\rangle$ and $|d\rangle$, the definite states of the
$z$ observable, are the eigenvectors of its operator $\sigma_z$, with
eigenvalues $+1$ and $-1$; the first post's "the measurement
prepares a state that repeats its answer" is the statement that the
state after a measurement is an eigenvector, which the next post
makes precise. From now on the word *observable* is used for the
Hermitian operator as well as for the quantity it stands for. The
three conditions one would otherwise have to *demand* of such an
operator
— real outcomes, definite states that span the space, definite
states that are orthogonal — are the spectral theorem above.

## Beyond the spin

### Degeneracy and the continuous spectrum

Two refinements. An eigenvalue may belong to more than one
independent eigenvector; it is then called **degenerate**, and the
outcome does not determine the state, only the subspace it lands in
— the hydrogen atom will make this concrete, with several orbitals
sharing one energy. And in infinite dimensions the spectrum need not
be a list of eigenvalues with eigenvectors inside the space: the
position operator of the [delta post](/quantum/from-kronecker-to-dirac/)
is the first example, its
"eigenvectors" $|x\rangle$ living just outside $L^2$ and its spectrum
being the whole real line — a **continuous spectrum**, with
$\hat x = \int x\, |x\rangle\langle x|\, dx$ as its spectral
decomposition. The problems ahead show all three kinds: the particle
in a box has a purely discrete spectrum, the tunneling problem a
purely continuous one, and hydrogen both at once. In infinite dimensions the spectral theorem holds in the same form
as above for *compact* self-adjoint operators (the Hilbert–Schmidt
theorem; Sergeev's lectures, Theorem 40, in the references), and for
general self-adjoint operators such as position it survives in this
integral form, which the delta post's Appendix A pointed at.

### Where every calculation starts

The post ends where a textbook begins. Shankar's *Principles*
states the content of this post as postulates and then gives the
procedure for using them (§4.2, p. 117): construct the operator of
the quantity; find its orthonormal eigenvectors $|\omega_i\rangle$
and eigenvalues $\omega_i$; expand the state in that basis,
$|\psi\rangle = \sum_i |\omega_i\rangle\langle\omega_i|\psi\rangle$;
the probability of the result $\omega_i$ is
$|\langle\omega_i|\psi\rangle|^2$. The last three steps are the last
post and this one. In his words (p. 119): "To extract this information for any
observable, we must determine the eigenbasis of the corresponding
operator and find the projection of $|\psi\rangle$ along all its
eigenkets." A working habit follows, also his: there is no need to
change basis each time. One keeps the state written in the eigenbasis
of a chosen observable and computes the eigenvectors of any other
observable as columns in that basis. Landau and Lifshitz go further and
open their §3 with the eigenfunctions: the wave functions of the
states in which the quantity has a definite value are the first
objects they name, and the operator is built afterwards to fit them.

For the problems of this road the chosen observable is the energy, and
the first step — which operator belongs to the observable — is what
the posts on dynamics settle. The second step is then the whole
work: for a particle on a line the eigenvectors are functions, and
"find the eigenbasis" means solving a differential equation. The
particle in a box, the tunneling barrier, the harmonic oscillator and
the hydrogen atom each begin by finding the eigenfunctions of their
energy operator, and everything else about them is read off the
expansion of the state in that basis.

## What we built

The chain of the post. The orthonormal basis in which an
observable's table is diagonal is a basis of eigenvectors, and the
numbers on the diagonal — the outcomes — are the eigenvalues; the
operator is the sum of outcomes times projectors, its spectral
decomposition. Readings are real, so the operator equals its own
adjoint: Hermitian. And Hermitian is enough: a Hermitian operator
has real eigenvalues and an orthonormal eigenbasis, so the
assumption of the last post costs nothing beyond the reality of the
readings. The eigenvectors are exactly the definite states of the
first post. In more than two dimensions an eigenvalue can repeat,
and in infinite dimensions the spectrum can be continuous, as it is
for position.

Wishlist item 3 is paid: **an observable is a Hermitian operator**,
whose eigenvalues are the outcomes, whose eigenvectors are the
definite states, whose average in a state is
$\langle \psi | \hat A | \psi \rangle$, and whose outcome
probabilities are the squared coordinates $|c_i|^2$ in the
eigenbasis. One thing remains: nothing has been said about what a
measurement does to the state. That is the next post.

## Onward

Next stop: what a measurement does. The warning that applying an
operator is not measuring; two of the three Pauli matrices read off
the spin experiments; the Born rule on a line, where the weights
become a density; and measurement itself as a projection, the last
item of the wishlist.

## References

- Л. Д. Ландау, Е. М. Лифшиц. *Квантовая механика (нерелятивистская
  теория)*, Теоретическая физика, т. III — chapter I, §3
  "Операторы" (pp. 24–28 of the 6th Russian edition; §3 "Operators"
  in the English *Quantum Mechanics: Non-Relativistic Theory*): the
  operator *defined* by the mean value (3.8), eigenfunctions (3.12),
  Hermiticity from the reality of the mean (3.15–3.17), and the
  orthogonality of eigenfunctions.
- P. A. M. Dirac. *The Principles of Quantum Mechanics*, 4th ed.
  Oxford University Press, 1958 (Russian translation: П. А. М. Дирак,
  *Принципы квантовой механики*, 2-е изд., Наука, 1979, под ред.
  В. А. Фока) — chapter II, §10 "Observables" (Russian ed. p. 52):
  real dynamical variables, their eigenvalues and eigenstates.
- W. Heisenberg. *Über quantentheoretische Umdeutung kinematischer
  und mechanischer Beziehungen.* Zeitschrift für Physik 33 (1925),
  879–893; English translation in B. L. van der Waerden (ed.),
  *Sources of Quantum Mechanics*, North-Holland, 1967 — the
  conjugate symmetry of the transition amplitudes,
  $X(m, n) = X(n, m)^*$, follows from the reality of the coordinate.
- [Quantum Sense](https://www.youtube.com/@quantumsensechannel), *Maths
  of Quantum Mechanics* — video 9
  ([Hermitian operators](https://youtu.be/da1rH0Hq62Q)).
- Т. Е. Панов. [*Лекции по линейной алгебре*](http://higeom.math.msu.su/people/taras/teaching/panov-linalg.pdf)
  (in Russian) — §4.1 (adjoint operators; the matrix of the adjoint
  is the conjugate transpose, p. 65) and §4.2 (self-adjoint
  operators: Theorem 4.2.3 on the orthonormal eigenbasis, with Lemmas
  4.2.4 and 4.2.5, pp. 66–67).
- R. Shankar. *Principles of Quantum Mechanics*, 2nd ed. Plenum, 1994 —
  chapter 4, "The Postulates — a General Discussion", §4.2, pp. 117–119:
  the four-step procedure (construct the operator, find its
  eigenbasis, expand the state, square the projections) and the
  remark that the eigenbasis of every observable must be found, but
  the basis one works in need not change.
- А. Г. Сергеев. [*Лекции по функциональному анализу*](https://mi-ras.ru/noc/13_14/2/sergeev/funkan.pdf)
  (in Russian) — Theorem 40, the Hilbert–Schmidt theorem, p. 81: the
  spectral theorem for compact self-adjoint operators in infinite
  dimensions.
- 3Blue1Brown, [*Eigenvectors and eigenvalues*](https://youtu.be/PFDu9oVAE-g)
  — the geometric picture of an eigenvector, in twenty minutes.
