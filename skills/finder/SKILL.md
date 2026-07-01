---
name: finder
description: PI Finder (v1). Use when the user wants to discover next-step research opportunities. The user must name a TARGET SCHOOL; deep-research PIs/labs at that school, run a verifier pass to confirm each PI is CURRENTLY at that school and active, then rank the survivors by fit against the user's STATE (experience, interests, beliefs) AND GOAL (direction). Output a ranked report to action/discovery/. Internships/industry roles and school-less discovery are Phase 2 — out of scope.
---

# Finder — PI Finder (v1)

Discover **Principal Investigators / labs** at a school the user names, ranked by genuine fit. This is the **explore** half of `action/` — reading `state` + `goal` to surface paths.

## Preconditions

- The user **must name a target school/institution**. If they haven't, ask for one before researching. (Open, school-less discovery is Phase 2.)

## Steps

1. **Read `state/` and `goal/`:** `state/identity.md`, `state/experience/` (+ `TIMELINE.md`), `state/interests.md`, `state/beliefs.md` (values + how they act on them), and **`goal/goals.md`**.
2. **Form a research profile:** skills, level (undergrad/MS/PhD-seeking), topical interests, **values/beliefs** (environment/style wanted), and **goal direction** (short/mid/long-term — e.g. academia vs industry).
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
6. **Write a report** to `action/discovery/<school>-<date>.md`.

## Report format

For each PI (most-fitting first):

```markdown
### <PI name> — <Lab name>
- **Link:** <lab / faculty page URL>
- **Area:** <research area>
- **Why it fits (topical):** ties to specific facts in state/experience or state/interests
- **Why it fits (beliefs):** ties to specific values in state/beliefs.md
- **Why it fits (goal):** how it serves goal/goals.md
- **Signal:** <recruiting note, recent relevant paper, etc.>
- **Verified:** currently at <school> as of <date> (basis: <faculty page / recent paper / …>)
```

End with a short **"gaps"** note: profile/goal areas with no strong match at this school, and anyone **excluded by the verifier** (moved/inactive/unconfirmed) so the user knows they were considered.

## Guardrails

- Never fabricate a PI, lab, or link — every entry must be a real, verifiable source.
- **Every listed PI must pass the verifier pass** (current + active). Unverified → dropped or explicitly flagged, never silently included.
- Ground every "why it fits" in specific `state`/`goal` facts; don't hand-wave.
- Read-only on `state/` and `goal/`. Write only to `action/` (git-ignored).
