# Design and context change log

## Recovered baseline

The correct user-supplied blogging context is organized under `diagrams/`, `docs/context/sources/` and `docs/presentation/midsem/`. The Chen ER, 14-table schema, 20-slide mid-semester deck, team guide and 33-page chat retain their original content; the manifest records old/current paths and hashes. Use [baseline.md](baseline.md) and [source review](../context/blogging-source-review.md). File presence does not prove which revision the professor received; retain the actual submitted snapshot when identified.

## Records

| ID | Earlier state | Current decision | Reason and status |
| --- | --- | --- | --- |
| DC-001 | Inventory files treated as the active assignment | Confirmed allotted blogging topic | Context correction; unrelated working files subsequently removed, committed versions remain in Git history |
| DC-002 | Nine-table blogging proposal with ACCOUNT/HUMAN_PROFILE/AGENT_PROFILE/MODERATION_ACTION | Supplied 14-table actor-based model | Correct artifacts now available; obsolete proposal removed, earlier committed version recoverable; no implemented data migration exists |
| DC-003 | Document-database proposal | MySQL/InnoDB + readable mysql2 SQL; React TSX/Tailwind + Node/Express TypeScript | Latest user choices; old vanilla/no-TypeScript advice is historical |
| DC-004 | Human author selector and owner posting on behalf of agents | Human sessions and independent agent API-key clients resolve to actor_id | Matches recovered workflow; ownership/key management remains, impersonation is not a required UI feature |
| DC-005 | Evaluated methods emphasized registration/direct revision/moderation | publishPost, addComment, castVote, submitEditProposal, reviewEditProposal | Better demonstrates recovered co-writing/vote/provenance model; these are proposed choices, not professor-mandated names |
| DC-006 | Flat supplied context folder, unrelated inventory files, competing historical proposal | Purpose-based sources/diagrams/presentation layout and meaningful implementation guides | User explicitly requested cleanup; seven original artifact hashes unchanged, obsolete files removed without rewriting Git history; no schema behavior change |

## Pending technical decisions

Resolve source-target XOR, actor subtype enforcement, same-post comments, result-revision uniqueness, human reviewer policy, stale-state semantics, transaction ownership and audit guarantees. Recheck the slides' normalization claims and relationship count. Views, triggers, approval procedure, FULLTEXT and indexing evidence are source ideas to prioritize deliberately; do not claim they already exist.

For each actual implementation deviation record before/after, technical reason, normalization and data/schema impact, affected diagrams/code/docs, and validation. Preserve the baseline files and distinguish a correction to repository understanding from an approved change to a submitted diagram. Add professor feedback only if actually received. No professor approval or formal approval process is invented.
