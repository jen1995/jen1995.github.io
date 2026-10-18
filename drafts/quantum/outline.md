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

## Status (2026-10-18)

- QM-1 *The Apparatus and the Arrow* (weight 47) and QM-2 *States Are
  Vectors* (48) published 2026-09-06; QM-2½ *From Kronecker Delta to Dirac
  Delta* (49, with Ivan Petrov) published 2026-10-18 with the companion
  notebook `notebooks/kronecker_to_dirac.ipynb`. Transformers/VAE moved to
  weights 80/90; next quantum posts take 50, 51, …
- Material cut from the delta post and kept for later posts is in
  `drafts/quantum/delta_post_cuts.md` (Born-rule/density remark, separability
  remark, the very-large-box section).
- QM-3 drafted 2026-10-18 as content/posts/observables-and-the-born-rule/
  (weight 50, draft: true): operators from the spin, the three conditions,
  the Born rule from basis independence (her §7), expectation values,
  Hermitian operators, σ_z and σ_x from the experiments (σ_y waits for the
  i/o states in QM-4), measurement as projection. Under review.

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

## Thread: spectra — discrete, continuous, mixed (added 2026-09-06)

Eugenia's find while reviewing QM-2: the hydrogen energy spectrum is
*mixed* — countably many bound levels E_n ∝ −1/n² crowding toward the
ionization threshold, and a continuous spectrum above it (ionized
electron). These are exactly the point/continuous spectra of
self-adjoint operators from functional analysis, and the four problem
posts form a natural taxonomy: box = purely discrete, tunneling =
purely continuous, hydrogen = both. Not a separate post — a thread with
one home:

- **QM-3 (observables)**: when stating "eigenvalues = outcomes", name
  the word *spectrum* and say honestly that in infinite dimensions it
  need not be pure point; cut with a pointer to the spectral theorem for
  self-adjoint operators (discrete vs continuous spectrum).
- **QM-2½ / QM-5**: position and momentum as the first operators with
  purely continuous spectrum — the "eigenvectors" |x⟩, |p⟩ are not
  normalizable, live outside the Hilbert space, and are normalized to a
  delta, ⟨x|y⟩ = δ(x−y) (rigged Hilbert space *named*, not built).
- **QM-7 (tunneling) — the thread's home**: unbound (scattering) states
  as the physics of the continuous spectrum; plane waves vs wave packets;
  why T(E) is a function of a continuous variable while the box had a
  discrete list.
- **QM-9 (hydrogen) — the payoff**: one operator, both kinds of spectrum;
  the ionization threshold as the boundary; bound orbitals vs scattering
  states. Closes the circle to QM-2's "countably many outcomes" example.

## Notes from Eugenia's dad (consultation 2026-10-11), mapped to the road

Source: a physicist's view of "any QM problem". Where each remark lands:

- **Scope.** All problems split into one-particle (barrier, levels, wells —
  "the domain of QM proper") and many-particle (beyond it). Our four
  problems are all one-particle; say so in QM-6's intro. Many-body / QFT
  stays deferred (his pointers: A. Zee, *QFT in a Nutshell* — has problems
  and solutions; Peskin & Schroeder, *Introduction to QFT* — "with a
  teacher").
- **QM-2½ (the box) — written, then cut from the delta post on 2026-10-18;
  text kept in drafts/quantum/delta_post_cuts.md.** "Physicists always mean
  a discretized Hilbert space": a very large box quantizes momentum
  (k_n = 2πn/L), box-normalized plane waves are Kronecker-orthonormal, and
  L → ∞ gives Σ_n → (L/2π)∫dk and ⟨k|k′⟩ = δ(k−k′) — our grid construction
  with position ↔ momentum swapped (box ↔ grid, 2π/L ↔ Δx, 1/√L ↔ 1/√Δx).
  New home: QM-3 or QM-5, next to eigenbases of operators — it answers why
  practice talks in boxes and discrete momenta rather than in deltas.
- **QM-3 (observables).** Kets are chosen by solving the one-particle problem:
  the eigenbasis of the Hamiltonian; observables are averages ⟨ψ|A|ψ⟩; a
  concrete representation = bra times ket, ⟨p|1⟩ "take the first function
  in the p-representation". History pointers for references: Dirac's
  *Principles* and Pauli's lectures (how the operator table arose).
- **QM-5 (dynamics).** His "scheme for mathematicians": start from the
  transformation operator (translation, rotation, time shift) → its
  infinitesimal version (Taylor around the identity) → the generator → the
  Lie algebra of the symmetry group; momentum is conserved only with
  translation symmetry, angular momentum with rotational, energy with time
  translation. This IS the generator section of QM-5 (§11 of the notes) —
  present it as "the three symmetries from which all operators of QM are
  built". Exercise idea (for nb-tunnel / QM-7): rewrite the barrier problem
  in the p-representation, p²/2m, then in the energy basis — practice
  changing bases without clinging to any one.
- **QM-6 (box).** Physical framing: quantization comes from boundary
  conditions (zero at the walls = infinite potential). A qubit in hardware
  is "a large potential well for electrons"; a crystal is a 3D well
  (silicon, germanium — flat inside, barrier at the boundary); a quantum
  dot = a 3D well ("circular harmonics"); hydrogen is a Coulomb potential,
  NOT a well. Mesoscopics as a cut: once the well is smaller than microns
  the shape of the boundary matters (graphene edges: armchair vs zigzag);
  larger — it does not. Box quantization of momentum for a cm-sized
  imaginary cube → discrete momenta → momentum representation as the
  infinite-box limit (ties back to the box text in delta_post_cuts.md).
- **QM-7 (tunneling).** Slowly varying potential → locally constant → piece
  together box solutions: the WKB idea, as a cut.
- **Contraction mapping (Banach fixed-point) theorem** — his general
  remark: "a very important theorem of functional analysis, important in
  practice", not tied to one place. Natural landings on our road: QM-5, a
  cut on *why* time evolution exists and is unique — Picard iteration for
  i d/dt|ψ⟩ = H|ψ⟩ is a contraction on a short time interval, and its limit
  is the exponential U(t) = e^{−iHt}; QM-7, the Born series for scattering
  as a fixed-point iteration (Lippmann–Schwinger). Also the honest reason
  iterative numerical solvers in the notebooks converge.
- **QM-9 (hydrogen).** Rotations → angular momentum as the generator →
  SO(3), Casimir operator L² — his route to spherical harmonics; aligns
  with the plan to derive them at the depth of the oscillator's ladder.
- **General.** "The physicist's criterion is the experiment, not whether the
  mathematics converges" (his aside on SR paradoxes) — a candidate sentence
  for a rigor-policy cut. Textbooks he recommends (all two-volume, Russian
  editions exist): von Neumann, *Mathematical Foundations of QM* (Nauka
  1964; English 1955 on archive.org); Richtmyer, *Principles of Advanced
  Mathematical Physics* (Mir 1982/84); Messiah, *Quantum Mechanics* (Nauka
  1978/79); also Kato, *Perturbation Theory for Linear Operators* (Mir 1972)
  for the spectral-theory side; Mackey, *Mathematical Foundations of QM*
  (1963, free on archive.org) — compact axiomatics, good for QM-3.

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
