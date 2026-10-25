# The Born rule from basis independence (cut from QM-3b on 2026-10-25)

Removed from the measurement post when the Born rule got its single derivation
(Landau–Lifshitz, bilinearity) in "Heisenberg's Table". Kept for a possible
notebook or appendix. Figure: figures/born_counterexample.png.

## The Born rule, from basis independence

The last post's derivation uses the assumption that probabilities
are bilinear in the coordinates. The following argument for the
squared magnitude uses no such assumption — only that probabilities must not depend on
the basis the state happens to be written in. It follows video 8 of
the Quantum Sense series.

Suppose the probability of the outcome $\lambda_i$ is some function
of the coordinate, $P_i = f(c_i)$ — the same function for every
outcome and every observable, since nothing in the formalism singles
one out. Take real coefficients first, in two dimensions, and try the
simplest guess: the probability is the magnitude, $P_i = |c_i|$, so
that $|c_1| + |c_2| = 1$. For the fifty-fifty state this gives
$c_1 = c_2 = \frac12$. Now write the *same* state in another
orthonormal basis — one obtained by rotating the first, which is what
a different measurement axis does. In the rotated basis the
coordinates of the vector $(\frac12, \frac12)$ are, say,
$(\frac{1}{\sqrt{10}}, -\frac{2}{\sqrt{10}})$, and the sum of
magnitudes is no longer one:

$$
\tfrac{1}{\sqrt{10}} + \tfrac{2}{\sqrt{10}} = \tfrac{3}{\sqrt{10}} \approx 0.95 .
$$

The coefficients in the new basis no longer add up to a probability
distribution, and the vector would have to be rescaled by hand every
time the basis changes. But the state is the same physical state
whichever apparatus we point at it; a rule that needs a rescaling
depending on the basis cannot be a law about the state.

![The same state vector in two orthonormal bases: the sum of the magnitudes of its coordinates changes with the basis, while the sum of their squares — the squared length — does not](figures/born_counterexample.png)

What *is* the same in every orthonormal basis is the length of the
vector: for a unit state, $\sum_i c_i^2 = 1$ in every one of them
(real case). So $f$ must produce a probability distribution on every
unit vector, in every orthonormal basis, from the coordinates alone.
Write down what that requires, for real coefficients.

1. **Normalization.** $\sum_i f(c_i) = 1$ whenever $\sum_i c_i^2 = 1$.
2. **A single function.** The same $f$ serves every coordinate, every
   basis, every observable.
3. **Sign does not matter.** $f(-c) = f(c)$: the state $-|\psi\rangle$
   is the same physical state as $|\psi\rangle$ (the second post: a
   unit scalar factor changes no measurement), so flipping the sign of
   one coordinate cannot change a probability.

Condition 1 ties $n$ numbers by one equation. Solve the tie for the
last coordinate, $c_n = \sqrt{1 - \sum_{i \lt n} c_i^2}$ (condition 3
lets us take the positive root), and condition 1 becomes an identity
in the $n - 1$ *independent* variables $c_1, \dots, c_{n-1}$:

$$
\sum_{i=1}^{n-1} f(c_i) + f\!\left(\sqrt{1 - \textstyle\sum_{i=1}^{n-1} c_i^2}\right) = 1 .
$$

An identity in independent variables can be differentiated with
respect to any of them. Differentiate with respect to $c_1$ (assume
$f$ differentiable; this is the argument's technical assumption):

$$
f'(c_1) - f'(c_n)\, \frac{c_1}{c_n} = 0 \qquad\Longrightarrow\qquad \frac{f'(c_1)}{c_1} = \frac{f'(c_n)}{c_n} .
$$

Differentiating with respect to $c_2$ instead gives the same
right-hand side, so

$$
\frac{f'(c_1)}{c_1} = \frac{f'(c_2)}{c_2}
$$

for all admissible values of two independent variables. A function of
$c_1$ alone that equals a function of $c_2$ alone is a constant:

$$
\frac{f'(c)}{c} = \lambda \qquad\Longrightarrow\qquad f(c) = \frac{\lambda}{2}\, c^2 + \mu .
$$

Two physical boundary conditions fix the constants. A state with
$c_i = 0$ has no component along $|a_i\rangle$ — it is orthogonal to
it, hence perfectly distinguishable from it — so the outcome
$\lambda_i$ never occurs: $f(0) = 0$, and $\mu = 0$. A state with
$c_i = 1$ *is* $|a_i\rangle$, and then $\lambda_i$ is certain:
$f(1) = 1$, so $\lambda = 2$. Therefore $f(c) = c^2$.

The coefficients are complex in general. One observation extends the
result. The eigenvector $|a_i\rangle$ is fixed by the physics only up
to a unit factor: $e^{i\theta}|a_i\rangle$ is the same physical
state, still an eigenvector with the same eigenvalue, still of length
one. So $\{e^{i\theta_i}|a_i\rangle\}$ is also an orthonormal eigenbasis
of the same observable, and in it the coordinates of $|\psi\rangle$
are $e^{-i\theta_i} c_i$. The probabilities cannot know which of these
bases was used; hence $f$ depends on $c_i$ only through $|c_i|$.
Apply the real result to the nonnegative numbers $|c_i|$, which
satisfy $\sum_i |c_i|^2 = 1$:

> **The Born rule.** If $|\psi\rangle = \sum_i c_i |a_i\rangle$ in the
> orthonormal eigenbasis of an observable, the probability that a
> measurement of it returns $\lambda_i$ is
> $$P(\lambda_i) = |c_i|^2 = |\langle a_i | \psi \rangle|^2 .$$

Squared magnitudes, because the squared length is the quantity that
does not change between orthonormal bases. The two derivations meet:
the weights that diagonalization produced are the only weights that
basis independence allows. (The argument assumed a differentiable
$f$, the same for every coordinate; Gleason's theorem removes the
assumptions in dimension three and more.)

