# Change Classification

| Class | Meaning | Required evidence |
|---|---|---|
| Preserve | Existing behavior remains valid | Source fact and unchanged acceptance case |
| Modify | Existing behavior remains but its contract changes | Old behavior, new requirement, migration impact |
| Add | New behavior has no current equivalent | Requirement source and new acceptance case |
| Delete | Existing behavior is obsolete, conflicting, or unsafe | Removal reason and compatibility impact |
| Split | One responsibility becomes independently triggered/tested units | Boundary, handoff contract, trigger conflict analysis |

Every row records: item, current evidence, proposed change, reason, affected files, risk, and test ID.

Do not classify missing source content as a deletion. It is an unresolved dependency.
