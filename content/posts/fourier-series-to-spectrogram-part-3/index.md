---
title: "From the Fourier Series to the Spectrogram, Part 3: From the DFT to the Spectrogram"
date: 2026-07-26
draft: true
tags: ["fourier", "dsp", "speech"]
summary: "Part 3 of 3: cut the signal into frames, pay for the cut with leakage, patch it with windows, stack the columns — the spectrogram, and its mel-compressed cousin that speech models actually consume."
math: true
---

[Part 2](/posts/fourier-series-to-spectrogram-part-2/) ended on an
asymmetry. The waveform of a spoken phrase knows *when* — you can count the
words in it — but no frequencies. Its spectrum knows *what* — every
frequency of every phoneme — but stacked into one column of numbers with no
notion of time. A chord survives such a summary; a sentence does not. Speech
is **non-stationary**: its spectrum changes many times per second, and the
whole point of listening is to follow the changes.

This closing part builds the tool that keeps both answers at once. The plan
writes itself: if one spectrum for the whole recording is too coarse, take
*many* — cut the signal into short pieces and transform each piece
separately. Everything else in this post is the honest accounting for that
one idea: what the cutting costs (spectral leakage), how to soften the blow
(windows), what the assembled picture is (the spectrogram), which trade-off
it can never escape (time versus frequency), and one final compression pass
borrowed from your own ear (the mel scale).

## Cut the signal into frames

Slide a short **window** along the recording and take the DFT of each
position separately. Each windowed stretch is called an **(acoustic)
frame**, and two numbers govern the slicing: the **window length** $W$ —
how many samples each frame holds — and the **hop length** $H$ — how far
the window advances between frames. With $H \lt W$ the frames overlap,
and every sample gets seen by several of them:

![A recording cut into overlapping frames](framing.png)

Formally, this is the **[Short-Time Fourier
Transform](https://en.wikipedia.org/wiki/Short-time_Fourier_transform)**
(STFT): the DFT of Part 2, applied to the $m$-th frame,

$$
\mathrm{STFT}[m, k] = \sum_{n=0}^{W-1} x[m H + n]\; w[n]\; e^{-2 \pi i \frac{k n}{W}},
$$

where $w[n]$ is a **window function** whose job we are about to discover —
for now, imagine $w[n] \equiv 1$, a plain rectangular cutout. The result is
indexed by *two* integers: $k$ still means "which frequency", exactly as in
Part 2, and the new index $m$ means "which moment". This is the whole idea;
the rest of the post is fine print. But in signal processing, as we have
learned twice already, the fine print is where the theorems live.

## The price of cutting: spectral leakage

Here is the debt from Part 2 coming due. Remember how the DFT was derived
in Part 1: we took $N$ samples and **glued copies of them end to end** —
the Fourier series demanded a periodic function, so we manufactured one.
That construction is still inside the machine: *the DFT of a frame is
honestly analyzing the infinite periodic signal made of glued copies of
that frame.*

Part 1 also showed what gluing demands: whatever happens on the frame must
join seamlessly to its own copy. A frequency that completes a whole number
of turns per frame arrives at the seam exactly where it started — its
copies glue smoothly, and the DFT gives it one clean bin. But our window
now lands wherever it lands: no real oscillation consults the frame
boundaries. A tone that completes, say, $8.5$ turns arrives at the seam
mid-swing — and the glued copies **tear**:

![On-grid tone: seamless copies, clean spike; off-grid tone: torn seam, smeared spectrum](leakage.png)

The DFT does not complain; it reports what it sees. And what it sees is a
signal with a *jump* at every seam — and jumps, as the square wave showed
us back in Part 1, take a whole choir of frequencies to build. So the
energy of one pure tone **leaks** across the spectrum: a tall pair of bins
where the tone roughly is, and a skirt of nonzero magnitudes everywhere
else. This is **spectral leakage** — Part 2's "not in the vocabulary"
effect, finally caught in the act. (You have already met it once: in the
Part 2 notebook, the strange *dip* between the two nearly-resolved notes
was the leakage skirts of two off-grid tones interfering.)

## Windows: taper, don't chop

The tear happens at the frame's edges — so treat the edges. Instead of
cutting the signal out with a rectangular cookie-cutter, multiply the frame
by a **[window function](https://en.wikipedia.org/wiki/Window_function)**
that rises smoothly from zero and falls smoothly back: whatever the signal
was doing, the *windowed* frame now starts and ends at zero, and the glued
copies meet without a jump. The standard first choice is the **Hann
window**,

$$
w[n] = \tfrac{1}{2} \left( 1 - \cos \tfrac{2 \pi n}{W - 1} \right).
$$

![The Hann window, a tapered frame, and the leakage suppressed](windowing.png)

Look at the right panel (magnitudes in **dB** — decibels, a logarithmic
scale; we will justify it in a moment). The rectangular cut leaves a skirt
decaying so slowly that a strong tone can drown quiet neighbors three
octaves away; the Hann window pushes the skirt down by tens of dB. The
price, visible at the very top: the central peak becomes about *twice as
wide* — a windowed tone occupies two-ish bins even when perfectly on-grid.
Windowing trades a little blur near the true frequency for enormous
cleanliness far from it. (There is a whole zoo of windows — Hamming,
Blackman, Kaiser — each choosing this trade slightly differently; the Hann
window is the workhorse default in speech.)

## The spectrogram

Now assemble. Compute the windowed DFT of frame $0$, frame $1$, frame $2$,
…; keep only the informative half of each spectrum (Part 2's mirror);
take magnitudes; stand each result upright as a column and line the columns
up in time order. The resulting matrix — frequency up the side, time along
the bottom, magnitude as brightness — is the **spectrogram**:

![The spoken phrase and its spectrogram](speech_spectrogram.png)

The same phrase as in Part 2 — but where the whole-recording spectrum
collapsed every syllable into one anonymous forest of peaks, the
spectrogram lays the sentence out like a musical score. Read it top to
bottom and left to right:

- **the bright horizontal striations** in the lower half are the harmonics
  of the voice — the Fourier series of Part 1, alive and visible, one row
  per harmonic; their spacing is the pitch of the speaker;
- **the tall unstructured columns** reaching high frequencies are the
  hissy consonants — "s", "f", "sh" — noise-like sounds with energy smeared
  across the spectrum;
- **the dark vertical gaps** are the silences between words: the *when*
  that Part 2's spectrum had lost is back on the horizontal axis.

Two familiar knobs decide the geometry of this picture, and both are Part 2
veterans. The **sampling rate** sets the ceiling: rows run from $0$ to
$f_s/2$, the Nyquist frequency — nothing above the ceiling exists on the
grid. The **window length** sets the resolution: each column is a
$W$-sample DFT, so its rows are spaced $\Delta f = f_s / W$ apart — the
number of rows *is* the window length (divided by two). And one new knob:
the **hop length** sets the frame rate of the movie — how many columns per
second of signal.

> 💡 **Why dB?** Spectrogram magnitudes are conventionally shown as
> $20 \log_{10}$ of the magnitude — **decibels**. Two reasons. First, the
> dynamic range: the loud harmonics and the quiet fricative hiss differ by
> factors of thousands; on a linear brightness scale everything but the
> harmonics would be black. Second, the ear: loudness perception is itself
> roughly logarithmic, so equal steps in dB feel like equal steps of
> loudness. The picture is drawn the way it is heard.

> 💡 **Typical numbers for speech:** window $\approx 25$ ms, hop
> $\approx 10$ ms — a hundred columns per second, each with a
> $\Delta f = 40$ Hz grid. Why 25 ms? Short enough that speech barely
> changes within one frame (quasi-stationarity), long enough to resolve
> the harmonics of a typical voice. The next section is about why you
> cannot have both at once.

## The trade-off you cannot escape

Part 2 proved a hard law: $\Delta f = 1/\text{duration}$ — frequency
resolution is one over the listening time. In the STFT, "listening time"
is the window length, and the law becomes a genuine dilemma. A *short*
window pins events precisely in time but smears them in frequency; a
*long* window resolves frequencies finely but averages away the timing.
Watch the law act on a **chirp** — a tone whose frequency climbs steadily:

![One chirp under a short and a long window](chirp_tradeoff.png)

The short window draws a crisp thin line: within each 32 ms frame the chirp
is nearly a constant tone, and $\Delta f = 31$ Hz is plenty. The long
window has $\Delta f = 3.9$ Hz — eight times sharper on paper — yet its
picture is *worse*: during each 256 ms frame the chirp sweeps through
hundreds of hertz, and the fine frequency grid resolves a smear. Sharper
$\Delta f$ bought blurrier time, and for this signal time was where the
action lived.

There is no window length that wins both ways — only a choice matched to
the signal. This is not an engineering shortcoming but mathematics: time
locality and frequency locality are fundamentally at odds (the same tension
that in quantum mechanics goes by the name *uncertainty principle* — a
story for another day). The speech-processing compromise from the previous
section — 25 ms — is simply where the trade sits comfortably for human
voices.

## The mel scale: compress like the ear does

The spectrogram is already a fine input for a machine. But it spends its
rows wastefully — from the *listener's* point of view. Your ear does not
weigh all frequencies equally: the
[cochlea](https://en.wikipedia.org/wiki/Cochlea) resolves low frequencies
finely and high frequencies coarsely. Neighboring keys at the bottom of a
piano differ by a couple of hertz and you hear the step clearly; at the top
of the keyboard the same one-semitone step is a couple of *hundred* hertz —
and sounds no bigger. Perceptually, frequency is closer to logarithmic than
linear.

The **[mel scale](https://en.wikipedia.org/wiki/Mel_scale)** (from
*melody*) is a practical approximation of that perception, fitted to
listening experiments:

$$
m = 2595 \, \log_{10}\!\left(1 + \frac{f}{700}\right).
$$

Equal steps in mel are meant to sound like equal steps of pitch — which
means the scale walks slowly through the low frequencies (where the ear
discriminates finely) and takes ever-larger strides up high:

![The mel curve and a mel filter bank](mel_scale.png)

To convert a spectrogram, build a **mel filter bank** $F$: a few dozen
triangular filters, evenly spaced *in mel* — therefore narrow and dense at
low frequencies, wide and sparse at high ones (bottom panel above). Each
filter takes a weighted sum of the spectrogram rows it covers, so the whole
conversion is one matrix multiplication per column,

$$
M = F \cdot S,
$$

followed by the same logarithm as before. The result is the
**mel-spectrogram**:

![The spectrogram and its mel-compressed version](mel_spectrogram.png)

Hundreds of linear-frequency rows become a few dozen mel bands, spending
their budget where the ear spends its attention — the harmonics-rich bottom
gets most of the rows, the hissy top is summarized coarsely. This picture —
compact, perceptually weighted, still laid out in time — is the actual
input of most speech recognition and synthesis models: when a paper says
"we feed the audio to the network", this matrix is almost always what is
being fed.

## The road, walked

This is where the series set out to arrive, so let us look back at the
whole road. A pressure wave shook a microphone, and an ADC turned the
voltage into $N$ numbers (Part 1). To do mathematics with those numbers we
built them an honest home — deltas, sifting, the comb — and the Fourier
series itself handed us the DFT (Part 1). We learned to read the DFT's
output: which bin is which hertz, why resolution is one over duration, why
half the spectrum is a mirror (Part 2). And today we made the Fourier view
local — frames, windows against the leakage, the spectrogram, and the mel
compression that matches the ear (Part 3). From air molecules to the input
tensor of a speech model, with no step taken on faith.

The journey of this series continues past the trilogy. The **Fourier
transform** proper — continuous time, continuous frequency, the one shade
we never defined — and the family bridges between all four shades are next.
Then the **theorem with three names** gets its promised proof (one picture,
as vowed in Part 2). And the finale reads the human voice itself: **F0,
pitch and the cepstrum**. The four shades await.
