---
name: finder
description: PI Finder (v1). Use when the user wants to discover next-step research opportunities. The user must name a TARGET SCHOOL; deep-research PIs/labs at that school, run a verifier pass to confirm each PI is CURRENTLY at that school and active, then rank the survivors by fit against the user's STATE (experience, interests, beliefs) AND GOAL (direction). Output per-PI folders under action/discovery/<school-slug>-<pi-slug>/ and update the generated action/discovery/INDEX.md. Internships/industry roles and school-less discovery are Phase 2 — out of scope.
---

# Finder — PI Finder (v1)

Discover **Principal Investigators / labs** at a school the user names, ranked by genuine fit. This is the **explore** half of `action/` — reading `state` + `goal` to surface paths.

## Preconditions

- The user **must name a target school/institution**. If they haven't, ask for one before researching. (Open, school-less discovery is Phase 2.)

## Steps

1. **Read `state/` and `goal/`:** `state/identity.md`, `state/experience/` (+ `TIMELINE.md`), `state/interests.md`, `state/beliefs.md` (values + how they act on them), and **`goal/goals.md`**.
2. **Form a research profile:** skills, level (undergrad/MS/PhD-seeking), topical interests, **values/beliefs** (environment/style wanted), and **goal direction** (short/mid/long-term — e.g. academia vs industry). Also extract the user's known PI/mentor network from state: advisors, mentors, collaborators, current/past labs, institutions, and coauthors when present.
3. **Deep research the named school:** find PIs/labs whose work matches the profile. Prefer primary sources (lab pages, faculty directories, recent papers). Note recruiting signals when visible. Aim for **≥5 genuinely relevant** candidates; if the school truly has fewer, say so rather than padding.
4. **Verifier pass — confirm currency before including anyone.** For each candidate, run an **independent, skeptical second check** (treat it as a separate verifier: a name appearing in search ≠ current affiliation). Confirm from a primary source that the PI is:
   - **currently faculty at the named school** — not moved, emeritus, retired, deceased, or a visitor listed elsewhere;
   - **active** — evidence of work in roughly the last ~18 months (recent papers/news/lab updates);
   - **recruiting**, if the lab states it.
   Re-verify each lab **link** resolves. **Drop** anyone you cannot confirm is currently at the school; **flag** (don't silently keep) anyone whose status is uncertain. Consider dispatching a verifier subagent per candidate for parallel checks.
5. **Rank the verified survivors by fit** against all three:
   - **Topical fit** — interests + experience ↔ the lab's research.
   - **Belief/values fit** — from `state/beliefs.md` (mentorship style, lab culture, mission).
   - **Goal fit** — does this path serve the user's stated `goal/` trajectory?
6. **Research practical application context:**
   - **Lab and PI:** lab URL, PI title, department, relevant centers/programs.
   - **Alumni and outcomes:** where visible from public sources, note lab alumni
     roles, PhD/postdoc placements, industry/research destinations, startups, or
     faculty outcomes. Do not infer outcomes when not published.
   - **Fit band:** label each lab as `reach`, `target`, or `safe` relative to the
     user's current state evidence, and include a confidence note. This is a
     profile-fit/readiness estimate, not an admissions probability.
   - **Connection map:** look for evidence that the user's current/past PIs,
     mentors, schools, labs, collaborators, or coauthors connect to the target PI
     or lab. Use only verified evidence such as coauthorship, shared institutions,
     advisor lineage, lab alumni, conference/workshop ties, or explicit
     collaborations. If there is a plausible intro path, name the evidence and
     the person/institution that could support it; otherwise write `none found`.
7. **Write discovery files** directly under `action/discovery/`:
   - `INDEX.md` — generated cross-school overview of all researched PI/lab folders.
   - `<school-slug>-<pi-slug>/finder.md` — one per-PI/lab profile folder.
   - `<school-slug>-<pi-slug>/notes.md` — optional user notes/todos stub.

## Discovery folder format

Use this layout:

```text
action/discovery/
  INDEX.md
  <school-slug>-<pi-slug>/
    finder.md
    notes.md
```

Do not write school-level wrapper folders or old date-based reports such as
`action/discovery/<school-slug>/SYNTHESIS.md` or
`action/discovery/<school>-<date>.md`.

## `INDEX.md` format

Regenerate `action/discovery/INDEX.md` whenever Finder or Paper Briefing changes
discovery files. This is the user's and agent's first stop for what has already
been researched.

```markdown
# Discovery Index

## Summary

- **Schools researched:** <school list>
- **PI/lab folders:** <count>
- **Most promising next action:** <one concrete action>

## By School

### <School>

| Rank | PI / Lab | Folder | Fit Band | Briefing Status | Connection Signal | Fit Thesis |
|---|---|---|---|---|---|---|
| 1 | <PI> — <Lab> | `<school-slug>-<pi-slug>/` | target | finder only | possible intro via <person/source> | <one-sentence fit thesis> |

## Gaps And Exclusions

- <profile/goal areas with no strong match at this school>
- <excluded candidates and why: moved, inactive, unconfirmed, weak fit>
```

Briefing status should be one of: `finder only`, `dossier ready`, `briefed`.
Connection signal should be one of: `direct`, `strong`, `weak`, `none found`,
or `unknown`, followed by a short evidence note.

## Per-PI `finder.md` format

For each verified PI/lab, create:

```markdown
# <PI name> — <Lab name>

- **School:** <school>
- **PI title/department:** <title, department, relevant center/program>
- **Lab:** <lab name and URL>
- **Faculty page:** <faculty page URL>
- **Area:** <research area>
- **School rank:** #<rank> of <N>
- **Fit band:** reach | target | safe
- **Fit band rationale:** <why this is reach/target/safe relative to current state evidence; include confidence>
- **Why it fits (topical):** ties to specific facts in state/experience or state/interests
- **Why it fits (beliefs):** ties to specific values in state/beliefs.md
- **Why it fits (goal):** how it serves goal/goals.md
- **Signal:** <recruiting note, recent relevant paper, etc.>
- **Alumni/outcomes:** <publicly visible lab alumni paths, placements, roles, or "not found">
- **Connection map:** <direct/strong/weak/none found/unknown; evidence and possible intro path>
- **Verified:** currently at <school> as of <date> (basis: <faculty page / recent paper / …>)
```

Each per-PI folder is designed for Paper Briefing to add `dossier.md` and
`briefing.md` later.

## Guardrails

- Never fabricate a PI, lab, or link — every entry must be a real, verifiable source.
- **Every listed PI must pass the verifier pass** (current + active). Unverified → dropped or explicitly flagged, never silently included.
- Ground every "why it fits" in specific `state`/`goal` facts; don't hand-wave.
- Do not treat reach/target/safe as an admissions guarantee. It is a planning
  label based on visible fit and current evidence.
- Do not invent alumni outcomes or connection paths. If no public evidence is
  found, write `not found` or `none found`.
- Read-only on `state/` and `goal/`. Write only to `action/` (git-ignored).
