# Fourier series — working outline

The angle that makes this series worth writing: **nobody walks the whole road from
the basic math to the spectrogram** — existing explanations all start from some
intermediate point. We start from the very beginning and keep going.

## The roadmap (order decided 2026-07-26)

Six posts in two acts. **Act one** — the three-part "From the Fourier Series
to the Spectrogram". **Act two** — three follow-ups, in this order: Four
Shades (introduces the Fourier *transform* and connects all four creatures)
→ the Kotelnikov proof (pays the debt teased in Part 2) → F0 & the cepstrum
(the finale: everything applied to the voice).

### Act one. From the Fourier Series to the Spectrogram — three parts
Based on the DSP lecture (see `lecture_digest.md`; deck: [Google Slides](https://docs.google.com/presentation/d/1Cte6w0t8yTJRFirde6GPxKB29VX3SrX1mhAkKYEN-n4/)).

- **Part 1: From Sound to the DFT** — **published 2026-07-26** ✔
  (`content/posts/fourier-series-to-spectrogram-part-1/`).
- **Part 2: Reading the DFT** — **published 2026-07-26** ✔
  (`content/posts/fourier-series-to-spectrogram-part-2/`), with the
  companion notebook `notebooks/reading_the_dft.ipynb`.
- **Part 3: From the DFT to the Spectrogram** — **published 2026-07-26** ✔
  (`content/posts/fourier-series-to-spectrogram-part-3/`), with the
  companion notebook `notebooks/building_the_spectrogram.ipynb`.

### Act two, post 1. Four Shades of Fourier
Role in the series: introduces the **Fourier transform** proper (continuous
time, continuous frequency — the one shade we have never defined) and builds
the bridges between all four shades; the "discrete in one domain ⇔ periodic
in the other" law, proved bottom-up for the DFT in Part 2, becomes the
organizing principle of the whole 2×2 table.
Title decided ✔ (Four/Fourier pun; the four shades are FS, FT, DTFT, DFT).
Base text: `shades_draft.md` (from the Notion draft; formulas already in LaTeX).
Centerpiece diagram (house SVG style): the 2×2 matrix —

|                    | continuous time | discrete time |
|--------------------|-----------------|---------------|
| continuous frequency | FT            | DTFT          |
| discrete frequency   | FS            | DFT           |

with the duality "periodic in one domain ⇔ discrete in the other" as the connecting idea.

TODOs inherited from the draft:
- funny intro idea: https://angeloyeo.github.io/2019/06/23/Fourier_Series_en.html
- formulas for the different Fourier coefficients side by side
- FT works for any integrable function — Zorich vol. II, p. 524
- figures: redraw the YSDA speech-course screenshots in our style / regenerate in matplotlib

### Act two, post 2. The theorem with three names: Kotelnikov / Shannon–Nyquist
Promised explicitly in Part 2 (the theorem is stated there, with the
"sinusoid at exactly $f$" fine print and aliasing both left as debts).
Perfect reconstruction of a continuous signal from its samples, provided the
spectrum is band-limited to $f_s/2$. Named differently in different
traditions: Kotelnikov (1933), Shannon (1949), Nyquist (the critical rate),
with Whittaker (1915) as the prequel — a naming story worth telling in itself.
Arc: what "band-limited" means → the theorem statement → proof sketch through
the Four Shades machinery (sampling makes the spectrum periodic; if the copies
don't overlap, the original spectrum is recoverable — cut one copy out, done)
→ sinc interpolation as the reconstruction formula → aliasing when the
condition fails (wagon-wheel effect, why 44.1 kHz) → demos in matplotlib.
Natural sequel to Four Shades: the periodized-spectrum picture *is* the proof.

### Act two, post 3 (the finale). F0, pitch and the cepstrum: reading the voice
Source: TTS lecture deck ([Google Slides](https://docs.google.com/presentation/d/1hR4koanl61qFXNAk2SRp45gYcgxUAc5Xt6_UQJMJYmM/), slides 26–38; local copy in scratchpad).
Arc: F0 & harmonics (Fourier series made flesh) → pitch as perception, the
missing-fundamental effect → when F0 exists: voiced vs whispered/voiceless
(reading spectrograms in practice) → finding F0: periodicity *of the spectrum*
→ the cepstrum (FFT of the log-spectrum, quefrency; "T became 1/T" duality
callback to Four Shades) → limitations (subharmonics, voiced/unvoiced).
Diagrams to draw: harmonic comb with period F0; cepstrum pipeline; missing
fundamental illustration.

### Later candidates
FFT (why O(n log n)), windowing and leakage, mel scale / mel-spectrograms
(bridge to the speech course), uncertainty principle, LTI systems &
convolution (sinusoids as eigenfunctions, why frequencies never mix — the
post-1 inset links dspguide ch. 5 for now and deliberately makes no promise).

## Sources
- The lecture deck + speaker notes (English, rich "fun facts")
- `shades_draft.md` — Notion draft with the math skeleton
- ru.dsplib.org is dead, but fully archived. Recipe: prepend
  `https://web.archive.org/web/2026/` to any dsplib URL — the archive
  redirects to the nearest snapshot. Verified working:
  [discrete_introduction](http://web.archive.org/web/20260514053433/https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)
  (full text intact as of May 2026). Key chapters for the series: `content/dft/dft.html`,
  `content/fourier_transform_delta_func/…`, `content/discrete_introduction/…`.
  Consult and cite via archive links; do **not** copy the text into this
  (public) repo — it is someone else's authored content.
- Lena Voita of the Fourier world is yet to be found :)
