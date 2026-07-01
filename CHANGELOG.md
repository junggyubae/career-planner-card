# Changelog

All notable changes to the Career Planner Card. Versions are git tags (`vX.Y.Z`).

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
