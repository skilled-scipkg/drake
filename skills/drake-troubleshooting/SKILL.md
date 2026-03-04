---
name: drake-troubleshooting
description: This skill should be used when users ask about troubleshooting in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Troubleshooting

## High-Signal Playbook
### Route Conditions
- Use this skill for reproducible failures, diagnostics strategy, and "why does this run fail" requests.
- Route to topic skills (`build-and-install`, `inputs-and-modeling`, `simulation-workflows`, `api-and-scripting`) after failure class is identified.

### Triage Questions
- What exact command failed, and what is the full error output?
- Which platform/toolchain/Python env is in use?
- Is failure at parse/build/import/runtime/solver-convergence stage?
- Can the issue be reproduced on a stock Drake example first?

### Canonical Workflow
1. Capture environment and command metadata from `doc/_pages/getting_help.md`.
2. Reproduce with smallest runnable command.
3. Map failure signature to known pages (`troubleshooting.md`, `issues.md`).
4. Confirm expected behavior with targeted tests.
5. Escalate to source-level error handling and debug helpers when docs + tests are insufficient.

### Minimal Working Example
```bash
python3 --version
bazel version
git rev-parse --short HEAD
python3 -c 'import pydrake; print("pydrake import ok")'
bazel run //examples/acrobot:run_passive
```

### Pitfalls and Fixes
- Missing environment metadata creates low-signal bug reports (`doc/_pages/getting_help.md`).
- Using `Plant` context directly instead of diagram-owned context causes frequent framework errors (`doc/_pages/troubleshooting.md`).
- Parsing failures are often model-format or resource-resolution issues; validate model path and parser compatibility first.

### Convergence and Validation Checks
- A minimal reproducer exists and is version-pinned.
- At least one related regression test path has been checked.
- Proposed fix removes the error without introducing new failures in adjacent tests.

### Source-Code Handoff
- Assertion/error surfaces: `common/drake_assertion_error.h`, `solvers/csdp_solver_error_handling.h`, `solvers/csdp_solver_error_handling.cc`.
- IVP/runtime diagnostics: `systems/analysis/initial_value_problem.h`, `systems/analysis/initial_value_problem.cc`, `systems/analysis/scalar_initial_value_problem.h`, `systems/analysis/scalar_initial_value_problem.cc`.
- Multibody debug scaffolding: `multibody/topology/spanning_forest_debug.cc`, `multibody/topology/link_joint_graph_debug.cc`, `multibody/contact_solvers/sap/sap_contact_problem.cc`.

## Scope
- Handle questions about known issues, diagnostics, and debugging patterns.
- Focus on reproducibility first, then root-cause analysis.

## Primary documentation references
- `doc/_pages/troubleshooting.md`
- `doc/_pages/getting_help.md`
- `doc/_pages/no_push_to_origin.md`
- `doc/_pages/issues.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use nearby tests as expected-behavior anchors.
- If ambiguity remains after docs/tests, inspect `references/source_map.md` and start with the ranked source entry points.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `common/test`
- `systems/analysis/test`
- `solvers/test`
- `multibody/plant/test`

## Optional deeper inspection
- `common`
- `systems/analysis`
- `solvers`
- `multibody`
- `tools`

## Source entry points for unresolved issues
- `common/drake_assertion_error.h`
- `solvers/csdp_solver_error_handling.h`
- `solvers/csdp_solver_error_handling.cc`
- `systems/analysis/initial_value_problem.h`
- `systems/analysis/initial_value_problem.cc`
- `systems/analysis/scalar_initial_value_problem.h`
- `systems/analysis/scalar_initial_value_problem.cc`
- `multibody/topology/spanning_forest_debug.cc`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" common systems/analysis solvers multibody`).
