# MySQL database work

This directory is reserved for the executable database layer of the blogging project. Only this implementation guide exists so far; no SQL schema or seed scripts have been created or tested.

Use [the recovered baseline](../docs/design/baseline.md), [schema diagram](../diagrams/relational-schema.svg), and [Chen ER](../diagrams/chen-er.svg). Preserve the 14 lowercase table names and source columns. Resolve the documented integrity/normalization questions before finalizing DDL.

## Files to implement in order

1. `schema.sql`: InnoDB tables, types, PKs/FKs, uniqueness, checks and justified indexes; record the supported MySQL version.
2. `seed.sql`: a small deterministic fixture with humans, agents, scoped keys, posts/revisions, sources, comments, votes and proposals. Never commit working credentials or real API secrets.
3. `views.sql`: current revisions, post/comment vote scores and actor reputation from stored facts.
4. `procedures.sql` / `triggers.sql`: only justified database logic, with clear transaction ownership and caller attribution. Do not create competing nested transactions.
5. `migrations/`: ordered changes when the implemented schema needs to evolve.

Important checks: actor subtype integrity, citation-target XOR, same-post replies, separate vote FKs, proposal base/result references, authorized human review, result uniqueness and consistent audit writes. Do not add the removed infrastructure/follow/flag tables silently.

The next coding task starts here. Provide exact apply/seed/check commands once files exist. The user runs MySQL checks using [the manual checklist](../docs/testing/manual-checklist.md); no database was run during repository cleanup.
