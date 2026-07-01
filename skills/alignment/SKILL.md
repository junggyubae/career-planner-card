---
name: alignment
description: Use when the user provides a target URL (a lab, internship, or job) and wants tailored application materials. Resolve a template (the user's own from state/uploads/ or the bundled default), analyze the target, match it against state + goal, and generate a tailored CV and SOP grounded strictly in state. Render as LaTeX and compile to PDF with pdflatex. Beliefs shape SOP voice and fit; goals shape the trajectory. Write an application bundle to action/applications/. Never fabricate.
---

# Alignment — tailored CV + SOP from a target URL

Given a **target URL**, produce a CV and SOP tailored to it, grounded strictly in the user's `state`, delivered as **`.tex` compiled to `.pdf`**. This is the **exploit** half of `action/` — committing to a specific target.

## Steps

1. **Resolve the template.** Ask the user: use **your own template** or the **default**?
   - If `state/uploads/` contains a user template (e.g. `cv-template.tex`, `sop-template.tex`), use it.
   - Otherwise use the bundled defaults shipped **alongside this skill** at `templates/cv-template.tex` and `templates/sop-template.tex` (modern one-page academic CV). In an applied project this resolves to `card/skills/alignment/templates/`.
2. **Fetch & analyze the target** at the URL: extract requirements, focus areas, keywords, and what the target values. If the page is unreachable, ask the user to paste the content.
3. **Read `state/` and `goal/`:** `state/identity.md`, `state/experience/`, `state/interests.md`, `state/beliefs.md`, `state/understanding.md`, and `goal/goals.md`.
4. **Match state ↔ target:** select the most relevant experience and framing. Use **`state/beliefs.md`** to argue genuine fit and set the SOP's voice; use **`goal/goals.md`** for the trajectory ("why this, why now, where it leads").
5. **Render `.tex`:**
   - **CV** — fill the template's placeholders from `state` (header from `identity.md`, entries from `experience/`).
   - **SOP** — narrative in the user's voice, arguing fit to this specific target, grounded in real experience + beliefs + goals.
6. **Create the application bundle** `action/applications/<target-slug>/` and write:
   - `target.md` — the analyzed target **with frontmatter** (see below) + requirements/keywords/coverage note.
   - `cv.tex`, `sop.tex` — the tailored materials.
   - `notes.md` — a stub for the user's own notes/emails/todos.
7. **Compile to PDF** with `pdflatex` (into the same folder):
   ```
   pdflatex -interaction=nonstopmode -output-directory action/applications/<target-slug> action/applications/<target-slug>/cv.tex
   ```
   producing `cv.pdf` and `sop.pdf`. If `pdflatex` is unavailable, still emit the `.tex` and tell the user how to install/compile.
8. **Regenerate** `action/applications/BOARD.md` from all `target.md` frontmatter, grouped by `status`.
9. **Coverage note:** in `target.md`, list any target requirement not backed by `state` (flag the gap — do **not** invent to fill it).

## Target frontmatter

```yaml
---
target: Prof. Surya Ganguli — Neural Dynamics & Computation Lab
kind: phd                 # phd | internship | job | fellowship
school: Stanford
deadline:                 # YYYY-MM-DD if known
status: drafting          # researching | drafting | submitted | interview | offer | reject | withdrawn
url: https://…
---
```

## Guardrails

- **100% of claims must trace to `state`.** Never fabricate experience, skills, or dates.
- Beliefs inform SOP voice **and** the fit argument; goals inform the trajectory — not just a list of experience.
- Read-only on `state/` and `goal/`. Write only to `action/` (git-ignored).
- Keep templates compiling on a vanilla `pdflatex` toolchain — avoid exotic packages.
