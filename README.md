# Career Planner Card

A **Darwinian Mind Card** for planning your next academic / research career step. This repo is the **shareable card** — logic only, **no personal data**.

Manifest: [`card.json`](card.json) — `@junggyubae/career-planner-card`.

> ⚠️ **Cross-dependency — use only with the [`career-planner`](https://github.com/junggyubae/career-planner) project.**
> This card is **not standalone**. Its skills read and write a specific memory/output layout
> (`memory/basic-info/`, `memory/experience/_manager.md`, `output/_manager.md`, `output/<target>/…`)
> that lives in the `career-planner` project. Applied to any other project, the skills have nowhere
> to read or write. `career-planner` pins this card as a git submodule at `card/`; that is the
> supported way to consume it.

## Skills (three blocks)

| Skill | Purpose | Reads | Writes |
|-------|---------|-------|--------|
| [info-retrieval](skills/info-retrieval/SKILL.md) | Grow memory via **upload → refine** or **interview → refine/enrich**. Refine/enrich only; asks on conflict. | `uploads/`, all memory | all memory |
| [finder](skills/finder/SKILL.md) | **PI Finder** — name a school, deep-research PIs/labs there ranked by memory + belief fit. | all memory (incl. `beliefs/`) | `output/pi-finder/*.md` |
| [alignment](skills/alignment/SKILL.md) | Target URL → tailored **CV + SOP**, LaTeX → PDF (`pdflatex`). | all memory + template | `output/<target>/` + `output/_manager.md` |

Default LaTeX templates ship with the alignment skill at [`skills/alignment/templates/`](skills/alignment/templates/) (modern one-page academic CV + matching SOP), used when the user has no template of their own.

## Invariants (all skills)

1. **Refine/enrich only** — never destructively overwrite or delete user memory.
2. **Never fabricate** — every CV/SOP claim and PI rationale traces to memory; flag gaps, don't invent.
3. **Ask on conflict** — new input vs. existing memory → stop and ask.
4. **Privacy** — no personal data in this card; personal artifacts live in the consumer project's git-ignored `memory/` and `output/`.

## Use with `drwn`

```bash
# clone this git-backed card into your local drwn store
drwn card clone git+https://github.com/junggyubae/career-planner-card.git#v0.1.0
# then apply it to a project (see darwinian apply-mind-card)
```

Or consume it directly as a git submodule at `card/` in a career-planner project.
