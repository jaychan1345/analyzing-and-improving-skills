# Test Matrix

| Layer | Required cases |
|---|---|
| Trigger | explicit, implied, should-not-trigger, adjacent conflict, orchestrator boundary |
| Function | normal input and all required outputs |
| Missing | missing file, field, dependency, permission, approval |
| Abnormal | malformed, conflicting, empty, duplicate, unsupported |
| Contract | output order, fields, format, traceability, multi-output consistency |
| Repeatability | same input twice, no hidden state or source mutation |
| Regression | preserved behavior plus every approved change |
| Portability | clean conversation, new user, relative paths, no local-only assumptions |

For scripts, test the documented command, input, output, exit code, dependency failure, and invalid input. If execution is impossible, mark each affected case `not-run` or `blocked`; do not substitute static review.
