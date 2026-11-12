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
- No blogging ER export, executable DDL/application, chosen DBMS/framework, seed dataset, or tests exist yet.
- The PPT is not available here. No allocation PDF was newly attached; the user's supplied exact title establishes the topic.
- Existing historical files remain at `docs/report/part1.*`, `diagrams/er_diagram.*`, and `docs/context/claude-chat.*`. The old handoff preserves original filenames and earlier review notes.

## Next useful work

1. Identify/preserve the submitted ER, normalized schema, and PPT; reconcile them with the allotted topic.
2. Compare the blogging proposal with that baseline and record material changes with technical reasons and key/cardinality/normalization impacts. Continue unrelated documentation while missing material is pending.
3. Finalize a comprehensible blogging model and schema with functional dependencies and normalization rationale. Suggested notation is Crow's Foot; retain/map a Chen/EER view if appropriate to the submission.
4. Establish stack constraints, choose DBMS/framework, and implement here with setup/migration/seed/run instructions.
5. Build five reusable methods, transactions, diagnostics, and meaningful success/rollback/repeated-call checks.
6. Prepare demo data, repeatable live-demo flow, a 10-minute product pitch, and whole-team Q&A preparation. Confirm schedule when announced.

## Open design choices

Exact operation choices, UI requirements, authentication, agent ownership/credentials, moderation permissions, revision rules, deletion policy, and live AI integration are unspecified. The proposal gives concrete suggestions. Modeling agent authors does not inherently require live model calls.

## Validation and continuity

This update changes documentation only. Checks cover new local Markdown links, preservation of original artifacts, and whitespace; no database behavior or Mermaid rendering is claimed as tested. Keep this note and README current as implementation develops.
