# Database Management System for a Blogging Site for AI agents and Humans

This repository is the working home for the **entire course project**: requirements, ER diagrams, normalized schema, SQL/database implementation, application code, five reusable prototype functions, tests, reports, and the final presentation. All further coding and project work will continue here.

The exact allotted topic is **"Database Management System for a Blogging Site for AI agents and Humans"**. A suggested product direction is a blogging platform where humans and AI agents have clearly identified accounts and can publish and discuss posts. Specific features are proposals until reconciled with the submitted ER design.

Open [the interactive project field guide](Project_Workflow.html) in a browser for a **60-minute study route** through architecture, proposed files, database operations, build stages, Codex prompts, debugging, and the final presentation. It follows [design.md](design.md), works offline, and includes search, theme switching, study progress, notes, and a browser-only transaction simulation. This is a learning artifact; its proposed application files are not implemented yet.

## Course requirements

The mid-semester requirement was a report containing **ER diagrams and normalized schema**, due **25 October 2026**. This is the historical mid-semester deadline; no final-submission or evaluation date has been provided.

The latest announcement requires:

- Continue the same allotted project; titles will not be shuffled.
- Faithfully implement the submitted ER diagram. Any changes need clear, technically sound justification.
- Implement **five meaningful prototype functions as reusable methods**, callable repeatedly. Interdependent operations in a logical transaction must succeed or roll back together.
- Handle failures and provide enough error information for investigation and troubleshooting.
- Give a **live demonstration**. Every member must understand the complete project; grading is at team level.
- Deliver a **10-minute Shark Tank-style pitch**, followed by Q&A: problem, solution, design effectiveness, the five operations, and product value. Teams choose presenters; everyone must be ready for questions.

The [requirements record](docs/requirements/course-project.md) preserves the supplied messages. The professor provided **no example ER diagram**, so we can choose a clear conventional notation.

## Current status and design mismatch

The user identifies the existing Claude-generated ER diagrams and another PPT as previous work and says they may be revised. The available diagram/report files describe **Inventory and Warehouse Management**, while the confirmed allotted topic is the blogging site. The PPT and a verified blogging-site submitted ER/schema are not present.

Resolve this mismatch before claiming that the final implementation matches the submission. Preserve the actual submitted design, compare it with the proposed model, and record technical reasons for changes in the [design-change log](docs/design/change-log.md). Existing inventory files remain historical references.

There is **no executable blogging application, database implementation, or application test suite** yet. The confirmed stack is **MySQL + Express + Node.js + React with TypeScript/TSX and Tailwind CSS**. The user chose SQL/MySQL for course suitability and familiarity. Use InnoDB tables and readable parameterized SQL through `mysql2/promise`; Vite is the suggested frontend tool. Dependency versions and authentication remain to be chosen. A [proposed blogging model and five functions](docs/design/proposed-model.md) offer a starting point; they are not approved or implemented features.

## Repository guide

```text
AGENTS.md                         Instructions for continuing the whole project
README.md                         Overview, status, and requirements
Project_Workflow.html              Offline interactive project field guide
design.md                         User-supplied handbook design system
.gitignore                        Temporary-file exclusions
diagrams/                         Historical inventory Draw.io and PNG
docs/
  requirements/
    course-project.md             Supplied topic and course announcements
    README.md                     Available sources and remaining inputs
  design/
    proposed-model.md             Suggested blogging model and five functions
    change-log.md                 Submitted-baseline status and revision records
  testing/
    manual-checklist.md            User-run HTML, SQL, and application checks
  context/
    handoff.md                    Current project decisions and next steps
    inventory-handoff.md          Superseded inventory-project handoff
    claude-chat.pdf               Historical inventory conversation
    claude-chat.txt               Searchable historical conversation
  report/
    part1.md                      Historical inventory report
    part1.pdf                     Historical inventory PDF
```

Read the [handoff](docs/context/handoff.md) and [agent instructions](AGENTS.md) before continuing. Original artifact filenames remain documented in the [historical handoff](docs/context/inventory-handoff.md#original-file-locations).

## Design and implementation direction

Use a readable **Crow's Foot ER diagram**, with explicit keys, optionality, and cardinalities, plus a relational schema explaining normalization. If the actual submission uses Chen/EER, retain or map that conceptual view clearly. No particular notation was mandated in the supplied announcements.

The proposal covers human/agent identities, agent ownership, posts and revisions, comments, tags, and moderation. Its five suggested functions are agent registration, publishing, revising, commenting, and moderating. The [design note](docs/design/proposed-model.md) explains their transaction boundaries and failure cases.

Use the chosen MySQL + React/Express/Node TypeScript/TSX + Tailwind stack. Match normalized tables, keys, constraints, and transaction boundaries to the submitted/revised ER model. Use one acquired MySQL connection for each logical transaction and release it after commit/rollback. Add source, database, test, and presentation directories as they contain real work. Document installation, migrations, seed data, configuration, and run commands here once available. Live model calls are optional unless a later requirement makes them necessary; agent-authored content can be demonstrated with reproducible fixtures.

## Manual verification

Follow [the manual testing checklist](docs/testing/manual-checklist.md). You run the browser and live MySQL checks yourself; agents should provide steps and expected outputs without taking over the laptop. HTML checks can run now; application tests and npm commands must wait until real code/scripts exist.

## Completion checklist

- [ ] Identify the submitted ER diagram, normalized schema, and existing PPT; resolve the topic mismatch.
- [ ] Finalize blogging requirements, ER model, keys, constraints, and normalization rationale.
- [ ] Justify design changes and align diagrams, schema, and implementation.
- [ ] Implement database and application here with reproducible setup and demo data.
- [ ] Implement five reusable functions with appropriate transactions and clear errors.
- [ ] Verify success, rollback, repeated calls, constraints, and relevant concurrent edits.
- [ ] Prepare the live demo, 10-minute pitch, and whole-team Q&A preparation.
- [ ] Confirm evaluation date and submission details when announced.
