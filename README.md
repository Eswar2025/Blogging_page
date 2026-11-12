# Database Management System for a Blogging Site for AI agents and Humans

This repository is the home for the complete course/resume project: ER design, normalized schema, MySQL SQL, backend, React TSX frontend, agent client, tests, reports, and final presentation.

Humans use the website. Agents use the API with their own scoped keys. Both are actors that can publish, comment, vote, and propose edits. Authorized humans review edit proposals; approval creates a new attributed revision. Citations, provenance, and audit history make the collaboration traceable.

## Start here

1. Open [Project_Workflow.html](Project_Workflow.html) in a browser for the updated 60-minute learning/build route.
2. Read [the recovered 14-table baseline](docs/design/baseline.md) and [source review](docs/context/blogging-source-review.md).
3. Continue with [AGENTS.md](AGENTS.md), [the current handoff](docs/context/handoff.md), and [the manual checklist](docs/testing/manual-checklist.md).

## Correct source material and current status

The [original blogging sources](docs/context/blogging-source-review.md) are organized by purpose: the 33-page chat PDF under `docs/context/sources/`, the 20-slide deck and team guide under `docs/presentation/midsem/`, and the Chen ER/table-schema SVG+PNG pairs under `diagrams/`. All seven artifacts retain their original contents. Searchable extracts and a path/hash manifest make them easy to inspect and verify.

The recovered design has **11 conceptual entity sets, 2 weak entities, and 14 relational tables**:

```text
actor, human_user, ai_agent, api_key,
post, post_revision, revision_source, tag, post_tag,
comment, post_vote, comment_vote, edit_proposal, audit_log
```

Use those names and columns from the actual source diagrams. Unrelated inventory material and the superseded proposal have been removed from the working tree. [The migration note](docs/context/repository-migration.md) records what moved/was removed and how earlier committed material remains recoverable.

**No executable application, SQL schema, seed data, agent script, or application test suite exists yet.** Recovered design files are evidence of prior work, not proof of professor approval or an implemented database. The missing full report/learning guide and several technical review questions are recorded in the source review/baseline.

## Stack and product boundaries

- **MySQL/InnoDB**, readable parameterized SQL via `mysql2/promise`, Node/Express TypeScript, **React TSX + Tailwind CSS**; Vite is suggested. Record actual installed versions during setup.
- Human login/session and agent API keys resolve to one actor identity. Human publishing uses the logged-in human; agent publishing comes from its own authenticated client. An agent dashboard manages ownership/keys, not a default browser author-impersonation selector.
- Keep revision provenance, citations, threaded comments, separate post/comment votes, edit proposals, key permission flags, and audit history.
- Current content, vote scores, and reputation are derived through queries/views. Keep title/body in revisions. Do not silently add stored pointers/counters.
- No follow/flag/scope-join/session/rate-limit-window core tables or dedicated moderation queue. Basic moderator status permissions remain possible using existing columns/audit history.
- Start with a scripted agent. Optional LLM integration, deployment, performance evidence, and stronger infrastructure come after the database/API are defensible.

## Five proposed evaluation functions

`publishPost`, `addComment`, `castVote`, `submitEditProposal`, and `reviewEditProposal` demonstrate the recovered model. Human/agent registration, key issuance/revocation, authentication, reading/search, and direct-author editing remain supporting work. The professor requires five reusable functions; these names are our current implementation proposal.

Use one transaction-owning layer and one acquired MySQL connection for each logical operation. Verify success, late-failure rollback, repeated calls, authorization, and relevant races. Proposal review must protect against stale revisions and duplicate concurrent approvals.

## Course deliverables

The mid-semester report required ER diagrams and normalized schema by **25 October 2026**. The supplied mid-semester diagrams use **Chen notation** for the conceptual model and a separate **Crow's Foot table view**. The slides claim BCNF; validate the actual dependencies rather than repeating that claim as proven.

The final announcement requires the same allotted topic, faithful implementation of the submitted ER or technically justified changes, five reusable functions with atomic interdependent operations and useful errors, a live demo, and a **10-minute Shark Tank pitch plus Q&A**. Every member must understand the entire project. No final date has been supplied. See [the announcement record](docs/requirements/course-project.md) and [change log](docs/design/change-log.md).

## Repository guide

```text
.
|-- AGENTS.md
|-- README.md
|-- Project_Workflow.html          Offline study/build guide
|-- design.md                      Handbook visual and UX rules
|-- .gitignore                     Local scratch-file exclusions
|-- database/README.md             SQL files, constraints and implementation order
|-- server/README.md               Express/SQL/auth/service responsibilities
|-- client/README.md               React TSX screens and API boundaries
|-- agents/README.md               Independent scripted agent plan
|-- diagrams/
|   |-- README.md
|   |-- chen-er.svg / .png
|   `-- relational-schema.svg / .png
`-- docs/
    |-- context/
    |   |-- handoff.md
    |   |-- blogging-source-review.md
    |   |-- blogging-source-manifest.json
    |   |-- blogging-chat.txt
    |   |-- repository-migration.md
    |   `-- sources/blogging-claude-chat.pdf
    |-- design/baseline.md / change-log.md
    |-- requirements/README.md / course-project.md
    |-- testing/manual-checklist.md
    `-- presentation/
        |-- README.md
        `-- midsem/
            |-- DBMS_Midsem_Slides.pptx
            |-- Team_Slide_Guide.docx
            |-- slides.txt
            `-- team-guide.txt
```

The [database](database/README.md), [server](server/README.md), [client](client/README.md), and [agent](agents/README.md) directories currently contain useful implementation guides, not executable code or empty scripts. Add actual schema/seed/package/run/test files and commands when implementing their stages. See [presentation materials](docs/presentation/README.md) for the existing deck and later final-pitch work.

## Next work and verification

Reconcile the recovered model's technical review questions, preserve the actual submitted snapshot when identified, and prepare executable MySQL schema/seed SQL. Then implement both authentication paths, a scripted agent, the five functions, and their UI/API flows in small explainable steps. Build evidence as you go; adapt the existing mid-semester deck into a final product pitch later.

The user runs browser and live database checks. Agents provide instructions and expected outputs **without taking over the laptop/browser**. Text/link/syntax checks are inexpensive supporting verification. No automated browser control unless the user explicitly asks later.
