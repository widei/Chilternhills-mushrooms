# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page static marketing website for **Chiltern Hills Mushrooms**, a small-batch gourmet mushroom farm (brand concept: "a film-editor's mushroom farm" — moody-forest editorial luxury). There is no build step, framework, package manager, or test suite. It is hand-authored HTML/CSS/vanilla JS.

The live page is `Chiltern Hills Mushrooms.html` at the repo root — a single self-contained file (~1,600 lines) holding all markup, an inline `<style>` block, and one inline `<script>`.

## Running / developing

- **Preview:** open `Chiltern Hills Mushrooms.html` directly in a browser, or serve the root with any static server (e.g. `python -m http.server`) so relative `assets/` paths resolve.
- No build, lint, or test commands exist. Edits to the HTML file are the deliverable.
- Fonts load from Google Fonts (Fraunces / Manrope / JetBrains Mono); product/photo imagery is hot-linked from `img1.wsimg.com` (GoDaddy/Websites+Marketing CDN). Only `assets/logo.png` is local.

## Architecture & conventions

- **Single source of truth:** `Chiltern Hills Mushrooms.html` is the canonical page. `uploads/index-v3.html` and `OLD MOCKUP/index-v3.html` are older identical snapshots (the "v3" mockup) kept for reference — do **not** edit those when making site changes; they are not what ships.
- **Design tokens:** all color/typography/layout values are CSS custom properties in `:root` at the top of the `<style>` block. Change the palette there, not at call sites. Note the deliberately misleading token names — `--amber` is actually a dusty petrol teal, and there is no primary pigment (heritage muted palette on warm-oat `--bg`). Read the inline comments before assuming a token's color.
- **Page sections** are `<section>` elements identified by anchor id, navigated via the fixed `#nav`: `#story`, `#harvest`, `#apothecary`, `#forage`, `#order`, `#faq`.
- **JS is minimal and additive** (bottom `<script>`): nav background toggles `.scrolled` past 40px; elements with class `.reveal` animate in via an `IntersectionObserver` adding `.is-in`; the hero stage frames get a mousemove parallax (desktop ≥961px only). Preserve these class/id contracts when restructuring markup.
- **Aesthetic effects:** a film-grain SVG overlay (`.grain`) and ambient vignette (`.ambient`) are fixed full-screen layers — keep their `z-index` and `pointer-events: none` if you touch them.

When making visual changes, prefer editing tokens and existing component classes over introducing new parallel styles.
