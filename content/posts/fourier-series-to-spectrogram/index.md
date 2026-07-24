---
title: "From the Fourier Series to the Spectrogram"
date: 2026-07-24
draft: true
tags: ["fourier", "dsp", "speech"]
summary: "The whole road, walked end to end: from air pressure and a guitar string, through sampling and the Fourier series, to the DFT and the spectrogram that speech models actually consume. First post of the Fourier world series."
math: true
---

Open any tutorial on speech processing and you will meet the spectrogram in the
first five minutes — usually with a hand-wave: "we apply the Fourier transform in
sliding windows". Open a math textbook, and you will find the Fourier series in
its full rigor — with no hint of why an ML engineer should care. The road between
these two points is almost never walked end to end: every explanation starts
somewhere in the middle. This post walks the whole road: from air pressure and a
guitar string, through sampling and quantization, through the Fourier series and
the DFT, to the spectrogram — the picture that speech models actually consume.

Along the way we will meet several *different* creatures that all answer to the
name "Fourier": the Fourier **series**, the Fourier **transform**, its
**discrete-time** cousin, and the **discrete** Fourier transform. They form a
tidy 2×2 family — and untangling their family relationships is a story of its
own, which gets a separate post (and more): for now, one picture as a teaser.

![Four Shades of Fourier](four_shades_of_fourier.svg)

*(a teaser of the next post — in this one we walk the bottom row: from the Fourier series to the discrete Fourier transform)*

## What is sound

The air around us is filled with molecules. Pull a guitar string — it creates a
vibration that travels through them as alternating zones of compression and
rarefaction: a pressure wave. A microphone senses exactly this: variations of
pressure relative to the atmospheric baseline. Plot that pressure against time —
and you get the most honest picture of sound there is: the **waveform**.

> 💡 Sound is a *mechanical* wave — it needs a
> medium. In the vacuum of space there is nothing to compress, which is why we
> can see the Sun but cannot hear it.

![From a vibrating string to the waveform](sound_to_waveform.svg)

## Analog → digital

The microphone's output is an analog signal: continuous in time and in value. A
computer needs numbers, and the Analog-to-Digital Converter produces them by
discretizing along both axes:

- **sampling** — measure the signal at regular moments, $f_s$ times per second
  (time discretization);
- **quantization** — round each measurement to the nearest level of a fixed grid
  (amplitude discretization).

The result — a sequence of integers at a fixed rate — is **Pulse-Code
Modulation (PCM)**, the format inside every WAV file. Two numbers fully describe
the grid: the sampling rate (e.g. 44.1 kHz) and the bit depth (e.g. 16 bits).

![Sampling and quantization](sampling_quantization.png)

## Why the waveform is not enough

The waveform is honest but unhelpful. One second of CD-quality audio is 44,100
numbers — and no individual number tells you anything about what you hear. Is
this a male or a female voice? Which note is the guitar playing? Is there a
hum from the power line polluting the recording? Staring at pressure values
will not answer any of these questions.

Fourier's idea flips the axis. A complex signal can be decomposed into a sum of
simple oscillations — the way a chord can be decomposed into individual notes.
Instead of asking "what is the pressure at each moment of time?", we ask "how
much of each frequency does this signal contain?" The answer lives on the
frequency axis rather than the time axis, and it is called the **spectrum**.

![A C-major chord: three notes in time, three peaks in frequency](chord_decomposition.png)

If decomposing sound into frequencies feels like an arbitrary idea, think of
a piano. Pressing a key produces an oscillation at a known frequency — the
keyboard is literally a frequency axis, laid out left to right. Playing music
is easy in this direction: choose which keys to press, how hard, and when —
frequencies in, melody out. Fourier analysis asks for the reverse: given only
the recorded sound, can we recover which keys were pressed and how hard? Most
of this post is the machinery that turns this "can we?" into "here is how".

Two things make this representation valuable in practice. First, it is
**compact**: a long sequence of time samples collapses into a handful of
meaningful frequency components. The wiggly curve below takes hundreds of
numbers to store — and just three frequency components to describe:

![Hundreds of samples versus three spectral components](compact_spectrum.png)

Second, it is **actionable**: frequencies can be inspected and *edited*. Say a
recording picked up the 50 Hz hum of the power line. In the time domain the hum
is smeared over every sample and there is nothing to grab; in the frequency
domain it is one column. Transform, erase that column, transform back — the
melody survives untouched, the hum is gone:

![Removing power-line hum by zeroing one spectral column](remove_hum.png)

## The Fourier series

Let us make the "sum of simple oscillations" idea precise. We start with the
version that history started with, too: a **periodic** function.

Any periodic function $x(t)$ with period $P$ that is absolutely integrable over
$\left[-\frac{P}{2}, \frac{P}{2}\right]$ can be represented as a **Fourier
series**:

$$
x(t) = a_0 + \sum_{n = 1}^\infty \left( a_n \cos\!\left( 2 \pi \frac{n}{P} t \right) + b_n \sin\!\left( 2 \pi \frac{n}{P} t \right) \right)
$$

with the coefficients

$$
a_0 = \frac{1}{P} \int_{-P/2}^{P/2} x(t)\, dt, \qquad
a_n = \frac{2}{P} \int_{-P/2}^{P/2} x(t) \cos\!\left(2 \pi \frac{n}{P} t \right) dt, \qquad
b_n = \frac{2}{P} \int_{-P/2}^{P/2} x(t) \sin\!\left(2 \pi \frac{n}{P} t \right) dt.
$$

The building blocks are sines and cosines whose frequencies are integer
multiples of $\frac{1}{P}$ — the **harmonics** of the base frequency. Nothing
else is allowed: only oscillations that fit a whole number of times into the
period.

A pair $(a_n, b_n)$ at the same frequency is really one oscillation in
disguise. Using the cosine-of-difference formula, the pair collapses into a
single cosine with an amplitude and a shift:

$$
x(t) = a_0 + \sum_{n = 1}^\infty A_n \cos\!\left( 2 \pi \frac{n}{P} t - \phi_n\right),
\qquad
A_n = \sqrt{a_n^2 + b_n^2}, \quad \phi_n = \operatorname{atan2}(b_n, a_n).
$$

Here $A_n$ is the **magnitude** of the $n$-th harmonic, $\frac{n}{P}$ its
**frequency**, and $\phi_n$ its **phase**. This form is the one to keep in
mind: *a periodic signal is a recipe — this much of this frequency, shifted by
this much.*

![Partial sums of the Fourier series of a square wave](fourier_partial_sums.png)

> 💡 **Why sinusoids, of all things?** Mathematics knows plenty of ways to
> decompose a function — why not, say, a Taylor series, with polynomials as the
> building blocks? Several reasons stack on top of each other. First, the shape
> of the data: sound is locally *quasi-periodic* — a guitar note, a vowel — and
> periodic building blocks describe such signals with a handful of
> coefficients, while a polynomial cannot even be periodic (it must run off to
> infinity) and needs ever more terms for every extra period. Second, and
> deeper: the physical world plays along. Put a speaker in one corner of a
> room, play a pure 440 Hz tone through it, and record with a microphone in
> the opposite corner. The walls reflect the sound, echoes pile on top of each
> other — yet the recording is still a 440 Hz tone: louder or quieter, shifted
> in time, but at the same frequency. The reason is one line of trigonometry:
> echoes are delayed, scaled copies, and a sum of sinusoids of one frequency —
> whatever their amplitudes and shifts — is again a sinusoid of that
> frequency.
>
> ![A room as a system: echoes are delayed scaled copies; the output tone keeps the input frequency](room_echoes.svg)
>
> (Can a room be an *anti-carpet* and make a frequency louder? It cannot add
> energy — but it can concentrate it: when the copies arrive in phase, they add
> up constructively. That is resonance, and it is exactly why your voice
> blossoms in a tiled bathroom — at the room's resonant frequencies, the
> echoes conspire in your favor.)
>
> The same holds for a vibrating string, a microphone membrane, an
> electronic filter: none of them can invent new frequencies. (A [distortion
> pedal](https://en.wikipedia.org/wiki/Distortion_(music)) *can* — precisely because it is not linear; that is what its "dirty"
> sound is made of.) That is *why* sound is built out of sinusoids in the first
> place, and the quasi-periodicity of the previous argument is not a lucky
> accident but physics. (Why this happens — and why it earns sinusoids the
> grand title of *eigenfunctions of linear time-invariant systems* — deserves
> its own discussion later in this series; for a very accessible standalone
> account, see [chapter 5 of The Scientist and Engineer's Guide to
> DSP](https://www.dspguide.com/ch5.htm).) Third, stability. To compare fairly, fix the
> reference point — the moment you press "record" — and delay the signal past
> it by $\tau$. The Fourier description barely notices: each coefficient
> keeps its magnitude, only its phase rotates ($c_n \mapsto c_n e^{-2\pi i n \tau / P}$ —
> the formulas are coming shortly). The Taylor description — the derivatives
> at the reference point — has no such luck: every new coefficient becomes a
> mixture of *all* the old higher-order ones. The cleanest example: $\sin t$
> and $\cos t$ are one signal shifted by a quarter period, yet one has only
> odd-degree terms and the other only even-degree ones. A note sounds the same
> whenever you play it, and the magnitude spectrum agrees; the Taylor
> coefficients do not. (It is the room argument again, in disguise: a time
> shift leaves every sinusoid being itself, just rotated — while it smears
> each monomial $t^k$ across all the degrees below it.) And finally, perception: the cochlea
> in your ear performs an approximate frequency analysis of its own — pitch
> *is* frequency. The coefficient of $t^{17}$ means nothing to your hearing;
> the amplitude at 440 Hz is the note A.

### The exponential form

One more rewrite, and the notation becomes so compact that every later formula
in this series will use it. Euler's formula,

$$
e^{i t} = \cos t + i \sin t
\quad\Longleftrightarrow\quad
\cos t = \tfrac{1}{2} \left(e^{it} + e^{-it} \right),
$$

lets us split every cosine into two complex exponentials — one rotating
"forward" and one "backward":

$$
\cos\!\left( 2 \pi \tfrac{n}{P} t - \phi_n \right)
= \tfrac{1}{2} e^{-i \phi_n} e^{2 \pi i \frac{n}{P} t}
+ \tfrac{1}{2} e^{i \phi_n} e^{-2 \pi i \frac{n}{P} t}.
$$

Absorbing the magnitudes and phases into complex coefficients, the whole
series collapses into a single sum:

$$
x(t) = \sum_{n = -\infty}^\infty c_n e^{2 \pi i \frac{n}{P} t},
\qquad
c_n = \frac{1}{P} \int_{-P/2}^{P/2} x(t)\, e^{-2 \pi i \frac{n}{P} t}\, dt.
$$

The set of coefficients $\{c_n\}$ is called the **spectrum** of the signal —
the same word we met informally above, now with an exact meaning. Each $c_n$
is one complex number that stores both the magnitude and the phase of the
$n$-th harmonic: $|c_n| = A_n / 2$ and $\arg c_n = -\phi_n$ for $n \ge 1$.

> 💡 **Wait, negative frequencies?** The sum now runs over all integers $n$,
> including negative ones — that is the price of the compact notation: each
> real oscillation split into a forward- and a backward-rotating exponential.
> For a real-valued signal the two halves are not independent:
> $c_{-n} = \overline{c_n}$, so the negative-frequency half of the spectrum is
> a mirror image carrying no new information. Remember this — the same
> symmetry will resurface in the DFT and explain why half of its coefficients
> can be thrown away.

## 🚧 Under construction

Coming next in this draft: the series-to-DFT derivation (the heart of the
post) → DFT properties → STFT, windows and leakage → the spectrogram → the mel
scale. Roadmap and slide pointers: `drafts/fourier/post1_draft.md`.
