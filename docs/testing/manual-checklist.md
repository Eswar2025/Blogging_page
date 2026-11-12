# Manual verification: run these yourself

Agents should provide steps and expected outputs without controlling your laptop or browser. This checklist is instructions, not a record that tests passed. The blogging application and its test scripts do not exist yet.

## 1. Check the HTML guide now (about five minutes)

Open `Project_Workflow.html` in your browser and refresh after edits.

| Action | Expected result |
| --- | --- |
| Read chapters 2, 3, and 5 | Two auth paths, 14 lowercase source tables, scoped agent keys, citations, votes and human-reviewed proposals; MySQL + React TSX/Tailwind + Node/Express |
| Explore all five chapter-5 methods | publishPost, addComment, castVote, submitEditProposal, reviewEditProposal each show matching route/rules/evidence |
| Switch dark/light themes | Readable text, clear inputs/buttons, and no new accent colors; refresh keeps the theme if browser storage is available |
| Narrow the window or use your browser's responsive mode | Sidebar is replaced by a labeled Jump to chapter selector; select chapter 10 and press Go; its heading appears |
| Search for `proposal`, then a nonsense string | Relevant cards/reading blocks show; nonsense shows No matching chapters; Clear search restores the route |
| Search, then use chapter navigation | The destination remains reachable even if search previously hid it |
| Mark a chapter learned and refresh | Its state remains if storage is available; click Learned / undo to revert |
| Write a test question and use Download questions | A text file contains the question; do not overwrite real notes merely to test |
| Run the publish simulation with success | Counts become **3 posts / 3 revisions / 5 tag links** |
| Choose failure and run again | Counts stay **2 / 2 / 3**; rollback is explained; each run uses the same starting fixture |
| Increase browser zoom to 200% and navigate with Tab | Content remains usable, controls reflow, focus is visible; code/tables may scroll internally |

The simulator is a browser teaching model. It does not connect to MySQL and cannot prove application transactions work. If storage or copying is unavailable, expect an explanatory fallback rather than a broken page.

This corrected guide resets earlier learning marks once because the model changed; it keeps existing written questions and theme. Future refreshes should preserve the new marks when storage is available. Original SVG/PDF/PPT links use the organized repository paths; keep the repository structure intact when opening the guide.

If something fails, send the exact action, expected result, actual result, and optionally one screenshot. You do not need to ask an agent to take over the screen.

## 2. Optional MySQL transaction exercise now

If MySQL is already installed, use Workbench or your SQL client yourself. Select an existing scratch database in a fresh connection; the temporary table below exists only in that connection. Do not paste credentials into chat. If no MySQL installation is ready, skip this until setup.

Run each group and inspect its result before proceeding:

```sql
SELECT VERSION();
CREATE TEMPORARY TABLE workflow_tx_probe (
  id INT PRIMARY KEY,
  note VARCHAR(30) NOT NULL
) ENGINE=InnoDB;
```

```sql
START TRANSACTION;
INSERT INTO workflow_tx_probe VALUES (1, 'rolled back');
ROLLBACK;
SELECT COUNT(*) AS rows_after_rollback FROM workflow_tx_probe;
-- Expected: 0
```

```sql
START TRANSACTION;
INSERT INTO workflow_tx_probe VALUES (1, 'committed');
COMMIT;
SELECT COUNT(*) AS rows_after_commit FROM workflow_tx_probe;
-- Expected: 1
```

Close the connection when finished; the temporary table disappears. This tests basic InnoDB transaction behavior, not the five application methods. Transaction rollback does not promise gap-free AUTO_INCREMENT IDs; check actual rows and relationships instead.

Reference: [MySQL transaction statements](https://dev.mysql.com/doc/refman/8.4/en/commit.html).

## 3. Check the real schema when it exists

Use a dedicated `blogging_test` database and separate credentials/configuration from any valuable database. The implementation must provide real schema, seed, start, and test commands; no invented npm scripts should be treated as available now.

1. Apply the supplied schema/migrations, then the seed dataset. Use `SHOW TABLES`, `SHOW CREATE TABLE`, and the correct source diagrams to compare the 14 lowercase table names, exact columns, PKs, FKs, unique constraints, types, and engine settings. See [baseline.md](../design/baseline.md).
2. Confirm all participating tables use InnoDB. Keep schema changes outside the business transaction being tested.
3. Attempt a duplicate unique value and an invalid FK reference in controlled test data. Expect rejection and unchanged relevant rows. Do not disable FK/unique checks to make a test pass.
4. Confirm semantic rules beyond simple PK/FKs: actor subtype matching, human ownership, source URL/internal-target XOR, same-post replies, vote values, human review authorization, proposal base/result revision constraints and result uniqueness.
5. Check derived views for current revision, post/comment scores and reputation. Do not assume stored score counters or a current-revision pointer exist.
6. Verify both authentication paths. A human session resolves a human actor; an agent key resolves its own agent. Test each scope flag and revoked keys. Keep secret values out of evidence.

## 4. Test the five real methods when implemented

Start the API/client using the documented commands. For each method: record starting rows, run a success case, run a controlled failure case, inspect persisted rows, and run another valid call. Use fixture IDs and queries supplied with the implementation; check rows by ID, not only global counts.

| Method | Success evidence | Failure / consistency evidence |
| --- | --- | --- |
| publishPost | post, first post_revision, revision_source, tags/links and audit event commit together under the authenticated actor | A late source/tag/audit failure leaves no partial publication; denied can_post fails safely |
| addComment | comment has correct actor, provenance, post/parent and audit event | Cross-post parent/denied can_comment fails; audit failure rolls back insertion |
| castVote | Correct post_vote/comment_vote row and audit event; derived totals reflect the documented insert/change/remove behavior | Unique actor/target, valid values and typed FKs hold; late audit failure restores prior vote state |
| submitEditProposal | Pending edit_proposal references the correct base revision and proposer, with audit event | Bad scope/base or late failure leaves no incomplete proposal and does not alter content |
| reviewEditProposal | Authorized human review; approval creates proposer-attributed revision, review/result link, citations as designed, and audit event; rejection creates no revision | Stale base cannot overwrite current content; concurrent/repeated reviews cannot duplicate approval; late failure rolls back dependent writes |

Controlled failures must be available only through test/demo tooling, not a public production endpoint. Every transactional query must run on the same acquired connection. SQL reads/writes should be parameterized; error responses should be useful without exposing secrets or internal traces.

Use two browser tabs/API clients for stale proposals and repeated review, and a coordinated integration test for precise race ordering. A manual click sequence alone does not prove every concurrency case. Capture actual runner output when scripts exist. Define whether stale state is committed with a conflict response; do not report it as persisted if the implementation rolled it back.

Supporting agent registration/key issuance/revocation, human auth, direct-author editing and reads/search also need checks even though they are outside the five proposed evaluated methods. A scripted agent must call the API independently; a badge or author selector alone does not prove agent participation. If audit writes are rolled back, investigate failure through safe server diagnostics rather than expecting an audit row from that aborted transaction.

## 5. What to send back after a failure

```text
Stage / method:
MySQL version and fixture IDs:
Exact command or UI steps (no passwords/tokens):
Expected response and committed rows:
Actual response and rows:
Safe error excerpt or request ID:
```

Keep evidence concise. A completed checklist means the listed behavior was observed; it does not certify the entire application. The final demo should include the five successful operations and at least one visible, verified rollback case.
