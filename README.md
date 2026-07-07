# Career Planner Card

A **Darwinian Mind Card** for planning your next academic / research career step. This repo is the **shareable card** — logic only, **no personal data**.

Manifest: [`card.json`](card.json) — `@junggyubae/career-planner-card`.

## Data model — `state · goal · action` (RL-shaped)

The card is the **policy** `π(action | state, goal)`:

- **`state/`** — who you are (past + present): identity, experience, interests, and **beliefs** (values + how you act on them — the irreducibly human core the card leans on hardest).
- **`goal/`** — where you're going: short / mid / long-term goals.
- **`action/`** — what you do about it: `roadmap/` (Career Compass = orient), `discovery/` (Finder + Paper Briefing = explore/deepen), and `applications/` (Alignment = exploit).

> ⚠️ **Cross-dependency — use only with the [`career-planner`](https://github.com/junggyubae/career-planner) project.**
> This card is **not standalone**. Its skills read/write the `state/ goal/ action/` layout that lives in the
> `career-planner` project. Applied to any other project, the skills have nowhere to read or write.
> `career-planner` pins this card as a git submodule at `card/`; that is the supported way to consume it.

## Skills (five blocks)

| Skill | Purpose | Reads | Writes |
|-------|---------|-------|--------|
| [info-retrieval](skills/info-retrieval/SKILL.md) | Grow **state + goal** via **upload → refine** or **interview → refine/enrich**. Refine/enrich only; asks on conflict. | `state/uploads/`, `state/`, `goal/` | `state/`, `goal/` (incl. derived `state/TIMELINE.md`) |
| [career-compass](skills/career-compass/SKILL.md) | Trajectory review — short-/mid-/long-term goals, readiness map, next steps, gaps, and awareness notes. | `state/`, `goal/`, recent `action/` | `action/roadmap/*.md` + derived `ROADMAP.md` |
| [finder](skills/finder/SKILL.md) | **PI Finder** — name a school, deep-research PIs/labs there ranked by topical + belief + **goal** fit. | `state/`, `goal/` | `action/discovery/INDEX.md` + `action/discovery/<school-slug>-<pi-slug>/` |
| [paper-briefing](skills/paper-briefing/SKILL.md) | Deepen Finder candidates through abstract-based paper dossiers, briefings, interview questions, SOP talking points, fit bands, alumni outcomes, and connection signals. Full-paper reading is opt-in. | `state/`, `goal/`, `action/discovery/` | `action/discovery/INDEX.md` + `action/discovery/<school-slug>-<pi-slug>/` |
| [alignment](skills/alignment/SKILL.md) | Target URL → tailored **CV + SOP**, LaTeX → PDF when available (`tectonic` preferred, `pdflatex` fallback). | `state/`, `goal/`, discovery briefings + template | `action/applications/<slug>/` + derived `BOARD.md` |

Default LaTeX templates ship with the alignment skill at [`skills/alignment/templates/`](skills/alignment/templates/) (modern one-page academic CV + matching SOP), used when the user has no template of their own. PDF compilation is optional for first-run onboarding; Tectonic is the preferred light compiler, and `pdflatex` remains a fallback.

## Invariants (all skills)

1. **Refine/enrich only** — never destructively overwrite or delete user `state`/`goal`.
2. **Never fabricate** — every CV/SOP claim and PI rationale traces to `state`; flag gaps, don't invent.
3. **Ask on conflict** — new input vs. existing `state` → stop and ask.
4. **Privacy** — no personal data in this card; personal artifacts live in the consumer project's git-ignored `state/`, `goal/`, `action/`.

## Use with `drwn`

```bash
# clone this git-backed card into your local drwn store
drwn card clone git+https://github.com/junggyubae/career-planner-card.git#v0.2.8
# then apply it to a project (see darwinian apply-mind-card)
```

Or consume it directly as a git submodule at `card/` in a career-planner project.
