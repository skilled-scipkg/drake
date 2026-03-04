# drake source map: Troubleshooting

Generated from source roots:
- `common`
- `systems/analysis`
- `solvers`
- `multibody`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" common systems/analysis solvers multibody`
- `rg -n "error|assert|problem|debug|exception|failure" common systems/analysis solvers multibody`
- For each failure signature, inspect implementation and closest regression test together.

## Implementation entry points
- `common/drake_assertion_error.h` | assertion error type surfaced to users.
- `solvers/csdp_solver_error_handling.h` | CSDP error handling API.
- `solvers/csdp_solver_error_handling.cc` | CSDP error handling implementation.
- `systems/analysis/initial_value_problem.h` | IVP API used by simulators/integrators.
- `systems/analysis/initial_value_problem.cc` | IVP implementation.
- `systems/analysis/scalar_initial_value_problem.h` | scalar IVP API.
- `systems/analysis/scalar_initial_value_problem.cc` | scalar IVP implementation.
- `multibody/topology/spanning_forest_debug.cc` | multibody topology debug support.
- `multibody/topology/link_joint_graph_debug.cc` | link-joint graph debug support.
- `multibody/contact_solvers/sap/sap_contact_problem.cc` | contact problem construction path.

## Function-level behavior checks
- `common/test/drake_assert_test.cc` | validates assertion failure semantics.
- `solvers/test/csdp_solver_test.cc` | validates solver behavior around CSDP integration.
- `systems/analysis/test/initial_value_problem_test.cc` | validates IVP behavior.
- `systems/analysis/test/discrete_time_approximation_test.cc` | validates discrete approximation behavior.
- `multibody/plant/test/calc_distance_and_time_derivative_test.cc` | validates multibody runtime derivative behavior.
