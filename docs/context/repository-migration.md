# Repository cleanup and migration

The user requested a structure containing the correct blogging work and removal of obsolete material.

## What was preserved

All seven original blogging artifacts were moved without changing their contents:

- Chat PDF to `docs/context/sources/blogging-claude-chat.pdf`.
- Mid-semester PPTX and team DOCX to `docs/presentation/midsem/`.
- Chen SVG/PNG to `diagrams/chen-er.*`.
- Schema SVG/PNG to `diagrams/relational-schema.*`.

Searchable slide/team-guide extracts moved beside the presentation files. The chat extract, source review, source hashes, baseline, current decisions, manual checklist and offline guide remain available. The manifest records original and current paths plus SHA-256 values.

## What was removed

The unrelated inventory report, PDF, diagrams, chat export/text and inventory handoff were removed from the working tree. Their committed versions remain recoverable in Git history, including commit `93d9ec8` under their earlier `docs/report/`, `diagrams/` and `docs/context/` paths.

The superseded nine-table proposal and redundant `docs/design/proposed-model.md` pointer were removed. The earlier proposal is recoverable from `93d9ec8:docs/design/proposed-model.md`; the active 14-table design is [baseline.md](../design/baseline.md). The supplied folder `Right Contxt Files` and old report directory were removed only after becoming empty.

No Git history was rewritten. No current blogging source was discarded. The source review/change log retain important context corrections and technical questions without keeping competing active plans.

## New implementation structure

`database/`, `server/`, `client/` and `agents/` contain useful implementation guides describing responsibilities, planned files and verification gates. They do not contain executable application code or empty placeholder scripts. Diagrams/presentation indexes explain the actual artifacts.

The next coding deliverable remains MySQL schema/seed/views, followed by the API, human frontend, scripted agent and verified operations. See the [handoff](handoff.md).
