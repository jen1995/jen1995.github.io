# The quantum road — act three of the blog

Goal: a **minimal but rigorous** path to four solved problems — particle in
a well, tunneling, harmonic oscillator, hydrogen orbitals — without
building the full axiomatic apparatus. Deep basic principles, with proofs;
companion notebooks with interactive visualizations wherever a concept can
be *played with*.

Primary sources:
- Eugenia's notes: ~/Desktop/smth/notion_exports/quantum_calculations
  ("Математические основы" §1–13 + "Кубит, сфера Блоха") — the backbone;
  built on the Quantum Sense series (https://youtu.be/3nvbBEzfmE8)
- Susskind & Friedman, *QM: The Theoretical Minimum* (local PDF) — the
  Stern–Gerlach measurement story, spin, ch. 1–4
- Susskind & Hrabovsky, *The Theoretical Minimum* (classical) + Bolotin et
  al., *Теоретическая механика* — the Lagrangian/Hamiltonian interlude
- Panov, linear algebra lectures (higeom.math.msu.su) — proofs for the
  finite-dimensional theorems
- ipetr0v's draft "From Kronecker Delta to Dirac Delta" (PR #2,
  drafts/dirac_delta/) — the continuous-basis bridge
- Fermi, *Лекции по квантовой механике* (Chicago 1954 notes; Russian
  edition at https://publ.lib.ru/ARCHIVES/F/FERMI_Enriko_(fizik)/_Fermi_E..html
  — recommended by Eugenia's dad): the physicist's-eye counterpart to our
  route. Three roles: (1) the optical–mechanical analogy as a SECOND
  bridge to the Schrödinger equation in QM-5 (section or big cut);
  (2) cross-check and tricks for the four problem posts; (3) Fermi-style
  order-of-magnitude estimates via uncertainty for asides/notebooks.
  Terse, assumes classical mechanics — a seasoning, not a first textbook.

Standing assets from the Fourier road (reuse, don't rebuild): the delta
built honestly in Part 1; Fourier pair machinery from Four Shades; the
time–frequency trade-off from Part 3. The blog's Onward already promised:
position–momentum is a Fourier pair, uncertainty is Δf·Δt in a lab coat —
these are the payoff bridges of this act.

Rigor policy (inherited from the Fourier road): main flow honest, classical
fine print flagged and pointed to; the genuinely hard functional analysis
(unbounded operators, continuous spectra, rigged Hilbert spaces) gets
*named* in details-cuts with references, not rebuilt. Physicist junctures
declared in each post's intro.

---

## QM-1. The apparatus and the arrow (measurement first)

Experiment before mathematics — the house move (Part 1 started from sound).
The Stern–Gerlach story from Susskind ch. 1 + the qubit notes: a black-box
apparatus with an orientation arrow; only ±1 ever appears; repeating
confirms; flipping negates; turning by θ gives ±1 at random with mean
cos θ. The apparatus *prepares* rather than *reveals*; measurement is not
reading off a preexisting vector. Ends with the wishlist: discrete
outcomes, probabilities, a state object that measurement disturbs — and
the observation that classical (value ↔ state) bookkeeping dies here.
No formulas beyond ⟨m,n⟩ = cos θ. Figures: apparatus strips (frames like
the wagon-wheel strips). Notebook: **nb-spin-lab** — simulated apparatus
the reader can rotate and fire, statistics converging to cos²(θ/2).

## QM-2. States are vectors (the language, part I)

Her notes §1–3, 5: why linear spaces (outcome objects M_A, superposition
with weights), kets, inner product axioms, orthonormal bases, norm/length,
Hilbert space (completeness as the reason infinite superpositions stay
states — details-cut: separability, Гильберт–Шмидт pointer), bras as
functionals, Riesz theorem (her careful "бра = сопряжённая строка только в
ортонормированном базисе" remark deserves its own cut), resolution of
identity Σ|i⟩⟨i| = I. Proofs: finite-dim Riesz (Panov), completeness
examples (ℂⁿ, L²). Notebook: **nb-state-space** — 2D complex vectors,
change of basis, inner products as overlaps.

## QM-2½. From Kronecker delta to Dirac delta (ipetr0v's post — PR #2)

The guest/joint post slots HERE: it answers the open questions of notes §4
(what is the continuous basis |x⟩, why ⟨x|y⟩ = δ(x−y), why the 1/√dx
normalization) by the continuum limit of the Kronecker delta, with the
weak-convergence reading of sifting. Cross-links both ways: Fourier Part 1
built the same delta as a limit of averaging bumps (analysis route); this
post builds it as a limit of orthonormality (linear-algebra route) — two
roads to one object, map-style. Review + house figures + publication
protocol as usual. Depends only on QM-2 (inner products, bases).

## QM-3. Observables and the Born rule (the language, part II)

Notes §6–8: observables as operators, eigenvalues = outcomes (postulate,
stated honestly as the codification of QM-1's experiments), eigenstates,
degeneracy; the Born-rule *derivation* from basis-invariance of
probability (her §7 — the differential-equation argument is a gem and
becomes the post's centerpiece), expectation values ⟨ψ|Ê|ψ⟩; Hermitian
operators: E = Σ E_i|E_i⟩⟨E_i|, self-adjointness ⇔ real spectrum +
orthonormal eigenbasis (finite-dim proof via Panov; Hilbert–Schmidt named
in a cut). Notebook: **nb-born** — measure a qubit state many times,
histogram → |c_i|², rotate the basis and watch probabilities change while
the state doesn't.

## QM-4. The qubit and the Bloch sphere (everything, applied)

The smallest quantum system carries every concept from QM-1..3 at once —
and answers "why complex numbers": deriving |i⟩, |o⟩ from the three
experimental constraints forces imaginary amplitudes (her notes' explicit
computation). u/d, l/r, i/o triples; global phase does not matter →
two real parameters → the Bloch sphere with θ/2 (why HALF the angle — the
sphere-vs-Hilbert-space geometry, her "Замечание" about orthogonal-in-ℂ² =
antipodal-on-sphere); apparatus at angle θ ⇒ P(+1) = cos²(θ/2), closing
the loop to QM-1's cos θ average. Geometric emphasis: what the device's
*position in space* selects — the measurement basis. Notebook:
**nb-bloch** — interactive sphere: drag the state, drag the apparatus
axis, fire measurements, see the collapse jump.

## QM-5. Dynamics: from unitarity to Schrödinger (and the Fourier payoff)

The longest post; notes §9–13 + the classical interlude.
1. Unitary operators: preserve probabilities (§10).
2. Classical interlude (Bolotin + Susskind classical + §11): Lagrangian,
   stationary action, Euler–Lagrange ⇒ Newton; the generator table
   (∂L/∂x = dp/dt, ∂L/∂t = −dE/dt) — as a details-heavy but self-contained
   section, only what the generator story needs.
2½. Fermi's second bridge (cut or section): the optical–mechanical
   analogy — geometrical optics : wave optics = classical mechanics :
   quantum mechanics; eikonal → de Broglie → the same Schrödinger
   equation from the wave side. Two roads, one equation — map-style.
3. Evolution operator U(t): three physical requirements ⇒ unitarity
   (her §12 proof), Taylor step ⇒ i d/dt|ψ⟩ = Ĥ|ψ⟩, the generator
   argument for Ĥ = energy, ħ for dimensions — flagged honestly as the
   act's physicist juncture (her own "натягивание совы" note becomes the
   post's honesty cut).
4. Translation operator ⇒ momentum operator p̂ = −iħ d/dx (§13),
   Schrödinger in the coordinate basis.
5. **The Fourier payoff**: ⟨x|p⟩ = plane wave ⇒ the momentum wavefunction
   is the Fourier transform of the position one — the bridge promised in
   Three Names' Onward, now proved. Fills the notes' open question "почему
   |p⟩ — собственный вектор p̂".
6. Commutator [x̂,p̂] = iħ (computed!), common-eigenbasis theorem (§9
   proof), generalized uncertainty σ_A σ_B ≥ |⟨[A,B]⟩/2i| — WITH the
   Cauchy–Schwarz proof (gap in the notes: stated there without proof),
   Heisenberg as corollary; side-by-side with Part 3's Δf·Δt.
   Notebook: **nb-wavepackets** — ψ(x) with phase-as-color, its Fourier
   twin ψ̃(p), squeeze one and watch the other spread (the uncertainty
   trade-off, interactive; reuses the Fourier road's machinery).

## QM-6. Particle in a box (problem #1)

Stationary Schrödinger equation (separation of time), infinite well:
boundary conditions ⇒ sin(nπx/L) eigenmodes, E_n ∝ n² — and the
eigenbasis is literally the Fourier sine basis: Part 1's series returns as
the energy representation. Superpositions, time evolution as rotating
phases, revivals. Notebook: **nb-box** — eigenmodes, |ψ|² animations,
measurement collapse simulation.

## QM-7. Tunneling (problem #2)

Finite well as the warm-up (bound states, transcendental equation), then
the barrier: piecewise solutions, matching, transmission/reflection
coefficients, the evanescent exponential inside the wall. Real-world
hooks: alpha decay, STM. Notebook: **nb-tunnel** — a wave packet hitting
a barrier (split-step Fourier integrator — the FFT earns its keep in the
quantum world!), T(E) curves.

## QM-8. Harmonic oscillator (problem #3)

The algebraic solution: ladder operators from [x̂,p̂] alone (the
commutator machinery of QM-5 pays off), spectrum ħω(n+½), Hermite
functions as the coordinate faces, ground state saturating the
uncertainty bound. Coherent states as the classical limit. Notebook:
**nb-oscillator** — Hermite gallery, coherent state wobbling like a
classical pendulum.

## QM-9. Hydrogen (problem #4, the finale)

The heaviest new machinery (not in the notes): 3D Schrödinger, central
potential, separation in spherical coordinates, angular momentum
operators and their algebra, spherical harmonics (derived at the depth of
the oscillator's ladder treatment — L±), the radial equation, E_n ∝ −1/n²
— closing the circle to QM-1's discrete hydrogen lines from notes §1.
Orbitals as |ψ|² geometry. Notebook: **nb-hydrogen** — spherical-harmonic
gallery, orbital cross-sections and isosurfaces.

---

## Deferred (not on the minimal path)

- Tensor products & entanglement (notes §14, multi-qubit) — act four
  material (quantum computing proper: gates, Deutsch, Grover, Shor, QFT —
  the rest of the notes are waiting).
- Spin-orbit coupling, identical particles, perturbation theory.
- Deep functional analysis of unbounded operators / rigged Hilbert spaces
  — named in cuts, never rebuilt.

## Practical notes

- New conda env `quantum-blog` for the notebooks (numpy/scipy/matplotlib,
  house palette; ipywidgets for interactivity where it helps).
- Weights: continue the ladder after Three Names (45) — QM posts at
  47, 48, ... or renumber by decades; decide at first publication.
- ipetr0v's PR #2 reviewed jointly, published in the QM-2½ slot with the
  usual protocol.
