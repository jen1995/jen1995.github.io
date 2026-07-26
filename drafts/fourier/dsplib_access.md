# Accessing ru.dsplib.org (the site is dead, the archive is not)

## The recipe

Prepend `https://web.archive.org/web/2026/` to any dsplib URL — the Wayback
Machine redirects to the nearest snapshot:

```
https://web.archive.org/web/2026/https://ru.dsplib.org/content/<chapter>/<chapter>.html
```

Notes:
- The site was archived in full as of **May 2026**, shortly before it died —
  snapshots are complete and recent.
- Formulas on dsplib are **images** (`img/eq-*.png` next to each chapter), so
  text extraction gives prose only; the math has to be read from the rendered
  page (or re-derived — which we do anyway).
- If a guessed URL 404s, find the real one through the CDX index:
  `https://web.archive.org/cdx/search/cdx?url=ru.dsplib.org*&fl=original&collapse=urlkey&filter=original:.*<keyword>.*`
- The availability API (`archive.org/wayback/available?url=…`) works too but
  rate-limits aggressively; direct `/web/2026/` links are more reliable.
- **Cite via archive links, never copy the text into this public repo** — it
  is someone else's authored content. Archive links also never rot.

## Chapters we need, verified working

| Chapter | What we take from it | Archived link |
|---|---|---|
| Аналоговые, дискретные и цифровые сигналы | **the discrete-signal model** (measurement → averaging → Dirac comb), lattice function | [archived](https://web.archive.org/web/2026/https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html) |
| Теорема Котельникова | **the sampling theorem** for post 3: statement, proof via periodized spectrum, reconstruction | [archived](https://web.archive.org/web/2026/https://ru.dsplib.org/content/discrete_sampling_theorem/discrete_sampling_theorem.html) |
| Преобразование Фурье дельта-функции | delta-function properties used in the series-to-DFT derivation | [archived](https://web.archive.org/web/2026/https://ru.dsplib.org/content/fourier_transform_delta_func/fourier_transform_delta_func.html) |
| ДПФ (вывод из ряда Фурье) | cross-check of our post-1 derivation | [archived](https://web.archive.org/web/2026/https://ru.dsplib.org/content/dft/dft.html) |
| Ряд Фурье | reference for post 2 formula tables | [archived](https://web.archive.org/web/2026/https://ru.dsplib.org/content/fourier_series/fourier_series.html) |

(The first two are verified end-to-end — pages open with full text. The rest
follow the same pattern; verify on first use.)
