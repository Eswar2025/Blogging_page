# Current project handoff

## Confirmed context

The project is **Database Management System for a Blogging Site for AI agents and Humans**. Read [the source review](blogging-source-review.md) and [recovered baseline](../design/baseline.md) first. The original 33-page chat PDF is under `docs/context/sources/`; the 20-slide deck, team guide and their text extracts are under `docs/presentation/midsem/`; both Chen/schema SVG+PNG pairs are under `diagrams/`. All seven original artifacts retain their content, with original/current paths and SHA-256 values in the manifest. The former supplied folder was removed after becoming empty.

The active model is **14 lowercase tables**: actor, human_user, ai_agent, api_key, post, post_revision, revision_source, tag, post_tag, comment, post_vote, comment_vote, edit_proposal, audit_log. The Chen conceptual model has 11 entity sets and two weak entities. The table diagram is a separate logical schema. Inventory material and the nine-table proposal were removed from the working tree; [the migration note](repository-migration.md) records recoverable history.

## Essential product correction

Humans use the website/session. Agents are API clients with their own scoped API keys and an accountable human owner. Both authenticate to actor_id. The standard human editor publishes as its logged-in human; agents publish from their own client credentials. The old author-selector/owner-impersonation assumption is removed.

Agents submit edit proposals against a base revision. An authorized human approves/rejects them; valid approval appends a revision with proposer/editor identity, review attribution, and audit history. Preserve citations, provenance, votes, keys/scopes and append-only history. Derive current revision/scores through queries/views. No flag/follow/scope-join/session/rate-limit-window core tables or dedicated moderation queue.

## User preferences and course constraints

- MySQL/InnoDB only; raw readable parameterized SQL through mysql2/promise; Node/Express TypeScript; React TSX + Tailwind; Vite suggested. Source materials recommend MySQL 8.4; installed versions still need checking. The user's latest TSX preference supersedes the old vanilla/no-TypeScript recommendation.
- Use the project for course evaluation and resume learning with enough depth to explain each choice. User works largely through bounded prompts, verification, debugging, and presentation prep, with friend review when helpful.
- No laptop/browser takeover or GUI automation unless explicitly requested later. Provide manual steps, commands, expected outputs, and safe failure-report templates.
- Follow design.md for the offline HTML handbook: existing palette, rem-based readable text, control contrast, 48px targets, unboxed explanations, search, theme/progress/notes, mobile chapter jump.
- Mid-semester report deadline was 25 October 2026, for ER and normalized schema. Final announcement requires ER fidelity or justified deviations, five reusable transactionally consistent functions, useful error handling, a live demo and a 10-minute Shark Tank pitch plus Q&A. All members must understand everything; actual names/team size/final date are not established by placeholders.

## Work completed in this context correction

Read all chat pages, all slide/notes text, the team guide, SVG labels, both original diagram PNGs, and selected rendered chat pages. Created searchable source extracts, source index, source hashes, exact-column baseline, technical review notes, and a historical copy of the earlier proposal. Updated README, AGENTS, requirements, design-change log, learning guide and manual tests to the actual model. No source binary, executable SQL, application, agent script, or final deck was created/modified by this correction.

The subsequent user-requested cleanup moved current source artifacts into their functional directories, removed nine obsolete files and empty old source/report directories, and replaced the historical proposal copy with a concise migration record. Added meaningful guides at `database/README.md`, `server/README.md`, `client/README.md`, `agents/README.md`, `diagrams/README.md` and `docs/presentation/README.md`. These prepare implementation; they do not claim an executable codebase exists. All links and source-manifest paths were updated. Do not recreate the removed inventory/competing proposal files.

Current proposed evaluated methods: **publishPost, addComment, castVote, submitEditProposal, reviewEditProposal**. Registration/authentication/key lifecycle/reads/search/direct-author revisions are necessary supporting operations, not removed scope.

## Next useful task

1. Review baseline.md's constraint/normalization issues and reconcile ENUMs, nullability/delete policies, same-post replies, citation XOR, subtype integrity, review authorization and result uniqueness.
2. Write executable MySQL schema, seed data and derived views using exact baseline names. Decide whether the approval procedure or application owns its transaction; do not nest competing begin/commit logic. Record justified enforcement changes in change-log.md.
3. Implement dual human/agent auth and key lifecycle, then one publish flow and a scripted external agent. Finish the five evaluated methods, review UI, citations, votes and history in explainable increments.
4. Supply real user-run success/late-failure/repeat/concurrency tests and reproducible commands. Prepare final pitch using actual evidence and the existing mid-semester deck as a source.

The full Mid-Semester Report, DBMS_Project_Learning_Guide.docx, diagram generators/DOT and Slide_Images.zip are mentioned but absent. Ask for report/learning-guide exports if available to verify detailed reasoning; diagrams/deck are already present, so do not request them as missing. Do not infer official submission receipt/approval.

## Review cautions and verification

The slides claim every table is BCNF; this is inherited, not independently certified. Check the reply-parent conditional dependency and nullable semantics, the 2NF/BCNF teaching example, all candidate keys, and the relationship-count convention. A cycle does not automatically violate 3NF, nor does a rich domain automatically violate 1NF. The baseline records these issues without modifying original sources.

All 14 table names and every baseline column were checked against the schema SVG. Source hashes, extraction completeness, guide structure/links, and inline JavaScript syntax are checked through file tools only. No GUI, live MySQL, or application runtime testing is performed for this update. The handbook's transaction panel is a browser teaching model, not database evidence. Keep this handoff aligned with actual code and commands as implementation begins.
