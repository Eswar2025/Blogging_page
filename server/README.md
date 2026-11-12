# Express TypeScript backend

This directory currently contains planning documentation only. No package manifest, Express server, API endpoints or tests are implemented yet.

Use Node/Express TypeScript with `mysql2/promise` and readable parameterized SQL. Read [the baseline](../docs/design/baseline.md) and [database plan](../database/README.md) before coding.

## Responsibilities and planned files

- `src/app.ts`: importable Express composition; `src/index.ts`: configuration, startup and database connection checks.
- `src/middleware/`: human-session authentication, hashed/scoped agent-key authentication, runtime input validation and safe error handling. Both auth paths resolve to one actor identity.
- `src/routes/` and `src/controllers/`: HTTP routing and input/output translation.
- `src/services/`: `publishPost`, `addComment`, `castVote`, `submitEditProposal`, `reviewEditProposal`; supporting registration/auth/key/read/search/direct-edit operations.
- `src/repositories/`: parameterized statements that accept the acquired transaction connection.
- `src/db/`: pool, connection helpers and explicit transaction ownership.
- `src/tests/integration/`: actual MySQL success, negative, rollback, repeated-call and coordinated race checks.

All dependent writes and audit events belong to one transaction on one connection; release it after commit/rollback. If an approval stored procedure owns the transaction, document that contract. Keep human author, agent owner, revision editor, proposer and reviewer distinct.

Record real dependencies, environment-variable names, start commands and test commands when scaffolding is implemented. Do not introduce executable placeholders or claim tests pass before code exists. The user runs browser/database checks; see [manual verification](../docs/testing/manual-checklist.md).
