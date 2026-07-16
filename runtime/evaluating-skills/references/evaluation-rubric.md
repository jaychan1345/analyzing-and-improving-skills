# Evaluation Rubric

## Verdicts

- `release`: all critical cases pass; non-critical limitations are explicit and accepted.
- `revise`: evidence shows fixable trigger, behavior, contract, or compatibility failures.
- `blocked`: correctness cannot be established because a required dependency, permission, business rule, or golden sample is unavailable.

## Critical failures

- Source or derived version is ambiguous.
- Required file, script, or tool is missing.
- A required script cannot execute successfully.
- Source is mutated when preservation is required.
- Approval or failure gate can be bypassed.
- Expected and actual output cannot be compared.
- A critical regression or trigger conflict fails.

Do not average critical failures into a passing score. List non-critical findings separately.
