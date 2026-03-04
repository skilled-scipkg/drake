# drake source map: Multibody

Generated from source roots:
- `multibody/plant`
- `multibody/tree`
- `multibody/parsing`
- `multibody/inverse_kinematics`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" multibody/plant multibody/tree multibody/parsing multibody/inverse_kinematics`
- `rg -n "contact|solver|joint|tree|kinematics|Finalize" multibody/plant multibody/tree multibody/inverse_kinematics`
- Pair implementation reads with nearest tests before changing behavior assumptions.

## Implementation entry points
- `multibody/plant/multibody_plant.h` | plant API surface.
- `multibody/plant/multibody_plant.cc` | plant core implementation.
- `multibody/plant/sap_driver.h` | SAP contact driver API.
- `multibody/plant/sap_driver.cc` | SAP contact driver implementation.
- `multibody/plant/tamsi_solver.h` | TAMSI solver API.
- `multibody/plant/tamsi_solver.cc` | TAMSI solver implementation.
- `multibody/tree/multibody_tree.h` | multibody tree API and invariants.
- `multibody/tree/multibody_tree.cc` | multibody tree implementation.
- `multibody/parsing/parser.cc` | parser integration path.
- `multibody/inverse_kinematics/inverse_kinematics.cc` | IK implementation path.

## Function-level behavior checks
- `multibody/plant/test/multibody_plant_test.cc` | validates core plant behavior.
- `multibody/plant/test/sap_driver_test.cc` | validates SAP driver behavior.
- `multibody/plant/test/tamsi_solver_test.cc` | validates TAMSI solver behavior.
- `multibody/tree/test/multibody_tree_test.cc` | validates tree structure and dynamics behavior.
- `multibody/parsing/test/parser_test.cc` | validates parser behavior against fixtures.
- `multibody/inverse_kinematics/test/inverse_kinematics_test.cc` | validates IK constraints and solver behavior.
