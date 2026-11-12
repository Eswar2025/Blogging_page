# Agent instructions

## Job and active topic

Complete **Database Management System for a Blogging Site for AI agents and Humans** with the user. This repository is the home for all code and deliverables: requirements, ER diagrams, normalized schema, database, application, five prototype functions, tests, reports, demo, and presentation. Make concrete progress on requested tasks and explain decisions so every member can defend the complete project.

Read `README.md`, `docs/context/handoff.md`, and `docs/requirements/course-project.md` first. Inspect the working tree and new sources; preserve unrelated user edits.

## Sources and historical material

- The latest user instructions/course announcements establish the blogging topic and final-evaluation scope. The earlier inventory-only Part 1 scope is superseded.
- Existing `docs/report/part1.*`, `diagrams/er_diagram.*`, and `docs/context/claude-chat.*` concern inventory. They are historical references, not a verified blogging schema. `docs/context/inventory-handoff.md` is a superseded record, not current instructions.
- The user identifies Claude ER diagrams and another PPT as previous work and allows necessary revisions. The PPT is absent; available diagrams conflict with the allotted topic. Identify and preserve the actual submitted baseline before claiming compliance.
- No professor example ER diagram exists. Do not ask for one. Crow's Foot with keys, cardinalities, and optionality is suggested; retain/map a Chen/EER view if appropriate to the submission.
- `docs/design/proposed-model.md` is a proposal. Do not describe its features or methods as professor-mandated, approved, or implemented.
- The supplied title is the complete known project-specific statement. Do not insist on a longer statement or allocation PDF to begin; other teams' topics are out of scope.

## Course deliverables

- Mid-semester report: ER diagrams and normalized schema, historical deadline 25 October 2026. This is not the final deadline.
- Continue the allotted topic and faithfully implement the submitted ER. Record technically justified deviations in `docs/design/change-log.md`: before/after, reason, normalization/schema/data impact, affected artifacts, and validation. User permission to revise does not waive this requirement. Do not invent professor approval or a formal approval process absent from the announcement.
- Implement five meaningful, well-defined prototype functions as reusable methods callable repeatedly. Multi-query interdependent operations forming one logical transaction must commit or roll back together.
- Handle failures and provide understandable errors and useful safe diagnostic context. Do not log secrets or unnecessary personal data.
- Prepare a live demonstration and a 10-minute Shark Tank pitch, followed by Q&A, covering problem, solution, design, five operations, and value. Team-level grading and complete-project understanding apply to every member regardless of presenters.
- Final schedule, team size, mandated stack, and submission identity are not established by the announcement. Do not invent them.

## Design, implementation, and validation

- Reconcile the submitted baseline with the allotted topic; continue independent documentation and clearly marked proposals while inputs are pending.
- Check course/user stack constraints before implementation. If unconstrained, choose a practical DBMS/framework and record why. Avoid speculative dependencies and empty scaffolding.
- Distinguish human and agent identities/permissions. Ownership, moderation roles, authentication, and live AI integration are design choices to resolve.
- Document keys, nullability, cardinalities, business rules, functional dependencies, and normalization rationale. Do not claim 3NF solely from table appearance. Avoid unexplained duplicated content or counters.
- Keep diagram sources/exports, normalized schema, migrations, code, and reports consistent. Review rendered diagrams and generated documents/presentations after edits. Label historical/stale exports clearly.
- Place transactions at reusable method boundaries and protect authorization/state checks appropriately. Cover relevant uniqueness, referential integrity, duplicate calls, revision conflicts, and concurrency. Repeatedly callable does not mean identical duplicate input must always succeed; define clean rejection behavior.
- Validate success and rollback paths on the selected DBMS, including a failure after an early write. State exactly what was checked and remaining limitations. Keep reproducible setup, migration, seed, run, and demo commands in README.
- Modeling agent accounts does not inherently require paid/live model services. Prefer a repeatable demo unless live generation is a confirmed requirement.

## Organization and continuity

Use `docs/requirements/` for instructions/submission sources, `docs/design/` for models/change rationale, `diagrams/` for diagram files, and `docs/report/` for reports. Add code/database/test/presentation directories with real work. Keep temporary files under ignored `tmp/`; never commit secrets or local environments.

Preserve baseline and historical artifacts. Update links when moving files. After meaningful work, update `docs/context/handoff.md` and README with decisions, progress, verification, unresolved inputs, and next steps.

Proceed with authorized reversible work without routine confirmation. Ask concise questions for missing information that materially affects correctness while continuing independent work. Do not stop at a plan when implementation or editing was requested.
