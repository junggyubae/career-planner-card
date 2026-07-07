---
name: career-compass
description: Use when the user wants a career trajectory review, roadmap, next-step recommendations, short-term/mid-term/long-term goals, gap analysis, readiness map, or advice on what they should do next based on their state, beliefs, interests, experiences, and goals. Read state/ goal/ and recent action/ outputs, then write a grounded Career Compass report to action/roadmap/. Do not grade the person; use a gentle map-style rubric.
---

# Career Compass

Produce a grounded career trajectory review: where the user's path currently
points, what goals make sense next, what gaps to fill, what to watch for, and
which next actions belong to the user vs. the agent.

## Opening

When starting, say:

```text
I'll run a Career Compass review.

I'll read your current state, beliefs, interests, experiences, and goals, then produce a roadmap with:

1. where your trajectory currently points
2. short-term, mid-term, and long-term goals
3. concrete next steps
4. gaps to fill
5. things to be careful about
6. what you should do yourself
7. what I can help with next

I'll keep this grounded in your existing files and won't invent facts.
```

## Step 1: Read State

Read these files if they exist:

- `state/identity.md`
- `state/interests.md`
- `state/beliefs.md`
- `state/TIMELINE.md`
- `state/experience/*.md`
- `goal/goals.md`
- recent `action/discovery/**/*.md`
- recent `action/applications/*/target.md`

If files are missing, note them as gaps instead of assuming.

## Step 2: Summarize Current Trajectory

Start with a concise diagnosis:

```text
Your current trajectory seems to be...
```

Use only grounded facts:

- current academic/professional stage
- recurring interests
- strongest experiences
- values/beliefs that shape fit
- stated goals
- patterns across past actions

## Step 3: Gentle Rubric

Assess these dimensions using: `emerging` / `forming` / `clear` / `strong`.

- Direction clarity
- Evidence strength
- Narrative coherence
- Opportunity fit
- Execution readiness

Also assess gap urgency as: `low` / `medium` / `high`.

For each rating, include 1-2 sentences explaining why. Do not make it feel like a
grade. Make it feel like a map.

## Step 4: Goals

Create or refine goals in three horizons:

### Short-term: 0-3 Months

Concrete actions the user can take soon.

### Mid-term: 3-12 Months

Positioning, skill-building, research/application preparation.

### Long-term: 1-3+ Years

Direction, identity, target environments, career thesis.

Each goal should include:

- goal
- why it fits the user's beliefs/state
- evidence from current state
- next action

## Step 5: Recommendations

Split recommendations into three groups.

### What You Should Do

Things only the user can do:

- reflect
- choose priorities
- reach out to people
- upload documents
- write raw thoughts
- make decisions
- practice telling their story

### What I Can Do Next

Agent tasks:

- interview the user
- find labs/PIs
- draft outreach emails
- tailor CV/SOP
- identify missing evidence
- compare target schools
- turn voice notes into state files

### Experiments

Low-cost ways to test direction:

- talk to one researcher
- read 2 papers from a target lab
- draft a 1-page research interest note
- apply to one low-risk opportunity
- do a small project to test interest

## Step 6: Gaps

List gaps clearly but gently.

For each gap, include:

- gap name
- why it matters
- evidence that it is missing or weak
- how to fill it
- whether it is urgent

Example categories:

- unclear short-term goal
- weak proof of research fit
- missing technical evidence
- interests too broad
- beliefs not yet concrete
- no outreach history
- target schools not selected
- application materials not ready

## Step 7: Awareness Notes

Add `Things To Be Aware Of`:

- risks of overfitting to one school/lab
- deadlines or timing issues
- missing prerequisites
- mismatch between stated values and target environment
- story gaps in CV/SOP
- uncertainty that needs exploration

## Step 8: Output File

Write the report to:

```text
action/roadmap/YYYY-MM-DD-career-compass.md
```

Then update the derived roadmap index `action/ROADMAP.md` with
reverse-chronological links to `action/roadmap/*.md`, brief titles, and the
highest-leverage next step from each report.

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

## Closing Message

After writing the roadmap, reply with:

```text
I created your Career Compass roadmap.

The highest-leverage next step is: <one concrete action>.

Good next prompts:
- Interview me to clarify my short-term goals.
- Find labs at MIT that fit this roadmap.
- Help me fill the biggest gap in my profile.
- Turn this roadmap into a 4-week action plan.
```
