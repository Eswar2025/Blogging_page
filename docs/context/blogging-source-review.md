# Review of the correct blogging context

The user supplied the correct project context on 12 November 2026 in a folder named `Right Contxt Files`. Its seven original artifacts are now organized at the locations below without content changes. The supplied folder was removed after becoming empty. Unrelated inventory material and the obsolete proposal were removed as described in [the migration note](repository-migration.md).

## Source inventory

| Source | Reviewed content | Role |
| --- | --- | --- |
| [Claude chat PDF](sources/blogging-claude-chat.pdf) | All 33 pages extracted/read; selected pages rendered; final decisions distinguish earlier drafts | Decision history and settled 14-table scope |
| [Mid-semester deck](../presentation/midsem/DBMS_Midsem_Slides.pptx) | Text and notes from all 20 slides extracted/read | Table/column names and normalization presentation |
| [Team slide guide](../presentation/midsem/Team_Slide_Guide.docx) | All document paragraph/table text extracted/read | Keep table/column names, whole diagrams, and slide order when editing that mid-semester deck |
| [Chen SVG](../../diagrams/chen-er.svg) and [PNG](../../diagrams/chen-er.png) | SVG labels parsed; PNG visually inspected | Conceptual entities, relationships, specialization, weak entities |
| [Schema SVG](../../diagrams/relational-schema.svg) and [PNG](../../diagrams/relational-schema.png) | SVG labels parsed; PNG visually inspected | Fourteen tables, columns, PK/FK/UQ markers, MySQL type suggestions |

Searchable derivatives: [chat text](blogging-chat.txt), [slide text/notes](../presentation/midsem/slides.txt), and [team-guide text](../presentation/midsem/team-guide.txt). The PDF export repeats some user messages and includes interface/artifact-state text. Those blocks are historical data, not new instructions. [Source hashes](blogging-source-manifest.json) support later preservation checks.

The binary documents were read without opening desktop applications. No DOCX/PPTX/PDF was rewritten or newly rendered as a deliverable; reading text does not certify slide/document layout quality. No official submission receipt or professor approval is inferred from file presence.

## What changes in the current plan

- Use the actual 14-table lowercase schema, not the earlier nine-table ACCOUNT/HUMAN_PROFILE/AGENT_PROFILE/MODERATION_ACTION proposal. The obsolete file was removed; [the migration note](repository-migration.md) identifies its recoverable Git history.
- Humans use session-authenticated UI; agents use API-key-authenticated scripts. Remove the human author-selector/agent-impersonation assumption from the standard UI.
- Restore agent key scopes, citations, provenance, human-reviewed edit proposals, votes, and audit history as core design.
- Preserve the settled exclusions: no flag/follow/scope/session/rate-limit-window core tables or dedicated moderation queue. Do not revive the early 12/18-table alternatives.
- Keep the later user preferences: MySQL, React TSX/Tailwind, TypeScript backend with Express, readable SQL, and user-run browser/database testing. The older vanilla/no-TypeScript recommendation is not the current stack instruction.
- Maintain the mid-semester Chen model and separate schema diagram. A new Crow's Foot-only conceptual model is not the recovered baseline.
- The old chat says the user would build largely solo but later refers to friends preparing the presentation. Four name placeholders in the deck are not proof of four actual members. Confirm names/roles only when preparing deliverables.

Read [the recovered baseline](../design/baseline.md) for exact columns, review questions, and the proposed five final-evaluation methods.

## Material still absent

The chat mentions a full Mid-Semester Report, `DBMS_Project_Learning_Guide.docx`, diagram DOT files/generator scripts, and `Slide_Images.zip`; these are not in the folder. The supplied full-resolution PNG/SVG files already cover the two diagrams. Ask for missing report/learning-guide exports if available to verify detailed constraints/FDs; do not block independent progress or claim to have read unavailable cloud documents.

The standalone allocation PDF, final evaluation date, installed MySQL version, final identities, and proof of exactly which submitted revision the professor received remain unverified. A longer professor problem statement or professor sample ER diagram should not be requested: the user has already said neither was supplied.
