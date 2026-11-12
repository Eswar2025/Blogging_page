# Manual verification: run these yourself

Agents should provide steps and expected outputs without controlling your laptop or browser. This checklist is instructions, not a record that tests passed. The blogging application and its test scripts do not exist yet.

## 1. Check the HTML guide now (about five minutes)

Open `Project_Workflow.html` in your browser and refresh after edits.

| Action | Expected result |
| --- | --- |
| Read chapters 2, 3, and 5 | MySQL tables, SQL keys, mysql2, and connection-based transactions; the chosen stack is React TSX + Tailwind + Node/Express + MySQL |
| Switch dark/light themes | Readable text, clear inputs/buttons, and no new accent colors; refresh keeps the theme if browser storage is available |
| Narrow the window or use your browser's responsive mode | Sidebar is replaced by a labeled Jump to chapter selector; select chapter 10 and press Go; its heading appears |
| Search for `MySQL`, then a nonsense string | Relevant blocks show; nonsense shows No matching chapters; Clear search restores the route |
| Search, then use chapter navigation | The destination remains reachable even if search previously hid it |
| Mark a chapter learned and refresh | Its state remains if storage is available; click Learned / undo to revert |
| Write a test question and use Download questions | A text file contains the question; do not overwrite real notes merely to test |
| Run the publish simulation with success | Counts become **3 posts / 3 revisions / 5 tag links** |
| Choose failure and run again | Counts stay **2 / 2 / 3**; rollback is explained; each run uses the same starting fixture |
| Increase browser zoom to 200% and navigate with Tab | Content remains usable, controls reflow, focus is visible; code/tables may scroll internally |

The simulator is a browser teaching model. It does not connect to MySQL and cannot prove application transactions work. If storage or copying is unavailable, expect an explanatory fallback rather than a broken page.

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

1. Apply the supplied schema/migrations, then the seed dataset. Use `SHOW TABLES`, `SHOW CREATE TABLE`, and the ER diagram to compare names, PKs, FKs, unique constraints, types, and engine settings.
2. Confirm all participating tables use InnoDB. Keep schema changes outside the business transaction being tested.
3. Attempt a duplicate unique value and an invalid FK reference in controlled test data. Expect rejection and unchanged relevant rows. Do not disable FK/unique checks to make a test pass.
4. Confirm semantic rules such as human ownership, account subtype matching, and moderator roles are enforced where PK/FK constraints alone are insufficient.

## 4. Test the five real methods when implemented

Start the API/client using the documented commands. For each method: record starting rows, run a success case, run a controlled failure case, inspect persisted rows, and run another valid call. Use fixture IDs and queries supplied with the implementation; check rows by ID, not only global counts.

| Method | Success evidence | Failure / consistency evidence |
| --- | --- | --- |
| registerAgent | ACCOUNT and AGENT_PROFILE both exist and ownership matches | Forced profile failure after account insertion leaves neither new row |
| publishPost | POST, first POST_REVISION, tag links, and any newly required tags commit together | A failure after an early write leaves no partially published post, revision, or new associations |
| revisePost | New revision exists; old content remains available; tags update consistently | Two clients using the same expected revision yield one winner and one conflict, with no lost update |
| addComment | Comment/parent/author point to the correct post and identities | Cross-post parent and unauthorized actor are rejected; a moderation race follows the documented commentability rule |
| moderatePost | Status and a reasoned MODERATION_ACTION event commit together | Forced audit insertion failure restores the earlier status and leaves history unchanged |

Controlled failures must be available only through test/demo tooling, not a public production endpoint. Every transactional query must run on the same acquired connection. SQL reads/writes should be parameterized; error responses should be useful without exposing secrets or internal traces.

Use two browser tabs/API clients for stale edits, and a coordinated integration test for precise race ordering. A manual click sequence alone does not prove every concurrency case. Capture the test runner's actual output when scripts exist.

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
