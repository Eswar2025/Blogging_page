# Project handoff

Last updated: 2026-11-12.

## Active project and scope

**Database Management System for a Blogging Site for AI agents and Humans** is the exact allotted topic confirmed by the user. This repository is the home for the complete project: code, SQL, ER diagrams, normalized schema, reports, reusable prototype functions, tests, live demo, and presentation.

The earlier inventory-only Part 1 scope is superseded. Preserve [inventory-handoff.md](inventory-handoff.md) as history; do not follow it as active project instructions. The existing report, Draw.io diagram, PNG, and exported Claude conversation concern inventory management and remain unchanged as reference material.

## Confirmed requirements and user answers

- The topic title was the entire project-specific statement. Other teams' topics are irrelevant.
- Mid-semester report required ER diagrams and normalized schema, due 25 October 2026.
- Latest announcement requires the same allotted project, fidelity to submitted ER, technically justified changes, five meaningful reusable functions, atomic interdependent operations, useful failure handling, a live demo, and a 10-minute Shark Tank pitch plus Q&A.
- Grading is at team level; every member must understand the entire project and answer questions. Team size is not established by that announcement.
- Professor supplied no example ER. Do not request one.
- Asked what was submitted, the user answered: "the above ER diagrams claude alreadyy created, and another ppt, but we can change them if needed!"
- That permits changes but does not resolve the mismatch between available inventory diagrams and the allotted blogging title. Identify the actual submitted baseline; do not reclassify inventory content as blogging work or claim professor approval.
- No final deadline/evaluation date or mandated technology stack has been supplied.

Read the [requirements record](../requirements/course-project.md) for supplied announcements and source limitations.

## Current repository state

- README and AGENTS cover the complete blogging-site project and final requirements.
- The [proposed model](../design/proposed-model.md) suggests Crow's Foot notation, human/agent identities, posts/revisions/comments/tags/moderation, and five functions. These are proposals, not approved or implemented features.
- The [change log](../design/change-log.md) records the unresolved submitted baseline and suggested domain correction.
- No blogging ER export, executable database/application implementation, seed dataset, or application tests exist yet. The database choice is now **SQL/MySQL only**; retain React TypeScript/TSX, Tailwind CSS, Node, and Express. Use InnoDB and explicit parameterized SQL via mysql2/promise as the initial plan. Vite is suggested; versions and authentication remain undecided. The previous database preference is superseded.
- [Project_Workflow.html](../../Project_Workflow.html) is a self-contained offline learning/build guide following the user's [design.md](../../design.md). Its ten chapters total 60 minutes of study and cover product scope, architecture, ER-to-MySQL table mapping, request flow, five functions, proposed files/screens, phased prompts and verification, debugging, and the pitch. It includes local study progress/notes, search, theme switching, copyable prompts, and a browser-only transaction simulation. It is not the blogging application's frontend or a real database test.
- The user expects to spend their project time prompting Codex, verifying outputs, debugging, and preparing presentations. Keep work in bounded, explainable slices with concrete acceptance evidence, and support questions/discussion with their developer friend.
- The PPT is not available here. No allocation PDF was newly attached; the user's supplied exact title establishes the topic.
- Existing historical files remain at `docs/report/part1.*`, `diagrams/er_diagram.*`, and `docs/context/claude-chat.*`. The old handoff preserves original filenames and earlier review notes.

## Next useful work

1. Identify/preserve the submitted ER, normalized schema, and PPT; reconcile them with the allotted topic.
2. Compare the blogging proposal with that baseline and record material changes with technical reasons and key/cardinality/normalization impacts. Continue unrelated documentation while missing material is pending.
3. Finalize a comprehensible blogging model and schema with functional dependencies and normalization rationale. Suggested notation is Crow's Foot; retain/map a Chen/EER view if appropriate to the submission.
4. Use the chosen MySQL + React TSX/Tailwind + Node/Express TypeScript stack. Record the installed MySQL version, InnoDB tables, SQL constraints, and transaction connection boundaries. Implement here with actual setup/schema/seed/run instructions; do not reopen the database choice.
5. Build five reusable methods, transactions, diagnostics, and meaningful success/rollback/repeated-call checks.
6. Prepare demo data, repeatable live-demo flow, a 10-minute product pitch, and whole-team Q&A preparation. Confirm schedule when announced.

## Open design choices

Exact operation choices, UI requirements, authentication, agent ownership/credentials, moderation permissions, revision rules, deletion policy, and live AI integration are unspecified. The proposal gives concrete suggestions. Modeling agent authors does not inherently require live model calls.

## User-run testing and UI review

The user explicitly asked that agents stop controlling their laptop/browser to conserve usage. Provide manual steps and expected results; no GUI automation unless they explicitly request it later. [The manual checklist](../testing/manual-checklist.md) separates immediate handbook checks from future SQL/application checks.

The agreed design refinements are applied to `design.md` and the HTML: 16px rem-based body text, 20px topic headings, 14px useful secondary/code text, readable numerals, a control-border token using the same palette, 48px control targets, unboxed reading blocks, explicit state labels, and mobile chapter navigation. Prior browser review verified both themes and a 375px chapter jump; a narrower-screen check was interrupted. This MySQL update uses text/syntax checks only.

## Validation and continuity

The workflow-guide update adds an HTML study artifact and updates project documentation; no blogging application was implemented. Static checks cover ten chapters totaling 60 minutes, unique IDs, existing local links/anchors, inline JavaScript syntax, palette compliance, and no external runtime dependencies. Chrome was used to inspect the wide and narrower desktop layouts and confirm live search's empty-result state. Prior design review checked both themes and a 375px chapter jump; narrower-width and exhaustive interaction checks were not completed; no real database behavior is claimed as tested. Keep this note and README current as implementation develops.

The MySQL switch updates the HTML, README, agent instructions, requirements, proposed model, change log, and manual testing checklist. Current verification is limited to source/link/syntax checks. No browser takeover or live MySQL/application testing was performed for this update.
