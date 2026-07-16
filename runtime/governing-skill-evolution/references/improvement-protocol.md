# Improvement Protocol

## Central-entry criteria

All conditions are required:

1. The issue appears in at least two distinct cases, or is a high-risk defect.
2. The change measurably reduces omissions, false decisions, unsafe behavior, or repeated work.
3. It does not impose unjustified context cost on all users.
4. At least one regression fails on the old version and passes on the candidate.
5. A designated maintainer approves the exact proposal and target version.

## Lifecycle

`observed → proposed → under-review → approved → implemented → evaluated → released`

Rejected proposals become `rejected` with reason. Unavailable evidence stays `proposed` or `blocked`; it does not become approval through time or urgency.

Retain the prior central version for rollback. Rollback restores a known version; it does not erase the failed case or regression evidence.
