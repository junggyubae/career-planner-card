---
name: paper-briefing
description: >-
  Use when the user wants to go deeper on PI/lab candidates than the initial
  Finder ranking: review paper abstracts for these labs, prioritize PIs, prep
  for interviews, or generate SOP talking points from abstract-level paper
  evidence. By default this is abstract-based; fetch/read full papers only when
  the user expressly asks for a paper summary or specific points inside a paper.
  Works only inside a career-planner repo with state/, goal/, and
  action/discovery/. Reads Finder outputs plus state/interests.md,
  state/beliefs.md, and goal/goals.md. Writes paper dossiers and briefings under
  per-PI discovery folders and updates action/discovery/INDEX.md.
---

# Paper Briefing

Deepen a Finder result by mapping the abstract-level intellectual terrain behind
candidate PIs/labs. Paper Briefing is the bridge between **Finder** and
**Alignment**: Finder says which labs look promising; Paper Briefing says which
papers look most relevant from abstracts, how the lab fits the user's identity
and goals, what to ask in interviews, and which points can later strengthen an
SOP.

## Discovery folder contract

Use the shared discovery layout:

```text
action/discovery/
  INDEX.md
  <school-slug>-<pi-slug>/
    finder.md
    dossier.md
    briefing.md
    notes.md
```

- Finder creates `INDEX.md` and one `<school-slug>-<pi-slug>/finder.md`
  folder per PI/lab directly under `action/discovery/`.
- Paper Briefing adds `dossier.md` and `briefing.md` under the same PI folder.
- Paper Briefing updates `INDEX.md` so users and agents can see all researched
  schools, PIs, labs, fit bands, statuses, alumni/outcomes, and connection
  signals in one place.
- Do not create old flat reports like `action/discovery/<school>-<date>.md`.

## Inputs

Read:

- `state/interests.md`
- `state/beliefs.md`
- `goal/goals.md`
- `action/discovery/INDEX.md`, if it exists
- the relevant per-PI `finder.md` files under
  `action/discovery/<school-slug>-<pi-slug>/`

If any input is missing, note the gap instead of inventing.

## Stage 1 — Dossier Collection

For each PI/lab in the school cohort:

1. Read the lab URL, faculty URL, affiliation, research area, and Finder fit
   rationale from `finder.md`.
2. Search for candidate papers relevant to the user's interests and goals.
   Prefer primary and durable sources:
   - lab publication pages
   - faculty publication pages
   - arXiv
   - PubMed
   - Semantic Scholar
   - publisher or conference pages
3. Collect 5-8 candidate papers with citation, link, year, abstract, source, and
   access status. Default to abstract and metadata only. Do not fetch or read
   the whole paper unless the user expressly requested a full-paper summary or
   specific details inside that paper.
4. Add or refine alumni/outcomes and connection evidence if paper/lab sources
   reveal new verified information.
5. Save the result to
   `action/discovery/<school-slug>-<pi-slug>/dossier.md`.

Use these access labels in `dossier.md`:

- `abstract_available` — abstract and metadata were available; this is the
  normal default.
- `abstract_unavailable` — title/citation exists, but no reliable abstract was
  found.
- `full_text_open_requested` — user explicitly requested full-paper reading and
  full text was available from an open source.
- `full_text_user_access_requested` — user explicitly requested full-paper
  reading and full text was read through the user's authorized browser/session
  access.
- `user_uploaded_pdf_requested` — user explicitly uploaded or provided the PDF
  for full-paper reading.
- `paywalled_or_unavailable` — full text was requested but not accessible.

Do not store full copyrighted PDFs in the repo by default. Store links,
citations, abstracts, notes, and access limitations. If the user explicitly
provides a PDF, keep it only in the user's private ignored workspace and cite it
as an uploaded source.

## Full-Paper Access On Explicit Request Only

Do not fetch or read a whole paper by default. Use abstracts for normal Paper
Briefing. Fetch/read full text only when the user expressly asks for one of
these:

- a summary of a specific paper
- specific methods/results/claims inside a paper
- a deeper comparison that requires reading beyond abstracts
- interview prep for a specific paper

When the user explicitly asks for full-paper reading, try access in this order:

1. **Open full text:** arXiv, PubMed Central, author/lab PDF, conference open
   access page, institutional repository, or publisher open-access page.
2. **User-provided file:** if the user uploads a PDF or document, read it as a
   private source and cite it in notes. Do not commit the raw file.
3. **Authorized browser access:** if the user has access through their browser,
   institution, library, publisher login, or VPN, ask them to open the paper in
   the browser or use an approved browser bridge/extension when available.
   Extract only text/metadata needed for notes and cite the URL/access path. Do
   not bypass paywalls, DRM, login controls, or access restrictions.
4. **Unavailable fallback:** if full text is unavailable, mark the paper
   `paywalled_or_unavailable`. Do not write a full-paper summary. You may still
   use the abstract-level notes, clearly labeled as such.

If the user explicitly requested full-paper reading and access limitations block
important papers, tell the user they can optionally use a browser extension or
browser bridge in the future, if available, to pass authorized paper
text/metadata into the agent session. This is optional, not required for default
Paper Briefing. Any such bridge must only use papers the user is authorized to
view and must not publish, redistribute, or commit copyrighted PDFs.

## Stage 2 — Abstract-Based Briefing And Identity Analysis

Batch by school when possible so cross-lab comparison is fair. With the flat
layout, use the school slug prefix to identify the cohort (for example,
`mit-*`). Read all available `dossier.md` files for that school, plus
`state/interests.md`, `state/beliefs.md`, and `goal/goals.md`.

For each PI/lab:

1. Select the top 3-5 papers that look most relevant from abstracts and metadata.
   Prefer a mix of recent work, methods-oriented papers, and landmark work when
   abstracts make that visible. Explain why each paper was selected.
2. Summarize each selected paper's likely topic, method direction, and
   contribution in 1-2 sentences based on the abstract. Label this as
   abstract-based.
3. Analyze fit against the user's interests, beliefs, and goals with concrete
   evidence from Finder output and paper abstracts.
4. Revisit the Finder fit band (`reach`, `target`, `safe`) based on
   abstract-level paper evidence. Keep the original label if the evidence still
   supports it; update it with a rationale if the abstract-based reading changes
   the picture.
5. Expand the connection map if papers reveal coauthors, collaborators,
   institutions, lab alumni, or advisor-lineage ties related to the user's known
   PIs/mentors.
6. Propose 2-3 interview questions grounded in the papers and lab direction.
7. Propose 1-2 SOP talking points that Alignment can reuse later.
8. Flag paper access limitations, abstract-only uncertainty, paywalls, or places
   where a full-paper read would be useful if the user wants to go deeper.
9. Save to `action/discovery/<school-slug>-<pi-slug>/briefing.md`.

Every `briefing.md` should open with:

```markdown
## Snapshot
- **Affiliation:** <department, rank/title, institution; joint program if relevant>
- **Lab:** <lab URL>
- **School rank:** **#X of N (Tier label)**
- **Fit band:** reach | target | safe
- **Alumni/outcomes:** <brief public outcome signal or not found>
- **Connection signal:** direct | strong | weak | none found | unknown
- **Evidence level:** abstract-based | full text requested/read
- **Fit thesis:** <one or two sentences on why this lab ranks where it does>
```

## Discovery Index

After per-PI briefings are written, update:

```text
action/discovery/INDEX.md
```

Include:

- schools researched and all PI/lab folders
- full-school ranking within each school cohort
- tier labels
- reach/target/safe fit bands with confidence notes
- lab alumni/outcome signals where public evidence exists
- connection signals between the user's known PIs/mentors/network and target PIs
- top papers the user should read first
- papers that may deserve a full-text read if the user wants more detail
- strongest fit themes across labs
- interview preparation priorities
- SOP angles worth saving for Alignment
- flags such as weak fit, narrow admissions path, inactive lab signals,
  adjunct/non-ladder status, or uncertain recruiting

The rank and fit band in each `briefing.md` must match the generated
`INDEX.md`, not a partial sub-batch.

## If Work Is Split Across Agents

Large schools may require parallel processing. In that case:

1. Each sub-batch writes abstract-based paper lists, fit analysis, interview
   questions, and SOP talking points, but uses provisional sub-batch standing
   only.
2. After all sub-batches finish, run one consolidation pass over every
   `briefing.md` for the relevant school or schools.
3. The consolidation pass writes final ranks and tier labels into each Snapshot
   and updates `INDEX.md`.

## Guardrails

- Do not fabricate papers, citations, methods, or lab claims.
- Prefer primary sources and stable scholarly sources over generic search
  snippets.
- Do not store full copyrighted PDFs by default; store links, citations, and
  access notes.
- Default to abstracts and metadata. Do not fetch/read full papers unless the
  user expressly asks for a paper summary or specific details inside a paper.
- Do not present abstract-based notes as full-paper summaries. Mark the evidence
  level clearly.
- Do not bypass paywalls, DRM, authentication, or institutional access controls.
  Browser-assisted reading is only for user-authorized access.
- Ground fit analysis in `state/interests.md`, `state/beliefs.md`, `goal/goals.md`,
  Finder output, abstracts/metadata, and any full-text notes the user explicitly
  requested.
- Do not overstate reach/target/safe. Treat it as a planning label based on
  visible fit, evidence strength, and current preparation, not an admission
  probability.
- Do not invent alumni outcomes or connection paths. If evidence is missing,
  state that it was not found.
- Keep Paper Briefing scoped to discovered career opportunities. For generic
  paper summarization unrelated to Finder/Application prep, use another workflow.
