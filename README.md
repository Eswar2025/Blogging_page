# Database Management System for a Blogging Site for AI agents and Humans

This repository is the working home for the **entire course project**: requirements, ER diagrams, normalized schema, SQL/database implementation, application code, five reusable prototype functions, tests, reports, and the final presentation. All further coding and project work will continue here.

The exact allotted topic is **"Database Management System for a Blogging Site for AI agents and Humans"**. A suggested product direction is a blogging platform where humans and AI agents have clearly identified accounts and can publish and discuss posts. Specific features are proposals until reconciled with the submitted ER design.

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

There is **no executable application, SQL implementation, chosen DBMS/framework, or test suite** yet. A [proposed blogging model and five functions](docs/design/proposed-model.md) offer a starting point; they are not approved or implemented features.

## Repository guide

```text
AGENTS.md                         Instructions for continuing the whole project
README.md                         Overview, status, and requirements
.gitignore                        Temporary-file exclusions
diagrams/                         Historical inventory Draw.io and PNG
docs/
  requirements/
    course-project.md             Supplied topic and course announcements
    README.md                     Available sources and remaining inputs
  design/
    proposed-model.md             Suggested blogging model and five functions
    change-log.md                 Submitted-baseline status and revision records
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

Choose the DBMS and application stack when implementation starts, using course constraints and the submitted design. Add source, database, test, and presentation directories as they contain real work. Document installation, migrations, seed data, configuration, and run commands here once available. Live model calls are optional unless a later requirement makes them necessary; agent-authored content can be demonstrated with reproducible fixtures.

## Completion checklist

- [ ] Identify the submitted ER diagram, normalized schema, and existing PPT; resolve the topic mismatch.
- [ ] Finalize blogging requirements, ER model, keys, constraints, and normalization rationale.
- [ ] Justify design changes and align diagrams, schema, and implementation.
- [ ] Implement database and application here with reproducible setup and demo data.
- [ ] Implement five reusable functions with appropriate transactions and clear errors.
- [ ] Verify success, rollback, repeated calls, constraints, and relevant concurrent edits.
- [ ] Prepare the live demo, 10-minute pitch, and whole-team Q&A preparation.
- [ ] Confirm evaluation date and submission details when announced.
