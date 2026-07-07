---
name: career-compass
description: Use when the user wants a career trajectory review, roadmap, next-step recommendations, short-term/mid-term/long-term goals, gap analysis, readiness map, or advice on what they should do next based on their state, beliefs, interests, experiences, and goals. Read state/ goal/ and recent action/ outputs, then write a grounded Career Compass report to action/roadmap/. Do not grade the person; use a gentle map-style rubric.
---

# Career Compass

Produce a grounded career trajectory review: where the user's path currently
points, what goals make sense next, what gaps to fill, what to watch for, and
which next actions belong to the user vs. the agent.

## Inputs

Read what exists; if a file is missing, record it as a gap instead of assuming.

- `state/identity.md`
- `state/interests.md`
- `state/beliefs.md`
- `state/TIMELINE.md`
- `state/experience/*.md`
- `goal/goals.md`
- recent `action/discovery/*.md`
- recent `action/applications/*/target.md`

## Workflow

1. **Summarize the current trajectory.** Start with: "Your current trajectory seems to be..." Ground this in stage, recurring interests, strongest evidence, beliefs/values, stated goals, and recent actions.
2. **Create a gentle readiness map.** Use these stages, not numbers: `emerging`, `forming`, `clear`, `strong`. Assess:
   - Direction clarity
   - Evidence strength
   - Narrative coherence
   - Opportunity fit
   - Execution readiness
   - Gap urgency (`low`, `medium`, `high`)
   For each dimension, explain the rating in 1-2 grounded sentences. Make it feel like a map, not a grade.
3. **Create or refine goals across three horizons.**
   - Short-term: `0-3 months`
   - Mid-term: `3-12 months`
   - Long-term: `1-3+ years`
   Each goal must include: the goal, why it fits the user's beliefs/state, evidence from current state, and the next action.
4. **Split recommendations.**
   - `What You Should Do`: reflection, choices, outreach, uploading documents, raw thinking, decisions, practice telling the story.
   - `What I Can Do Next`: interviews, lab/PI discovery, outreach drafts, CV/SOP tailoring, gap analysis, school comparison, turning voice notes into state.
   - `Suggested Experiments`: low-cost tests of direction before committing.
5. **List gaps gently and concretely.** For each gap, include: gap name, why it matters, evidence that it is missing or weak, how to fill it, and urgency.
6. **Add awareness notes.** Include risks, timing/deadlines, missing prerequisites, mismatch between values and target environments, story gaps, and uncertainty worth exploring.
7. **Write the report** to `action/roadmap/YYYY-MM-DD-career-compass.md`.
8. **Update the derived roadmap index** `action/ROADMAP.md` with reverse-chronological links to `action/roadmap/*.md`, brief titles, and the highest-leverage next step from each report.

## Report Format

```markdown
# Career Compass — YYYY-MM-DD

## Summary

## Current Trajectory

## Readiness Map

| Dimension | Stage | Why |
|---|---|---|

## Short-Term Goals: 0-3 Months

## Mid-Term Goals: 3-12 Months

## Long-Term Direction: 1-3+ Years

## Recommended Next Steps

## What You Should Do

## What I Can Do Next

## Suggested Experiments

## Gaps To Fill

## Things To Be Aware Of

## Suggested Next Prompt
```

## Guardrails

- Ground every claim in `state/`, `goal/`, or existing `action/` artifacts. If evidence is missing, say so as a gap.
- Do not invent achievements, goals, interests, deadlines, preferences, or target constraints.
- Do not make medical, legal, immigration, or financial claims.
- Do not frame the user as failing. Prefer "emerging/forming/clear/strong" and "gap urgency" over scores.
- Read-only on `state/` and `goal/`. Write only to `action/roadmap/` and derived `action/ROADMAP.md`.
