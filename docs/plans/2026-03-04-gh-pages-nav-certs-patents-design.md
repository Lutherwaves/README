# Design: GH Pages Nav Fix, Certs & Patents Update

**Date:** 2026-03-04

## Problem

The site at `lutherwaves.github.io/README/` has several staleness issues:

1. **Nav links are broken** — `_layouts/default.html` references `/MARTIN` (deleted) and `/BORING` (renamed to `/LONG`). The print-button script also still checks for `'BORING'`.
2. **Skills/Certifications are outdated** — Missing Google Cloud Certified Generative AI Leader and Associate Cloud Engineer.
3. **Patents lack identifiers** — BG patent numbers and issue dates are absent from both `README.md` and `LONG.md`.
4. **No Credly profile link** — Should surface skills and all credentials.

## Changes

### `_layouts/default.html`

- Nav: replace 3-item (`About` / `Me` / `Resume`) with 2-item (`Short` → `/`, `Long` → `/LONG`)
- Print button JS: change `'BORING'` check to `'LONG'`

### `README.md`

- **Skills table** — Certifications row: append `GenAI Leader` and `Associate Cloud Engineer` badge links, add Credly skills/badges link
- **Patents section** — Add BG numbers and issue dates

### `LONG.md`

- **Certifications section** — Add at top:
  - Google Cloud Certified Generative AI Leader (Credly badge link)
  - Google Cloud Certified Associate Cloud Engineer (Credly badge link)
  - All credentials + skills on Credly link
- **Patents section** — Add BG numbers, issue dates, and descriptions

## Badge / Profile URLs

| Cert | Credly URL |
|------|-----------|
| Generative AI Leader | `https://www.credly.com/badges/9911a7b6-0cac-4b2f-bd22-0d106191f4db/linked_in_profile` |
| Associate Cloud Engineer | `https://www.credly.com/badges/b82ad90c-03c4-4b05-9729-2e2bac260fd3/linked_in_profile` |
| All badges | `https://www.credly.com/users/martin-yankov.d8a8ae03/badges#credly` |
| Skills | `https://www.credly.com/users/martin-yankov.d8a8ae03/skills` |
