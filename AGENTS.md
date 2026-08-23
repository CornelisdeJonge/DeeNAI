# Project Development Instructions

## Project context

This repository is a Rust workspace. 
The project plan is in `plans/project-plan.json`, 
and the current development state is in `plans/development-state.json`.

Read both files before proposing implementation work.

## Architecture

- `crates/app` contains application orchestration and entry points.
- `crates/core` contains domain logic and must remain independent of infrastructure.
- `crates/infrastructure` contains external systems and implementation details.
- Integration tests belong in the appropriate crate or `tests/integration`.

## Application structure metadata

`plans/application-structure.json` describes the current Rust application structure.

Before adding or modifying a type, method, field, function, module, or public API:

1. Check whether an existing symbol already serves the purpose.
2. Follow the naming rules in the structure file.
3. Preserve documented invariants.
4. Keep dependency direction consistent with the workspace rules.
5. Update the structure file when the source structure changes.

Use the summaries and invariants in the structure file when generating Rust documentation comments. Do not generate comments that claim behavior not represented by the source code or tests.

## Development rules

- Work on one primary goal at a time.
- Check the goal's acceptance criteria before writing code.
- Prefer the smallest implementation that satisfies the current goal.
- Do not add unrelated features or refactor unrelated code.
- Record newly discovered work in `development-state.json`.
- Defer nonessential ideas to the backlog.
- Update the plan when scope, architecture, or priorities change.
- Add tests with behavior changes.
- Do not add dependencies without recording their purpose.

## Required verification

Before marking work complete, run:

```bash
cargo fmt --all
cargo check --workspace
cargo test --workspace
cargo clippy --workspace --all-targets --all-features -- -D warnings
