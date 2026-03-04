# GH Pages Nav Fix, Certs & Patents Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Fix broken nav links, add two GCP certifications with Credly links, and add patent IDs to both README.md and LONG.md.

**Architecture:** Pure content edits across three files — no build step required. GitHub Pages re-deploys on push to main.

**Tech Stack:** Jekyll / GitHub Pages, Markdown, HTML

---

### Task 1: Fix `_layouts/default.html` nav and print button

**Files:**
- Modify: `_layouts/default.html`

**Step 1: Replace the nav links**

Current:
```html
    <a href="{{ '/' | relative_url }}">About</a>
    <a href="{{ '/MARTIN' | relative_url }}">Me</a>
    <a href="{{ '/BORING' | relative_url }}">Resume</a>
```

Replace with:
```html
    <a href="{{ '/' | relative_url }}">Short</a>
    <a href="{{ '/LONG' | relative_url }}">Long</a>
```

**Step 2: Fix the print button path check**

Current:
```js
    if (window.location.pathname.includes('BORING')) {
```

Replace with:
```js
    if (window.location.pathname.includes('LONG')) {
```

**Step 3: Verify the full file looks correct**

Read `_layouts/default.html` and confirm:
- Nav has exactly two links: `Short` → `/`, `Long` → `/LONG`
- Print button checks for `'LONG'`
- No references to `MARTIN` or `BORING` remain

**Step 4: Commit**

```bash
git add _layouts/default.html
git commit -m "fix: update nav to Short/Long, fix print button path for LONG"
```

---

### Task 2: Update `README.md` — Skills certifications + Patents

**Files:**
- Modify: `README.md`

**Step 1: Update the Certifications row in the Skills table**

Current:
```markdown
| **Certifications** | Google Cloud (Core Infrastructure, Terraform, Security, Networking, GKE) |
```

Replace with:
```markdown
| **Certifications** | Google Cloud (Core Infrastructure, Terraform, Security, Networking, GKE, [GenAI Leader](https://www.credly.com/badges/9911a7b6-0cac-4b2f-bd22-0d106191f4db/linked_in_profile), [Associate Cloud Engineer](https://www.credly.com/badges/b82ad90c-03c4-4b05-9729-2e2bac260fd3/linked_in_profile)) · [All credentials ↗](https://www.credly.com/users/martin-yankov.d8a8ae03/badges#credly) · [Skills ↗](https://www.credly.com/users/martin-yankov.d8a8ae03/skills) |
```

**Step 2: Update the Patents section**

Current:
```markdown
## Patents

- Modular system for preparatory repairs of buildings (BG, 2020)
- Construction process management and control system (BG, 2020)
```

Replace with:
```markdown
## Patents

- **BG 3721 U1** · Jun 29, 2020 — Modular system for preparatory repairs of buildings
- **BG 3640 U1** · Jun 1, 2020 — Construction process management and control system
```

**Step 3: Commit**

```bash
git add README.md
git commit -m "feat: add GCP GenAI Leader + ACE certs with Credly links, add patent IDs"
```

---

### Task 3: Update `LONG.md` — Certifications + Patents

**Files:**
- Modify: `LONG.md`

**Step 1: Prepend new certs to the Certifications section**

Current top of Certifications:
```markdown
## Certifications

- Google Cloud Fundamentals: Core Infrastructure
```

Replace with:
```markdown
## Certifications

- [Google Cloud Certified Generative AI Leader](https://www.credly.com/badges/9911a7b6-0cac-4b2f-bd22-0d106191f4db/linked_in_profile)
- [Google Cloud Certified Associate Cloud Engineer](https://www.credly.com/badges/b82ad90c-03c4-4b05-9729-2e2bac260fd3/linked_in_profile)
- Google Cloud Fundamentals: Core Infrastructure
```

**Step 2: Add Credly profile links after the last certification entry**

Current last cert entry + following line:
```markdown
- Complete React Developer (2020)

---
```

Replace with:
```markdown
- Complete React Developer (2020)

[All credentials ↗](https://www.credly.com/users/martin-yankov.d8a8ae03/badges#credly) · [Skills ↗](https://www.credly.com/users/martin-yankov.d8a8ae03/skills)

---
```

**Step 3: Update the Patents section**

Current:
```markdown
## Patents

- Modular system for preparatory repairs of buildings (Bulgaria, 2020)
- Construction process management and control system (Bulgaria, 2020)
```

Replace with:
```markdown
## Patents

- **BG 3721 U1** · Jun 29, 2020 — Modular system for preparatory repairs of buildings
- **BG 3640 U1** · Jun 1, 2020 — Construction process management and control system
```

**Step 4: Commit**

```bash
git add LONG.md
git commit -m "feat: add GCP certs with Credly links, patent IDs to LONG.md"
```

---

### Task 4: Verify and push

**Step 1: Check no broken references remain**

```bash
grep -r "BORING\|MARTIN" _layouts/ README.md LONG.md
```

Expected: no output.

**Step 2: Check markdown lint passes**

```bash
npx markdownlint-cli2 README.md LONG.md
```

Expected: no errors (or note any pre-existing warnings to ignore).

**Step 3: Push to main**

```bash
git push origin main
```

Expected: CI passes, GitHub Pages redeploys. Verify at `https://lutherwaves.github.io/README/`.
