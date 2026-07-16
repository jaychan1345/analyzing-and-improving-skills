# Analysis Framework

Analyze in this order:

1. **Source inventory:** supplied files, file tree, referenced paths, missing dependencies.
2. **Purpose and audience:** core objective, target user, out-of-scope work.
3. **Trigger boundary:** explicit, implied, prohibited, adjacent conflicts.
4. **Inputs:** required, optional, inferable, system-fetched; format and missing behavior.
5. **State model:** entry condition, action, product, failure handling, next state.
6. **Rules:** general, domain, configurable, and prohibited; priority and conflicts.
7. **Knowledge and dependencies:** references, scripts, assets, agents metadata, external tools, permissions.
8. **Responsibility split:** model judgment versus deterministic code.
9. **Output contract:** deliverables, order, format, traceability, cross-deliverable consistency.
10. **Failure contract:** abnormal inputs, degradation, stop conditions, permission blocks.
11. **Acceptance:** definition of done and verifiable evidence.
12. **Findings:** facts, inferences, issues, and opportunities in separate sections.

For each workflow step, record: input, precondition, action, output, decision, failure, and next state.
