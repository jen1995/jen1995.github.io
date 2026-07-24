# Cohomology Zero

Blog about machine learning and mathematics, built with [Hugo](https://gohugo.io/) + [PaperMod](https://github.com/adityatelange/hugo-PaperMod), deployed to GitHub Pages.

Live at: https://jen1995.github.io/

## Repository layout

- `content/posts/` — published posts (each post is a folder: `index.md` + its images)
- `drafts/` — shared scratch space for work-in-progress; never published (see `drafts/README.md`)
- `notebooks/` — hands-on notebooks referenced from posts

## Local development

Hugo is installed at `~/.local/bin/hugo` (v0.164.0 extended).

```bash
# live-preview at http://localhost:1313/
~/.local/bin/hugo server -D

# production build into public/
~/.local/bin/hugo --gc --minify
```

## Writing a post

Each post is a *page bundle* — a folder with `index.md` and its images next to it:

```bash
~/.local/bin/hugo new content posts/my-post-name/index.md
```

```
content/posts/my-post-name/
├── index.md
└── figure1.png        # referenced as ![caption](figure1.png)
```

Front matter (see `archetypes/posts.md`):

```yaml
---
title: "Post title"
date: 2026-07-21
draft: false          # drafts are only visible with `hugo server -D`
tags: ["transformers"]
summary: "One-two sentences shown in the post list."
math: true
---
```

## Math

Math is rendered client-side by KaTeX (configured in `layouts/partials/extend_head.html`; the passthrough config in `hugo.toml` keeps Markdown from mangling TeX).

- Inline: `$s_k = f(s_{k-1}, x_k)$`
- Display: `$$ ... $$` — supports `\tag{1}`, `\begin{aligned}...\end{aligned}` inside
- Prefer `$$ ... $$` over bare `\begin{equation}` blocks — it is what the passthrough extension protects
- Handy macros defined globally: `\R`, `\E`, `\KL`

Tables, `> 💡` callout quotes, `<details>` blocks and code fences all work — see the *Math rendering test* post, and delete it once real posts are up.

## Migrating source posts

When translating posts from `transformer_blog` / `ml-handbook`:

1. Create a page bundle and copy the post's images into it; change image paths to bare filenames.
2. `{:toc}` (kramdown) is not needed — PaperMod generates a TOC from headings.
3. Replace `\|` inside math with `\mid` (the `\|` escaping was a Jekyll/kramdown workaround).
4. `\begin{equation} ... \end{equation} \tag{1}` → `$$ ... \tag{1} $$`.

## Deployment

Pushes to `main` trigger `.github/workflows/deploy.yml`, which builds the site and publishes it to GitHub Pages.

Pages is already configured (**Settings → Pages → Source: GitHub Actions**); nothing to set up.

The PaperMod theme is a git submodule — clone with `git clone --recurse-submodules`, update with `git submodule update --remote --merge`.
