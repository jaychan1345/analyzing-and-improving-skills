# Architecture Decisions

## Keep one Skill when

- The work has one trigger and one independently accepted outcome.
- Steps share the same inputs, approval boundary, and failure contract.

## Split Skills when

- Stages can trigger independently.
- Different owners or approval gates apply.
- One stage can fail or be released without the others.
- The original Skill mixes orchestration with specialist work.

## Add a reference when

Detailed rules or templates exceed the core workflow and are loaded only in specific cases.

## Add a script when

The operation is deterministic, repeated, testable, and safer in code than model judgment. Define input, output, exit behavior, dependencies, and a runnable test before approving it.

## Naming

Use a new lowercase hyphenated name. For a personal branch, append a distinct owner marker and record source version, owner, personal rules, and scope. Never reuse the central name for a divergent branch.
