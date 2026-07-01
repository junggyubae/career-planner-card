---
name: info-retrieval
description: Use to build and enrich the user's career STATE and GOALs. Two paths — (1) UPLOAD: the user provides a document (CV, SOP, transcript), save it to state/uploads/ and refine its facts into state/ (identity, experience, interests, beliefs) and goal/; (2) INTERVIEW: the user wants to say more about a topic (an experience, interests, beliefs, or goals), present a list of focused questions then iterate, and refine/enrich the target file. Beliefs (values + how you act on them) are the user's core identity — invest most there. Both paths only refine/enrich — never overwrite. Ask on any conflict.
---

# Info Retrieval

Grow the user's **state** (who they are) and **goal** (where they're going). This skill is the **only** writer of `state/` and `goal/`. It performs **refine and enrichment only** — it never destructively overwrites or deletes user-authored content.

> Data model: `state/` = who you are (past + present), `goal/` = where you're going. The card is the policy mapping `state + goal → action`.

## Choose a path

Ask (or infer): **upload a document**, or **explain more (interview)**?

## Path A — Upload → refine

1. **Save raw file** to `state/uploads/` (keep the original untouched).
2. **Extract facts** from the document.
3. **Detect conflicts** against existing state (e.g. a role with different dates/titles).
   - On any conflict: **STOP and ask the user** which is correct. Never auto-resolve.
4. **Route facts** to the right place (see table below). For each experience, write a file **with YAML frontmatter**.
5. **Regenerate** `state/TIMELINE.md` from the experience frontmatter (reverse-chronological), linking each entry title to its source file with a relative Markdown link such as `[Title](experience/YYYY-slug.md)`.
6. **Never invent** facts not present in the source.

> If the uploaded file is a CV/SOP **template** (`.tex`), leave it in `state/uploads/` for Alignment to use — don't extract it as experience.

## Path B — Interview → refine/enrich

1. **Pick a topic** with the user: a specific experience, their interests, **beliefs** (values + how they act on them — the richest topic), or **goals**.
2. **Generate the questions yourself, on the fly — there is no fixed question bank.** Compose a tailored **list** of focused questions for that topic, adapted to **what's already in `state`/`goal`**: probe the gaps, the *why* behind past choices, and concrete specifics; don't re-ask what's already recorded. For **beliefs** (the core identity), go deeper — values, the principles behind real decisions, trade-offs they'd defend, environments where they thrive vs. stall, and non-negotiables. Present the whole list at once (not one at a time).
3. Let the user **answer the subset they want** — unanswered questions don't block progress.
4. **Iterate** with follow-ups until the user signals they're done.
5. **Refine/enrich** the target file: add new detail *and* sharpen existing facts. Never overwrite prior content wholesale.
6. **Regenerate** `state/TIMELINE.md` if an experience changed, preserving source links for each entry.

## Where facts live

| Fact kind | Destination |
|-----------|-------------|
| name, contact, homepage, GitHub, LinkedIn, IDs, affiliation, current status | `state/identity.md` |
| an experience (research/work/project/education/award/…) | `state/experience/<YYYY-slug>.md` (with frontmatter) |
| research/career interests | `state/interests.md` |
| **values, beliefs, and how you act on them** (core identity) | `state/beliefs.md` |
| short / mid / long-term goals | `goal/goals.md` |
| raw uploaded document or user CV/SOP template | `state/uploads/` |
| *(derived)* time-ordered index of experience | `state/TIMELINE.md` — regenerate with links to source experience files, don't hand-edit |

## Experience frontmatter

```yaml
---
title: Honorary Member, SNU Tomorrow's Engineers Membership (STEM)
type: activity            # research | work | project | education | award | leadership | activity
start: 2024-09            # YYYY-MM
end: present              # YYYY-MM | present
org: SNU Tomorrow's Engineers Membership (STEM)
tags: [mentoring, teaching, outreach, research]
highlight: Mentored students through teaching, outreach, and research activities
---
Prose detail the user writes/answers freely…
```

## Guardrails

- Refine/enrich only — no destructive overwrite or deletion.
- Ask the user on any conflict.
- Never fabricate; store only what the user provided.
- Everything you write lives under `state/` or `goal/` (git-ignored, private).
