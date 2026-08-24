# From Kronecker Delta to Dirac Delta

The Dirac delta is one of those mysterious objects that shows up everywhere in quantum mechanics, usually handed to you as-is: a "function" that is zero everywhere except at a single point where it's infinitely tall, and this function somehow integrates to one. It is defined by the **sifting property**

$$
\int_{-\infty}^{\infty} f(y)\, \delta(x - y)\, dy = f(x)
$$

which says that integrating any function against $\delta(x-y)$ simply plucks out its value at $y = x$. Very useful, but where does such a thing actually *come from*?

In this post we'll try to derive the Dirac delta from another object that is famous in linear algebra: the **Kronecker delta** $\delta_{ij}$.

---

## Kronecker Delta

In finite-dimensional linear algebra, an orthonormal basis $\{|e_i\rangle\}$ satisfies the following relation:

$$
\langle e_i | e_j \rangle = \delta_{ij} = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases}
$$

This is called the **Kronecker delta**, and it helps us work with discrete inner products. If we expand two vectors $|\psi\rangle = \sum_i a_i |e_i\rangle$ and $|\varphi\rangle = \sum_j b_j |e_j\rangle$, the inner product collapses (here $\overline{a_i}$ denotes the complex conjugate of $a_i$):

$$
\langle \psi | \varphi \rangle = \sum_i \sum_j \overline{a_i}\, b_j \, \langle e_i | e_j\rangle = \sum_i \sum_j \overline{a_i}\, b_j \, \delta_{ij} = \sum_i \overline{a_i}\, b_i
$$

The $\delta_{ij}$ acts as a **diagonal selector**: it removes every term of the double sum except those on the diagonal $i = j$.

But what happens when we move to a continuous setting? For instance, a particle on the real line, where the "basis" is indexed by a continuous label $x \in \mathbb{R}$ rather than a discrete index $i$. We would like an analogue of the Kronecker delta: some object $\langle x \mid y \rangle$ that selects the diagonal $x = y$ inside an *integral* instead of a sum.

That object is the **Dirac delta** $\delta(x - y)$.

---

## Inner Product

Now let's take two "continuous superpositions":

$$
|\psi\rangle = \int a(x)\, |x\rangle \, dx, \qquad |\varphi\rangle = \int b(y)\, |y\rangle \, dy
$$

where $|x\rangle$ is the "basis" ket labeled by the real number $x$, and the functions $a, b$ are assumed to be continuous and integrable ($\int |a(x)|\, dx < \infty$), so that every sum and integral below converges. And let's compute $\langle \psi | \varphi \rangle$ by discretizing each integral into a Riemann sum and taking a limit.

Let's lay down a grid of spacing $\Delta x$, with sample points $x_i$, and by the definition of the Riemann integral we'll get:

$$
|\psi\rangle \approx \sum_i a(x_i)\, |x_i\rangle\, \Delta x, \qquad |\varphi\rangle \approx \sum_j b(y_j)\, |y_j\rangle\, \Delta y
$$

Let's call them $|\psi_\Delta\rangle$ and $|\varphi_\Delta\rangle$.

It's important to note that those are **finite** linear combinations of kets, so everything we do with them below is finite-dimensional linear algebra. It's also worth flagging now that the *continuous* objects these sums approach (the integral $\int a(x)|x\rangle\,dx$ and the kets $|x\rangle$ themselves) are more delicate to define rigorously than ordinary vectors.

Now we compute the inner product of those finite sums. We will use two standard properties of the inner product: *additivity* (it distributes over sums in each slot) and *(conjugate-)linearity* (scalars pull out of each slot, the first-slot one conjugated).

$$
\langle \psi_\Delta | \varphi_\Delta \rangle
= \Big\langle\; \sum_i a(x_i)\, |x_i\rangle\, \Delta x \;\Big|\; \sum_j b(y_j)\, |y_j\rangle\, \Delta y \;\Big\rangle =
$$

**By additivity**, we can pull both sums outside the single bracket:

$$
= \sum_i \sum_j \Big\langle\, a(x_i)\, |x_i\rangle\, \Delta x \;\Big|\; b(y_j)\, |y_j\rangle\, \Delta y \,\Big\rangle =
$$

**By (conjugate-)linearity**, we can pull the scalars out of each slot (and the coefficient in the first slot is conjugated):

$$
= \sum_i \sum_j \overline{a(x_i)}\; b(y_j)\; \langle x_i | y_j \rangle\; \Delta x\, \Delta y
$$

Here the inner kets $|x_i\rangle$ and $|y_j\rangle$ have **fused** into the single scalar $\langle x_i | y_j \rangle$. Let's call it the **kernel** of this sum and denote it $K_\Delta(x_i, y_j) := \langle x_i | y_j \rangle$. And the **main question** is now: what is the kernel?

---

## Finding the Kernel

It's tempting to say that this kernel is just the Kronecker delta:

$$
\langle x_i | y_j \rangle \overset{?}{=} \delta_{ij}
$$

Let's check whether that works. Using the definition of the Kronecker delta (it is $1$ only when $i = j$, and $0$ otherwise), we collapse the $j$-sum:

$$
\sum_i \sum_j \overline{a(x_i)}\, b(y_j)\, \delta_{ij}\, \Delta x\, \Delta y
= \sum_i \overline{a(x_i)}\, b(x_i)\, \Delta x\, \Delta y =
$$

Since we are free to choose the grid as we like, take $\Delta x = \Delta y$:

$$
= \sum_i \overline{a(x_i)}\, b(x_i)\, \Delta x\, \Delta x
= \left( \sum_i \overline{a(x_i)}\, b(x_i)\, \Delta x \right) \cdot \Delta x
$$

We are left with **two** factors: a Riemann sum and a leftover $\Delta x$. As $\Delta x \to 0$ the Riemann sum approaches the finite number $\int \overline{a(x)}\, b(x)\, dx$, but it is multiplied by that extra $\Delta x$, which goes to zero. So the whole expression converges to $0$:

$$
\left( \sum_i \overline{a(x_i)}\, b(x_i)\, \Delta x \right) \cdot \Delta x \;\xrightarrow{\;\Delta x \to 0\;}\; 0
$$

Which means that the naive guess $\langle x_i | y_j \rangle = \delta_{ij}$ is a **dead end**.

<details>
<summary><b>A fully rigorous Riemann sum</b> (click to expand)</summary>

In the main text we treated $\sum_i \overline{a(x_i)}\, b(x_i)\, \Delta x$ as a Riemann sum over the whole line. Strictly speaking, a Riemann sum is defined on a *bounded* interval: you pick a finite window, partition it into cells, and sample the function in each cell. So let's redo the computation exactly that way, with every step an explicit estimate.

We work on the window $[-A, A]$ and split it into $2N$ equal cells, so the spacing is $\Delta x = \frac{2A}{2N} = \frac{A}{N}$ and the sample points are $x_i = i \cdot \Delta x$ for $i = -N, \dots, N$. The kets are taken genuinely orthonormal, exactly as in the naive guess: $\langle x_i | x_j \rangle = \delta_{ij}$. Since $a, b$ are continuous, they are bounded on the window: $|a(x)|, |b(x)| \le M$ for some constant $M$ (a continuous function on a closed bounded interval is always bounded).

As in the main text, each coefficient carries one factor of the spacing:

$$
|\psi_\Delta\rangle = \frac{A}{N}\sum_{i=-N}^{N} a(x_i)\,|x_i\rangle,
\qquad
|\varphi_\Delta\rangle = \frac{A}{N}\sum_{j=-N}^{N} b(y_j)\,|y_j\rangle
$$

Taking the inner product:

$$
\langle \psi_\Delta | \varphi_\Delta \rangle
= \frac{A^2}{N^2} \sum_{i=-N}^{N} \sum_{j=-N}^{N} \overline{a(x_i)}\, b(y_j)\, \delta_{ij}
= \frac{A^2}{N^2} \sum_{i=-N}^{N} \overline{a(x_i)}\, b(x_i)
=: S_N
$$

Now we bound $S_N$ term by term, using that each of the $2N+1$ terms is at most $M^2$ in absolute value:

$$
|S_N|
\le \frac{A^2}{N^2} \cdot (2N+1) \cdot M^2
\;\xrightarrow{\; N \to \infty \;}\; 0
$$

There are $\sim 2N$ bounded terms against a $1/N^2$ prefactor, so the sum converges to zero.

</details>

---

## Normalizing the Basis

So the dead end is not a failure of the limit machinery. The limit worked flawlessly and faithfully reported that the state we built converges to zero. We didn't compute the right state wrongly; we **discretized the wrong state**.

So which discrete state is the right one? The failed guess showed that we don't actually know the inner products of the original kets: assuming $\langle x_i | x_j \rangle = \delta_{ij}$ led to zero. So let's build the state from a basis we define to be orthonormal. We introduce a new symbol: let $|\hat x_i\rangle$ be the orthonormal cell-states, $\langle \hat x_i | \hat x_j\rangle = \delta_{ij}$, where each $|\hat x_i\rangle$ represents "the particle is somewhere in cell $i$". Write the state as $|\psi_\Delta\rangle = \sum_i c_i\, |\hat x_i\rangle$, so that $|c_i|^2$ is the probability of finding the particle in cell $i$. The modulus squared of the wavefunction, $|a(x)|^2$, is the probability **density** (probability per unit length). So the probability of landing in a cell of width $\Delta x$ is:

$$
|c_i|^2 = |a(x_i)|^2\, \Delta x \quad\Longrightarrow\quad c_i = a(x_i)\, \sqrt{\Delta x}
$$

(This also diagnoses the dead end: the naive coefficients $c_i = a(x_i)\,\Delta x$ correspond to cell probabilities $|a(x_i)|^2\,\Delta x^2$, so the total probability $\sum_i |a(x_i)|^2\,\Delta x^2 = \Delta x \sum_i |a(x_i)|^2\,\Delta x \to 0$.)

And now we can finally answer what the $|x_i\rangle$ from the original Riemann sum is. We have two expressions for the same discretized state $|\psi_\Delta\rangle$: the Riemann-sum notation $\sum_i a(x_i)\,|x_i\rangle\,\Delta x$ that we adopted at the start (with the normalization of $|x_i\rangle$ left open), and the expansion $\sum_i a(x_i)\,\sqrt{\Delta x}\;|\hat x_i\rangle$ that we just derived. Both sums run over the same cells, so for them to describe the same state, the terms must agree cell by cell:

$$
a(x_i)\,|x_i\rangle\,\Delta x
\;=\;
a(x_i)\,\sqrt{\Delta x}\;|\hat x_i\rangle
\quad\Longrightarrow\quad
|x_i\rangle = \frac{1}{\sqrt{\Delta x}}\,|\hat x_i\rangle
$$

So $|x_i\rangle$ was never an independent object that got rescaled. It is determined by the equation above: the unique ket that makes the Riemann-sum notation $\sum_i a(x_i)\,|x_i\rangle\,\Delta x$ (and its limit $\int a(x)\,|x\rangle\,dx$) describe the correct state.

With this identification, the kernel becomes:

$$
\langle x_i | y_j \rangle = \frac{1}{\Delta x}\, \langle \hat x_i | \hat x_j \rangle = \frac{\delta_{ij}}{\Delta x}
$$

It carries a factor of $1/\Delta x$, which cancels out the leftover $\Delta x$, and we get the correctly normalized kernel:

$$
\boxed{\; \langle x_i | y_j \rangle = \frac{\delta_{ij}}{\Delta x} \;}
$$

Notice that the norms $\| |x_i\rangle \| = 1/\sqrt{\Delta x}$ diverge as $\Delta x \to 0$: the limiting objects $|x\rangle$ cannot be ordinary normalizable vectors. This is why "basis" was in scare quotes at the start.

---

## Taking the Limit

Substituting the new kernel we get:

$$
\langle \psi_\Delta | \varphi_\Delta \rangle
= \sum_i \sum_j \overline{a(x_i)}\, b(y_j)\, \frac{\delta_{ij}}{\Delta x} \, \Delta x\, \Delta y
$$

We now have two options.

### Option A

Do the $j$-sum with $\delta_{ij}$ (using the grid $\Delta y = \Delta x$):

$$
\sum_i \sum_j \overline{a(x_i)}\, b(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta x\, \Delta y
\;\underset{\Delta y = \Delta x}{=}\;
\sum_i \overline{a(x_i)}\, b(x_i)\, \Delta x
\;\xrightarrow{\;\Delta x \to 0\;}\;
\int \overline{a(x)}\, b(x)\, dx
$$

The $1/\Delta x$ cancelled exactly one of the two spacings, leaving a single Riemann sum.

### Option B

Keep the double structure and take the limit of the whole double sum as a *number*:

$$
L := \lim_{\substack{\Delta x \to 0 \\ \Delta y = \Delta x}} \sum_i \sum_j \overline{a(x_i)}\, b(y_j)\, \underbrace{\frac{\delta_{ij}}{\Delta x}}_{K_\Delta(x_i, y_j)}\, \Delta x\, \Delta y
$$

This limit exists: it is the limit of the same double sum we just computed in Option A, so it equals $\int \overline{a(x)}\, b(x)\, dx$. Now, the summand has exactly the shape of a double Riemann sum with kernel $K_\Delta(x_i, y_j) = \delta_{ij}/\Delta x$, so we would *like* to write $L$ as a double integral against some limiting kernel:

$$
L \overset{?}{=} \iint \overline{a(x)}\, b(y)\, K(x, y)\, dx\, dy
$$

Now the question is whether any object $K(x,y)$ makes this legitimate, and what *kind* of object it would have to be. Comparing with Option A, such a $K$ would have to satisfy:

$$
\iint \overline{a(x)}\, b(y)\, K(x, y)\, dx\, dy = \int \overline{a(x)}\, b(x)\, dx
$$

The rest of the post is about pinning down this $K$.

---

## Limiting Kernel

Let's fix the index $i$ (so the spike's location $x_i$ is fixed; call it $x$) and view $K_\Delta(x_i, y_j) = \delta_{ij}/\Delta x$ as a function of $y_j$:

- at $y_j = x_i$: the value is $1/\Delta x$,
- at every other grid point: the value is $0$.

This is a single spike of **width** $\Delta x$ and **height** $1/\Delta x$, hence the **area** is:

$$
\text{width} \times \text{height} = \Delta x \cdot \frac{1}{\Delta x} = 1
$$

As $\Delta x \to 0$: the width shrinks to $0$, the height diverges to $\infty$, and the area stays pinned at $1$. This is exactly the picture people draw for the Dirac delta: an infinitely thin, infinitely tall spike of unit area.

So it's tempting to just take the limit of $K_\Delta = \delta_{ij}/\Delta x$ directly and call the result $K(x,y)$. But that doesn't work, and it's worth seeing why.

If we tried to take the limit pointwise, we'd get a "function" that is $0$ everywhere except at the single point $y = x$, where it is infinite. But there is **no ordinary function** like that: a function that is zero everywhere except at one point has integral $0$, not $1$, because a single point has no width and contributes no area. So the spike, taken literally, is not a legitimate function, and the naive pointwise limit doesn't exist.

This is the key obstacle: the object we are reaching for is **not a function at all**. So we cannot define $K(x,y)$ by its pointwise values. Instead we fall back on the definition from the introduction. The Dirac delta is defined not by its values but by **what it does inside an integral**, the sifting property:

$$
\int f(y)\,\delta(x - y)\, dy = f(x)
$$

So to identify $K(x,y)$ with the Dirac delta, we won't take a pointwise limit at all. Instead we'll show that $K$ obeys this sifting property.

---

## Identifying the Kernel

We now show that $K(x,y)$ obeys the sifting property, which is what *earns* it the name $\delta(x-y)$. The strategy: test the discrete kernel $K_\Delta$ against an arbitrary function $f$, evaluate as an honest finite sum, and take the limit only at the end.

Let's form the discrete analogue of "integrating $f$ against $K$": $f$ summed against $K_\Delta$ with the spacing $\Delta y$. Here we fix a target point $x$ once and for all, and let $i$ be the index of the grid cell containing $x$, so that $x_i$ is the grid point nearest our target (hence $|x_i - x| \le \Delta x$):

$$
\sum_j f(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta y
$$

On our grid $\Delta y = \Delta x$, so the $1/\Delta x$ and $\Delta x$ cancel exactly, and the Kronecker delta keeps only the $j = i$ term:

$$
\sum_j f(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta x
= \sum_j f(y_j)\, \delta_{ij}
= f(x_i)
$$

Taking $\Delta x \to 0$: the grid point $x_i$ is squeezed onto the target ($|x_i - x| \le \Delta x \to 0$), so by continuity of $f$ we get $f(x_i) \to f(x)$:

$$
\lim_{\Delta x \to 0} \sum_j f(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta y = f(x)
$$

This holds for **every** continuous function $f$. It is exactly the sifting property, stated in the only rigorous form available to us: as a limit of numbers. We therefore *define* the notation $\int f(y)\, K(x,y)\, dy$ to mean this limit, and with that reading:

$$
\int f(y)\, K(x, y)\, dy = f(x) \qquad \text{for every continuous function } f
$$

An object satisfying the sifting property for all $f$ is, by definition, the **Dirac delta**. We have therefore *earned* the identification

$$
\boxed{\; K(x, y) = \delta(x - y) \;}
$$

Now the spike features from earlier follow as *consequences* of the sifting property. They are conclusions, not assumptions:

- **Unit area:** set $f \equiv 1$, giving $\int \delta(x - y)\, dy = 1$.
- **Concentration at $y = x$:** for any $f$ vanishing at $x$, the integral returns $f(x) = 0$, so $\delta$ "feels" nothing away from the diagonal.

This also closes the question we had previously. Sifting in the $y$-variable collapses the double integral into the single one, $\iint \overline{a(x)}\, b(y)\, \delta(x-y)\, dx\, dy = \int \overline{a(x)}\, b(x)\, dx$, which is exactly the condition we required of $K$.

Note what we did **not** do: we never claimed the spikes converge as functions. We tested against $f$, producing a limit of *numbers*, and identified $K$ by its action. That is the only sense in which the identification holds, as the next section makes precise.

---

## Weak Convergence

It is tempting to write

$$
\frac{\delta_{ij}}{\Delta x} \longrightarrow \delta(x - y)
$$

but read as an ordinary limit of functions this is wrong: the pointwise limit of the spikes does not exist, and $\delta(x-y)$ is not a function anyway (it is a **distribution**: an object defined only by its action inside integrals). The correct statement is called **weak convergence**: for every continuous function $f$, the *numbers* $\sum_j f(y_j)\, \frac{\delta_{ij}}{\Delta x}\, \Delta y$ converge to $f(x)$. Compare with the previous section: this is the same tested sum, with the same conventions, and the same limit we computed there. The arrow above is universally used as shorthand for this statement.

---

## Summary

The Kronecker delta $\delta_{ij}$ and the Dirac delta $\delta(x-y)$ are really one idea in two settings. The first selects the diagonal of a double sum:

$$
\sum_i \sum_j \overline{a_i}\, b_j\, \delta_{ij} = \sum_i \overline{a_i}\, b_i
$$

The second selects the diagonal of a double integral:

$$
\iint \overline{a(x)}\, b(y)\, \delta(x-y)\, dx\, dy = \int \overline{a(x)}\, b(x)\, dx
$$

To get from the first to the second, the discrete kernel must be rescaled by $1/\Delta x$, because that is the normalization a continuous basis forces, and the resulting spikes converge to $\delta(x-y)$ only in the weak sense: not point by point, but through what they do to every function they are integrated against. In short, the Dirac delta is what the Kronecker delta becomes when a sum becomes an integral.

---

## References

- G. Stefanucci, R. van Leeuwen, *Nonequilibrium Many-Body Theory of Quantum Systems* (Cambridge University Press, 2013), Ch. 1
- [Going from Kronecker deltas to Dirac deltas](https://www.physicsforums.com/threads/going-from-kronecker-deltas-to-dirac-deltas.1064459/), a Physics Forums discussion of the passage from the book above
- [Heisenberg-Langevin Formalism For Open Circuit-QED Systems](https://arxiv.org/abs/1711.05699) (2017), Appendix A.2
- [Exact asymptotic solutions to nonlinear Hawkes processes](https://arxiv.org/abs/2110.01523) (2021), Appendix A
- [Derivation of the Four-Wave Kinetic Equation in Action-Angle Variables](https://arxiv.org/abs/1911.13057) (2019)
- [Discretized light-cone quantization and the effective interaction in hadrons](https://arxiv.org/abs/hep-ph/9910203) (1999)
- N. Wheeler, [Simplified production of Dirac delta function identities](https://www.reed.edu/physics/faculty/wheeler/documents/Miscellaneous%20Math/Delta%20Functions/Simplified%20Dirac%20Delta.pdf)
- [What Exactly is Dirac's Delta Function?](https://www.physicsforums.com/insights/what-exactly-is-diracs-delta-function/), a Physics Forums Insights article