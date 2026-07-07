---
name: alignment
description: >-
  Use when the user provides a target URL (a lab, internship, or job) and wants
  tailored application materials. Resolve a template (the user's own from
  state/uploads/ or the bundled default), analyze the target, match it against
  state + goal, and generate a tailored CV and SOP grounded strictly in state.
  Render as LaTeX and compile to PDF with the lightest available compiler:
  tectonic first, then pdflatex; if neither is installed, leave complete .tex
  drafts and explain how to install Tectonic. The CV must be strictly one page
  when a compiler is available. Beliefs shape SOP voice and fit; goals shape
  the trajectory. The SOP should be fun, vivid, and exciting to read while
  staying professional, and each paragraph should make the reader want to know
  more and continue to the next paragraph. Write an application bundle to
  action/applications/. Never fabricate.
---

# Alignment — tailored CV + SOP from a target URL

Given a **target URL**, produce a CV and SOP tailored to it, grounded strictly in the user's `state`, delivered as **`.tex` plus `.pdf` when a lightweight PDF compiler is available**. This is the **exploit** half of `action/` — committing to a specific target.

## Steps

1. **Resolve the template.** Ask the user: use **your own template** or the **default**?
   - If `state/uploads/` contains a user template (e.g. `cv-template.tex`, `sop-template.tex`), use it.
   - Otherwise use the bundled defaults shipped **alongside this skill** at `templates/cv-template.tex` and `templates/sop-template.tex` (modern one-page academic CV). In an applied project this resolves to `card/skills/alignment/templates/`.
2. **Fetch & analyze the target** at the URL: extract requirements, focus areas, keywords, and what the target values. If the page is unreachable, ask the user to paste the content.
3. **Read `state/` and `goal/`:** `state/identity.md`, `state/experience/`, `state/interests.md`, `state/beliefs.md` (values + how they act on them — the core of the SOP's voice), and `goal/goals.md`.
4. **Read relevant discovery context when available:** if the target matches a PI/lab already explored under `action/discovery/**/finder.md` or `action/discovery/**/briefing.md`, use those files for target-specific fit, paper-grounded interview/SOP talking points, and current lab context.
5. **Match state ↔ target:** select the most relevant experience and framing. Use **`state/beliefs.md`** to argue genuine fit and set the SOP's voice; use **`goal/goals.md`** for the trajectory ("why this, why now, where it leads").
6. **Render `.tex`:**
   - **CV** — fill the template's placeholders from `state` (header from `identity.md`, entries from `experience/`).
   - **SOP** — narrative in the user's voice, arguing fit to this specific target, grounded in real experience + beliefs + goals. Make it interesting enough that a reader wants to know the user's story more after every paragraph.
   - **LaTeX safety (both files):** escape the special characters `& % $ # _ { } ~ ^ \`; render symbols via math mode / packages (`∩`→`$\cap$`, `×`→`$\times$`, `→`→`$\to$`, `≤`→`$\le$`; en-dash `–` is fine). **`pdflatex` cannot render non-Latin scripts** — romanize or translate any Korean / Chinese / etc. into English; never leave raw CJK in the `.tex`.
7. **Create the application bundle** `action/applications/<target-slug>/` and write:
   - `target.md` — the analyzed target **with frontmatter** (see below) + requirements/keywords/coverage note.
   - `cv.tex`, `sop.tex` — the tailored materials.
   - `notes.md` — a stub for the user's own notes/emails/todos.
8. **Compile when a compiler is available.** Prefer Tectonic because it is much lighter than a full TeX Live/MacTeX install. For both `cv.tex` and `sop.tex`, choose the first available compiler:
   1. `tectonic`
   2. `pdflatex`
   3. no compiler — leave complete `.tex` drafts and tell the user how to install Tectonic later

   Tectonic command:
   ```
   tectonic --keep-logs --outdir action/applications/<target-slug> action/applications/<target-slug>/cv.tex
   ```

   pdflatex fallback:
   ```
   pdflatex -interaction=nonstopmode -output-directory action/applications/<target-slug> action/applications/<target-slug>/cv.tex
   ```

   **If a compile fails, read the `.log`, find the offending line (almost always an unescaped char or an unsupported symbol/glyph), fix the `.tex`, and recompile with the same compiler. Loop until both `cv.pdf` and `sop.pdf` exist.** A run that ends without a built PDF is acceptable only when neither `tectonic` nor `pdflatex` is installed; in that case, emit the `.tex` files, note that PDFs were skipped, and recommend installing Tectonic rather than full TeX Live.
9. **Enforce a strict one-page CV when a compiler is available.** After the CV compiles, check its page count. If it is **more than one page**, tighten and recompile — iterate until it is exactly **one page**:
   1. first cut the **least-relevant** entries/bullets for *this* target;
   2. then **shorten wording** — concise phrasing, drop filler, compress descriptions;
   3. do **not** shrink the template's font size or margins to fake it.
   (The SOP has no page cap unless the target specifies one — honor a stated limit the same way.)
10. **Regenerate** `action/applications/BOARD.md` from all `target.md` frontmatter, grouped by `status`.
11. **Coverage note:** in `target.md`, list any target requirement not backed by `state` (flag the gap — do **not** invent to fill it).

## SOP narrative standard

The SOP is not a formal inventory of achievements. It is a grounded story of
curiosity, preparation, fit, and direction. It should be fun and exciting to
read in a professional way: specific, alive, intellectually sincere, and paced
so the reader wants to know what happens in the next paragraph.

- **Use a reader-momentum test.** After each paragraph, ask: "Would a busy
  reader want to keep reading because something specific, human, or intellectually
  interesting is unfolding?" If not, revise the paragraph before moving on.
- **Open with a real hook, not generic passion.** Start from a concrete
  question, tension, observation, problem, or turning point grounded in `state/`.
  Avoid "I have always been passionate about..." unless the state files contain a
  very specific reason that makes it fresh.
- **Make experience causal.** Do not list experiences chronologically. Show how
  one experience changed the user's questions, skills, taste, or direction, then
  use that change to motivate the next paragraph.
- **Make target fit feel like a conversation.** Tie the user's interests and
  beliefs to the target's actual work, methods, values, or environment. The fit
  should feel discovered from evidence, not pasted from the website.
- **Keep the user's voice alive.** Use concrete nouns, active verbs, and a few
  precise details from `state/experience/` and `state/beliefs.md`. Vary sentence
  length. Cut bureaucratic phrases that could belong to anyone.
- **Stay professional, not gimmicky.** "Fun" means engaging and memorable, not
  cute, exaggerated, jokey, or theatrical. Never add drama that is not supported
  by state.
- **End with forward motion.** The final paragraph should make the trajectory
  feel inevitable: why this target, why now, and what the user is ready to build,
  study, or contribute next.

Before finalizing `sop.tex`, do a revision pass:

1. Remove any sentence that could be copied into another applicant's SOP without
   changing facts.
2. Replace abstract claims with state-backed details.
3. Check that every paragraph either advances the story, sharpens fit, or raises
   the stakes for the next paragraph.
4. Confirm every claim still traces to `state/`, `goal/`, or the target page.

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
- Keep templates compiling on Tectonic and a vanilla `pdflatex` toolchain — avoid exotic packages.
- **The preferred deliverable is a built PDF plus `.tex`.** Never hand back a `.tex` that failed to compile when `tectonic` or `pdflatex` is available — iterate until it builds. If no compiler is installed, the `.tex` draft is a valid onboarding-friendly deliverable and the user can install Tectonic later. The CV is **strictly one page** when a compiler is available.
