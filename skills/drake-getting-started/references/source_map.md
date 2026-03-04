# drake source map: Getting Started

Generated from source roots:
- `.`
- `bindings/pydrake`
- `multibody/contact_solvers/icf`
- `tools/workspace`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" MODULE.bazel tools/workspace bindings/pydrake multibody/contact_solvers/icf`
- `rg -n "icf|solver|builder|import|workspace" bindings/pydrake multibody/contact_solvers/icf tools/workspace`
- Start with the high-level entry module and then drill into the specific subsystem implementation.

## Implementation entry points
- `MODULE.bazel` | repo-level dependency/module starting point.
- `tools/workspace/default.bzl` | default external dependency loading path.
- `bindings/pydrake/__init__.py` | top-level Python package entrypoint.
- `bindings/pydrake/systems/__init__.py` | systems package entrypoint.
- `bindings/generated_docstrings/multibody_contact_solvers_icf.h` | generated docstrings for ICF bindings.
- `multibody/contact_solvers/icf/icf_solver.h` | ICF solver API.
- `multibody/contact_solvers/icf/icf_solver_parameters.h` | ICF solver parameter API.
- `multibody/contact_solvers/icf/icf_solver.cc` | ICF solver implementation.
- `multibody/contact_solvers/icf/icf_model.h` | ICF model API.
- `multibody/contact_solvers/icf/icf_model.cc` | ICF model implementation.
- `multibody/contact_solvers/icf/icf_builder.h` | ICF builder API.
- `multibody/contact_solvers/icf/icf_builder.cc` | ICF builder implementation.

## Function-level behavior checks
- `bindings/pydrake/test/all_install_test.py` | validates package install import behavior.
- `bindings/pydrake/systems/test/analysis_test.py` | validates simulator-related Python behavior.
- `multibody/contact_solvers/icf/test/icf_solver_test.cc` | validates ICF solver behavior.
- `multibody/contact_solvers/icf/test/icf_model_test.cc` | validates ICF model invariants.
- `multibody/contact_solvers/icf/test/icf_builder_test.cc` | validates problem assembly behavior.
- `multibody/contact_solvers/icf/test/two_spheres_test.cc` | validates contact benchmark-style scenario behavior.
