# Changelog

All notable changes to the Career Planner Card. Versions are git tags (`vX.Y.Z`).

## v0.2.8
- **paper-briefing:** add a fifth skill for abstract-based PI/lab paper briefings between Finder and Alignment.
- **finder:** replace flat `action/discovery/<school>-<date>.md` reports with generated `action/discovery/INDEX.md` plus per-PI folders: `action/discovery/<school-slug>-<pi-slug>/`.
- **discovery:** add lab alumni/outcome notes, reach/target/safe fit bands, and connection mapping between the user's known PIs/mentors/network and target PIs.
- **paper access:** make abstracts the default evidence layer; full-paper fetching/reading is opt-in when the user explicitly requests a paper summary or specific internal details.
- **alignment:** reuse relevant discovery briefings for paper-grounded SOP talking points when available.
- **SOP:** add a narrative standard for vivid, professional SOPs that keep the reader moving paragraph to paragraph.

## v0.2.7
- **career-compass:** expand the skill instructions with the full step-by-step script, including opening language, detailed goal/recommendation/gap sections, awareness notes, output file instructions, and closing message.

## v0.2.6
- **career-compass:** add a fourth skill for grounded trajectory reviews, short-/mid-/long-term goals, next-step recommendations, gaps, awareness notes, and roadmap reports under `action/roadmap/`.

## v0.2.5
- **alignment:** prefer Tectonic for lightweight PDF compilation, fall back to `pdflatex`, and allow complete `.tex` drafts when no compiler is installed.
- **templates:** clarify that bundled LaTeX templates should compile with Tectonic or a vanilla `pdflatex` toolchain.

## v0.2.4
- **info-retrieval:** regenerated `state/TIMELINE.md` entries should link each title back to its source experience Markdown file.
- **docs:** replace identifying sample experience frontmatter with the STEM activity example and keep public skeleton docs non-personal.

## v0.2.3
- **alignment:** escape LaTeX specials + translate non-Latin scripts; compile loop that reads the `.log`, fixes, and retries until the PDF builds; enforce a strictly one-page CV by trimming/tightening and recompiling.
- **finder:** verifier pass confirming each PI is currently at the named school and active before ranking; excluded candidates surfaced in the gaps note.
- **info-retrieval:** interview questions are LLM-generated on the fly and adapted to existing state (no fixed bank); deeper probing for beliefs.

## v0.2.2
- Fix a stray "understanding" reference left in the finder skill description.

## v0.2.1
- Drop `understanding.md`; `beliefs.md` becomes the core-identity doc (values + how you act on them). All skills read beliefs as the identity/voice anchor.

## v0.2.0
- Restructure the data model from `memory/` + `output/` to **`state · goal · action`** (RL-shaped; the card is the policy `π(action | state, goal)`).
- Frontmatter on experience files; derived `state/TIMELINE.md` and `action/applications/BOARD.md` replace the hand-maintained `_manager.md` indexes.
- Applications become first-class bundles under `action/applications/<slug>/`.

## v0.1.1
- Fix default CV/SOP templates: underscore-free placeholders so the blank `.tex` compiles under `pdflatex`.

## v0.1.0
- Initial card: three skills (info-retrieval, finder, alignment) + default one-page academic CV/SOP LaTeX templates. Cross-dependent on the `career-planner` consumer project.
