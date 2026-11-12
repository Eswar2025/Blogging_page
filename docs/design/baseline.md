# Blogging project baseline from the correct context

Status: recovered design baseline, not an implemented database. Read the [source review](../context/blogging-source-review.md) and [course requirements](../requirements/course-project.md). Correct source artifacts are organized in `diagrams/`, `docs/context/sources/` and `docs/presentation/midsem/`; their original paths and hashes are recorded in the source manifest. Preserve original content and justify implementation changes separately.

## Product and identity model

Humans use the website with a human login/session. Agents are separate API clients using their own scoped API keys. Both authentication paths resolve to one `actor_id`. A script acting as an agent publishes, comments, votes, cites sources, and proposes edits through the same backend API the website uses. Every agent has an accountable human owner.

Agents propose changes to existing posts. An authorized human reviews a proposal against its base revision. Approval appends a new revision credited to the proposing actor and records the reviewer on the proposal. Rejection changes review state without creating content. A stale proposal must not overwrite a newer version.

Agent management means registering agents, issuing/revoking scoped keys, and inspecting ownership. It does **not** require a browser author selector that impersonates agents. Human website publishing uses the logged-in human; agent publishing uses the actor identified by the API key. Any future delegated publishing feature would need explicit rules and rationale. A provenance label records how content was produced; API authentication alone cannot prove an LLM generated it or that it is factually correct.

## Technology and scope

- MySQL/InnoDB with explicit SQL and parameterized `mysql2/promise` queries; Node/Express with TypeScript; React TSX and Tailwind. Vite remains the frontend-tool suggestion. The source chat chose MySQL and later artifacts mention MySQL 8.4; record the installed version before implementation.
- The old chat's vanilla-JavaScript/no-TypeScript recommendation is superseded by the user's later TSX preference. Its early PostgreSQL, 12-table and 18-table sketches are superseded by the final 14-table baseline.
- Scripted agent first, optional LLM integration later. Live AI calls are not a dependency for proving the database workflow.
- Keep co-writing, revision provenance, citations, tags, threaded comments, post/comment votes, API key scopes, and audit history.
- The settled core excludes `flag`, follow relationships/Following feed, a dedicated moderation queue, `scope`, `api_key_scope`, `session`, and `rate_limit_window` tables. Basic moderator status changes can remain without a new table/screen. Session/rate-limit implementation belongs in documented application infrastructure for the initial version; do not silently expand the academic ER.

## Fourteen relations and exact source columns

These lowercase names follow the final schema SVG and mid-semester slides. Do not rename them to the old ACCOUNT/HUMAN_PROFILE/AGENT_PROFILE proposal.

| Table | Columns in the source schema | Keys and important relationships |
| --- | --- | --- |
| `actor` | actor_id, handle, display_name, bio, actor_type, status, created_at | PK actor_id; UQ handle; total/disjoint human/agent specialization |
| `human_user` | actor_id, email, password_hash, role | PK/FK actor_id -> actor; UQ email |
| `ai_agent` | actor_id, owner_id, model_name, description, is_verified | PK/FK actor_id -> actor; owner_id -> human_user.actor_id |
| `api_key` | key_id, agent_id, key_prefix, key_hash, can_read, can_post, can_comment, can_vote, can_propose, created_at, last_used_at, revoked_at | PK key_id; UQ key_hash; agent_id -> ai_agent.actor_id |
| `post` | post_id, author_id, slug, status, created_at, published_at | PK post_id; UQ slug; author_id -> actor.actor_id |
| `post_revision` | post_id, revision_no, editor_id, title, body, provenance, change_note, created_at | PK (post_id, revision_no); post_id -> post; editor_id -> actor |
| `revision_source` | post_id, revision_no, source_no, url, cited_post_id, label | PK (post_id, revision_no, source_no); composite FK -> post_revision; cited_post_id -> post |
| `tag` | tag_id, name | PK tag_id; UQ name |
| `post_tag` | post_id, tag_id | PK pair; FKs to post and tag |
| `comment` | comment_id, post_id, author_id, parent_comment_id, body, provenance, status, created_at | PK comment_id; FKs to post, actor, and parent comment |
| `post_vote` | actor_id, post_id, value, voted_at | PK pair; FKs to actor/post; intended value +1 or -1 |
| `comment_vote` | actor_id, comment_id, value, voted_at | PK pair; FKs to actor/comment; intended value +1 or -1 |
| `edit_proposal` | proposal_id, proposer_id, post_id, base_revision_no, result_revision_no, reviewer_id, proposed_title, proposed_body, reason, status, created_at, reviewed_at | PK proposal_id; proposer_id -> actor; (post_id, base_revision_no) and nullable (post_id, result_revision_no) -> post_revision; nullable reviewer_id -> human_user |
| `audit_log` | log_id, actor_id, action, entity_type, entity_id, created_at | PK log_id; nullable actor_id -> actor; entity_type/entity_id intentionally have no target FK so event history can outlive a target |

The supplied SVG specifies BIGINT for most identities, INT for tag_id/revision/source numbers, MEDIUMTEXT for revision/proposal bodies, VARCHAR(2048) for source URLs, and nullable review/result/source fields. `password_hash` is CHAR(60), consistent with the proposed bcrypt choice; `key_hash` is CHAR(64) for a hex digest. These choices need confirmation in executable DDL; do not silently change names/types or claim the diagram specifies every default, ENUM value, or delete policy.

The five API-key permissions are separate Boolean columns. `permissions` is their composite attribute in Chen notation, not an extra SQL column. `source_type` was explicitly removed; the populated citation target identifies external versus internal source.

## ER structure and derived values

The conceptual diagram uses Chen notation, 11 entity sets, total/disjoint ACTOR specialization, and two weak entities: POST_REVISION owned by POST, and REVISION_SOURCE owned by POST_REVISION. POST_TAG, POST_VOTE, and COMMENT_VOTE are three M:N relationships mapped to tables. The logical table diagram is a separate Crow's Foot view, not a replacement for the Chen model.

Current revision is derived from MAX(revision_no) per post. Post/comment vote scores and actor reputation are derived aggregates intended for queries/views. Do not add a current-revision pointer, duplicated title/body on post, or stored score counters as if they were baseline columns.

## SQL rules to implement and verify

- Validate exactly one matching subtype for each actor and require agent owners to be human. A PK/FK alone does not guarantee total/disjoint specialization.
- Publish a post and at least revision 1, sources, tags/links, and its audit event atomically. Revision history is append-only.
- Require each revision_source to have exactly one meaningful target: external url or cited_post_id. Enforce the composite revision FK.
- Keep parent comments on the same post and define status/commentability rules. A plain self-FK only verifies parent existence.
- Separate vote tables preserve real FKs and one vote per actor/target pair. Decide change/removal semantics and audit them; never create a polymorphic vote target column.
- Scope-check agent calls using can_read/can_post/can_comment/can_vote/can_propose; hash random keys, show the secret only at issuance, reject revoked keys, and keep secrets out of logs.
- Authorize reviewers as humans allowed to review the post: the human author, or an explicitly defined owner rule for an agent-authored post. Finalize that rule; do not grant every human review permission.
- Lock the post/proposal in a consistent order during review. Check pending state and the current revision against base_revision_no. A valid approval creates the next revision, copies approved sources as designed, records result_revision_no/reviewer/time/status, and writes audit history in one transaction. Rejection creates no revision. Define whether a stale state is committed with a conflict result; do not accidentally roll it back while claiming it was recorded.
- The ER's optional 1:1 RESULTS_IN relation needs an appropriate uniqueness rule on non-null result revision pairs if implemented literally. The source diagrams do not show all enforcement details.
- Use one acquired connection for each logical transaction. Decide whether the review transaction belongs to the application or an approval stored procedure; use one transaction owner rather than nesting competing begin/commit logic. Views, triggers, a review procedure, FULLTEXT and EXPLAIN are prior project ideas, not additional professor mandates established by the announcement.
- Audit events for committed operations belong to their transaction. A rolled-back operation's audit insert rolls back too; failed-call diagnostics must remain available in safe application logs. Do not promise durable failure audit rows inside an aborted transaction.

## Normalization review before final claims

The slides claim BCNF for all 14 tables. Preserve that as a source claim, not a fresh verification result. Candidate-key claims include actor.handle, human_user.email, api_key.key_hash, post.slug, and tag.name, under the stated uniqueness/nullability assumptions.

Review these issues before final report/DDL:

1. The slides simplify 2NF using only the primary key; the formal reasoning must consider all candidate keys. BCNF requires every nontrivial determinant to be a superkey.
2. The POST_TAG_V example with tag_id -> tag_name also violates 2NF when its key is (post_id, tag_id); it is not evidence of a relation that satisfies 3NF but fails BCNF.
3. The reply same-post rule can introduce a conditional dependency involving parent_comment_id and post_id. The complete report's referenced comment discussion is missing; examine the actual dependencies and nullable-root semantics rather than certifying BCNF from the slide summary.
4. A cycle of FK relationships does not automatically violate 3NF. Here the based-on composite FK already carries post_id, so the direct conceptual edge can be omitted without asserting a universal normalization rule.
5. JSON or another rich domain does not automatically make every schema non-1NF. Explain the atomicity and facts of this actual model; retain the chosen separate permission columns without repeating categorical claims from the old chat.
6. Slide notes refer to 19 relationship sets; the SVG has 18 named relationship diamonds plus ISA. State the counting convention consistently.

## Five proposed final-evaluation functions

The professor requires five meaningful reusable methods; these revised choices fit the recovered model. Supporting registration, authentication, key management, reading/search, and direct-author revision operations are still required product work.

| Method | Logical operation | Evidence |
| --- | --- | --- |
| `publishPost` | Authenticated actor publishes post + revision 1 + sources + tags + audit | Late source/tag failure leaves no partial publication |
| `addComment` | Authenticated actor adds a comment/reply with provenance and audit | Cross-post parent fails; audit-write failure rolls back the comment |
| `castVote` | Insert/change/remove a post or comment vote in the correct typed table, plus audit | Unique actor/target behavior, FK failures, audit rollback, correct derived totals |
| `submitEditProposal` | Actor submits suggested content against an existing base revision, plus audit | Scope/base validation and late failure leave no incomplete proposal |
| `reviewEditProposal` | Authorized human approves/rejects or records stale state; approved content becomes a revision with provenance and review attribution | Two concurrent reviews cannot create duplicate results; late audit failure rolls back approval and revision |

These methods are planned, not implemented. Do not count a browser simulation as evidence of SQL correctness. Follow [the user-run checklist](../testing/manual-checklist.md) for eventual verification.
