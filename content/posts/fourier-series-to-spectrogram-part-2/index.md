---
title: "From the Fourier Series to the Spectrogram, Part 2: Reading the DFT"
date: 2026-07-26
draft: true
tags: ["fourier", "dsp", "speech"]
summary: "Part 2 of 3: learning to read the DFT's output — which bin is which frequency, why resolution is one over duration, the mirror symmetry, and the Nyquist frequency."
math: true
---

[Part 1](/posts/fourier-series-to-spectrogram-part-1/) ended with the machinery
built. The Discrete Fourier Transform takes the $N$ samples of a recording and
returns $N$ complex numbers:

$$
X[k] = \sum_{n=0}^{N-1} x[n]\, e^{-2 \pi i \frac{k n}{N}}, \qquad k = 0, 1, \dots, N-1.
$$

$N$ numbers in, $N$ numbers out — and every trace of physical time gone: the
formula sees only the two integers $k$ and $n$. That was a feature during the
derivation, but it leaves us unable to answer the simplest practical question.
Back in Part 1 we removed a power-line hum by "erasing one column of the
spectrum" — well, *which* column? Which $k$ is 50 Hz? This part is about
learning to read the DFT's output: matching indices to physical frequencies,
seeing what the resolution of that matching costs, and discovering along the
way why half of the output is a mirror image of the other half.

## What does X[k] measure?

Look at the DFT formula through the lens of the inner product we introduced
while proving the sifting property in Part 1: multiply two signals pointwise,
sum up — with the sum over a continuum becoming an integral, and, for complex
signals, the second factor conjugated. The DFT sum is *exactly* that, in the
finite-dimensional case the notation came from:

$$
X[k] = \sum_{n=0}^{N-1} x[n]\, \overline{w_k[n]} = \langle x, w_k \rangle,
\qquad
w_k[n] = e^{2 \pi i \frac{k n}{N}}.
$$

Each coefficient is the inner product of the signal with one **basis
oscillation** $w_k$ — a number that measures how much the signal *resembles*
that oscillation, exactly like a dot product measures how much one vector
leans along another. As $n$ runs through the $N$ samples, the exponent of
$w_k$ grows to $2 \pi i k$: the basis oscillation makes exactly $k$ full
turns across the recording. This is Part 1's "whole number of oscillations
per period" rule wearing its discrete clothes: the DFT offers us $N$ probe
frequencies — zero turns, one turn, two turns, … — and reports the signal's
resemblance to each.

> 💡 **The $k = 0$ probe** makes zero turns: $w_0[n] \equiv 1$, and
> $X[0] = \sum_n x[n]$ is just $N$ times the *average* of the signal. Audio
> engineers call it the **DC component** (from "direct current" — the
> electrical origin shows). For sound it is normally near zero: pressure
> oscillates around the atmospheric baseline, and the microphone measures
> only the deviation.

(For a lovely interactive treatment of these facts, see [chapter 5 of Brian
McFee's *Digital Signals Theory*](https://brianmcfee.net/dstbook-site/content/ch05-fourier/DFT.html) —
the source of several pictures this part reimagines.)

## From the index to hertz

So $X[k]$ measures the content of "$k$ turns per recording". To turn that
into hertz, bring back the physical time that the DFT so pointedly forgot.
The $n$-th sample was taken at $t = nT$, and the whole recording lasts $NT$
seconds — so "$k$ full turns per recording" is the physical frequency

$$
f_k = \frac{k}{NT} = k \frac{f_s}{N},
$$

where $f_s = 1/T$ is the sampling rate. The probe frequencies are not
arbitrary: they form a uniform grid with step

$$
\Delta f = \frac{f_s}{N} = \frac{1}{NT},
$$

called the **frequency resolution** — no probe exists between $f_k$ and
$f_{k+1}$, so the DFT simply cannot distinguish frequencies closer together
than $\Delta f$.

Now, a question worth pausing on. The sampling rate is not really ours to
choose — it is a property of the microphone and the ADC, fixed in hardware.
The one knob we do control is $N$: how many samples we feed the transform.
**What exactly does that knob turn?** Watch the $k = 1$ basis oscillation —
"one turn per recording" — as $N$ grows at a fixed sampling rate:

![The k = 1 basis stretches as N grows at a fixed sampling rate](basis_stretch.png)

The basis rides the *window*, not the clock: more samples at the same rate
means a longer recording, and the one turn of $w_1$ spreads over it — its
physical frequency $\Delta f = \frac{1}{NT}$ drops. And since every other
probe sits at a multiple of it, the whole frequency grid tightens:

![Recording longer buys a finer frequency grid](freq_resolution.png)

That is what the knob turns. Look at the second formula for $\Delta f$
again: $NT$ is simply the *duration* of the recording, so

> $\Delta f = \dfrac{1}{\text{duration}}$ — **frequency resolution is one over the listening time.**

To tell two tones one hertz apart, you must listen for at least a second —
only then does the slower tone fall a full turn behind and the difference
become visible. There is no way around this trade, only a choice along it:
this very tension — resolution in frequency versus locality in time — will
return as the central design decision of the spectrogram in Part 3.

A worked example in unforgiving numbers: at $f_s = 8000$ Hz, taking
$N = 100$ samples (an eighth of a second) gives
$\Delta f = 8000 / 100 = 80$ Hz. That grid is too coarse to tell middle C
(262 Hz) from the B just below it (247 Hz): both land in bin $k = 3$. To
separate them you need $\Delta f$ around their 15 Hz gap — that is
$N \approx 530$ samples, a fifteenth of a second. Music transcription from
spectra is possible, but the resolution bill must be paid first.

## The spectrum, at last

We can now do properly what Part 1 could only preview: plot the magnitudes
$|X[k]|$ against their physical frequencies $f_k$. This picture is the
**(magnitude) spectrum** of the recording:

![Two signals and their magnitude spectra](simple_spectra.png)

A pure sine shows up as a single spike on an empty axis (well — *two*
spikes; hold that thought), and a mix of three sines as three spikes with
the right heights, each recoverable at a glance. This is the "hundreds of
numbers → three meaningful ones" compression promised at the very start of
Part 1 — delivered.

What about the other half of the complex number? Each $X[k]$ carries a
magnitude *and* a phase, and the phase stores where in its cycle the $k$-th
oscillation starts — Part 1's $\phi_n$, one per harmonic. Much of speech
processing works with magnitudes alone: what a vowel sounds like, which note
was played, whether the hum is there — all of it lives in the magnitudes.
The phase becomes essential the moment you need to rebuild the *waveform* —
shifting every component back to its proper starting point — which is why
speech synthesis and enhancement systems must treat it with care while a
speech recognizer can throw it away.

## The mirror

Now to the promised puzzle: why does a single 4 Hz sine light up *two*
bins? Compute the coefficient at index $N - k$ for a real-valued signal,
using $e^{-2\pi i n} = 1$ one more time:

$$
\begin{aligned}
X[N-k] &= \sum_{n=0}^{N-1} x[n]\, e^{-2 \pi i \frac{(N-k) n}{N}} \\
       &= \sum_{n=0}^{N-1} x[n]\, e^{2 \pi i \frac{k n}{N}}
        = \overline{X[k]}.
\end{aligned}
$$

The second half of the spectrum is the complex conjugate of the first, read
backwards: $|X[N-k]| = |X[k]|$. Every spike below the middle has a twin
above it, and the spectrum of any real signal is symmetric about $k = N/2$.

We have met this mirror before. Part 1's exponential form split every real
oscillation into a forward- and a backward-rotating exponential, with
$c_{-n} = \overline{c_n}$ — and we promised the symmetry would resurface in
the DFT. Here it is: by the periodicity $c_{k+N} = c_k$ that we proved when
deriving the DFT, the coefficient $c_{-k}$ *is* $c_{N-k}$. The upper half of
the DFT output is precisely the negative-frequency half of the spectrum,
wrapped around by periodicity into the range $k = N/2, \dots, N-1$. The twin
spike at "96 Hz" is really the spike at $-4$ Hz, filed under an alias.

> 💡 **Do the books still balance?** If half of the output mirrors the other
> half, doesn't the DFT return only $N/2$ numbers' worth of information for
> $N$ numbers of input? Count the *real* degrees of freedom (say $N$ is
> even). $X[0]$ is a sum of real samples — real, one number. $X[N/2]$ pairs
> with itself in the mirror ($N - N/2 = N/2$), forcing
> $X[N/2] = \overline{X[N/2]}$ — real, one number. The remaining $N - 2$
> coefficients come in conjugate pairs, each pair carrying one independent
> complex number — two real ones. Total: $1 + 1 + \frac{N-2}{2} \cdot 2 = N$
> real numbers. Exactly the information content of $N$ real samples — the
> books balance to the cent, as they must for an invertible transform.

## The Nyquist frequency

The mirror axis itself deserves a name. The probe at the fold, $k = N/2$,
is the oscillation

$$
w_{N/2}[n] = e^{2 \pi i \frac{(N/2) n}{N}} = e^{\pi i n} = (-1)^n
$$

— the sequence $+1, -1, +1, -1, \dots$, flipping sign at every single
sample. No oscillation representable on the grid can flip faster: there is
nothing between the samples to flip *in*. Its physical frequency,

$$
f_{N/2} = \frac{N}{2} \cdot \frac{f_s}{N} = \frac{f_s}{2},
$$

is the **Nyquist frequency** — the ceiling of what a given sampling rate can
represent, sitting always at exactly half of it. Everything above the
ceiling and below $f_s$ is the mirror land we just mapped. So here is the
full geography of the DFT's frequency axis on one picture:

![The frequency axis of the DFT: resolution, Nyquist frequency, sampling rate](freq_axis_map.png)

The genuinely informative range runs from $0$ to $f_s/2$ — which finally
explains a number from Part 1: CD audio samples at 44.1 kHz because its
ceiling must clear the ~20 kHz limit of human hearing, with a little
engineering margin on top.

One question this part leaves deliberately open: the ceiling is a statement
about what the *grid* can represent — but the analog world does not consult
our grid. What happens if the sound contained frequencies above $f_s/2$
*before* sampling? They do not politely disappear; they fold back into the
visible range under false names. That story — **aliasing**, and the theorem
with three names that tells you exactly when you are safe from it — deserves
a post of its own.

## Onward

We can now read a spectrum: find any frequency's bin, trust the left half,
ignore the mirror, and budget the resolution by the length of the recording.
But notice what the DFT gives us: *one* spectrum for the *entire* signal.
A chord is a fine thing to summarize with one spectrum — a melody is not:
"which notes appear" is not the same as "which notes appear *when*". In
**Part 3** we make the Fourier view local — slide a window along the
recording, pay the resolution bill we just learned about at every stop, and
stack the results into the picture this series is named after: the
spectrogram.
