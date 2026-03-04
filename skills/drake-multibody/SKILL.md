---
name: drake-multibody
description: This skill should be used when users ask about multibody in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Multibody

## High-Signal Playbook
### Route Conditions
- Use this skill for multibody internals: plant dynamics, contact solvers, kinematics, and inverse-kinematics behavior.
- Route to `drake-inputs-and-modeling` for model authoring/parsing workflow setup.
- Route to `drake-simulation-workflows` for run-loop/integrator controls.

### Triage Questions
- Is the question about parsing, plant state evolution, contact solving, or IK?
- Is the system continuous or discrete (`time_step` choice)?
- Which contact path is active (SAP, TAMSI, ICF/CENIC-related)?
- Are we validating via example behavior, numeric checks, or unit tests?

### Canonical Workflow
1. Start from multibody docs (`README_model_directives.md`, `contact_solvers/icf/README.md`, `multibody/benchmarking/README.md`).
2. Validate baseline behavior with a known multibody example.
3. Identify subsystem (parsing, tree, plant, contact, IK) before source dive.
4. Inspect paired implementation + tests from `references/source_map.md`.
5. Make one numerical/configuration change at a time and re-validate.

### Minimal Working Example
```bash
bazel run //examples/multibody/four_bar:passive_simulation -- --initial_velocity=1.0
bazel run //multibody/benchmarking:cassie_experiment -- --output_dir=trial1
```

### Pitfalls and Fixes
- Calling `Finalize()` too early blocks later model composition changes.
- Contact model assumptions (SAP/TAMSI/ICF) can invalidate expected dynamics if mixed unintentionally.
- IK behavior is sensitive to constraint scaling and initialization; validate with test analogs before broad tuning.

### Convergence and Validation Checks
- Multibody example behavior remains stable under small step-size changes.
- Relevant plant/contact/IK tests align with observed behavior.
- Benchmarks or diagnostics are compared within the same environment.

### Source-Code Handoff
- Plant core: `multibody/plant/multibody_plant.h`, `multibody/plant/multibody_plant.cc`.
- Contact drivers: `multibody/plant/sap_driver.h`, `multibody/plant/sap_driver.cc`, `multibody/plant/tamsi_solver.h`, `multibody/plant/tamsi_solver.cc`.
- Tree internals: `multibody/tree/multibody_tree.h`, `multibody/tree/multibody_tree.cc`.
- Parsing + IK internals: `multibody/parsing/parser.cc`, `multibody/inverse_kinematics/inverse_kinematics.cc`.

## Scope
- Handle questions about multibody dynamics and related internals.
- Keep guidance behavior-oriented with concrete validation hooks.

## Primary documentation references
- `multibody/parsing/README_model_directives.md`
- `multibody/models/README.md`
- `multibody/contact_solvers/icf/README.md`
- `multibody/benchmarking/README.md`
- `multibody/plant/images/README.md`
- `examples/multibody/four_bar/README.md`
- `examples/multibody/strandbeest/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `multibody/plant/test`
- `multibody/tree/test`
- `multibody/parsing/test`
- `multibody/inverse_kinematics/test`

## Optional deeper inspection
- `multibody`
- `systems`
- `geometry`
- `solvers`
- `bindings/pydrake/multibody`

## Source entry points for unresolved issues
- `multibody/plant/multibody_plant.h`
- `multibody/plant/multibody_plant.cc`
- `multibody/plant/sap_driver.h`
- `multibody/plant/sap_driver.cc`
- `multibody/plant/tamsi_solver.h`
- `multibody/plant/tamsi_solver.cc`
- `multibody/tree/multibody_tree.h`
- `multibody/tree/multibody_tree.cc`
- `multibody/parsing/parser.cc`
- `multibody/inverse_kinematics/inverse_kinematics.cc`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" multibody systems geometry solvers`).
