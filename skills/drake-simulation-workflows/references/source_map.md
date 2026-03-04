# drake source map: Simulation Workflows

Generated from source roots:
- `examples`
- `systems/analysis`
- `systems/primitives`
- `multibody/fem`
- `multibody/benchmarking`
- `multibody/plant`
- `manipulation/kuka_iiwa`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" examples systems/analysis systems/primitives multibody/fem multibody/benchmarking multibody/plant manipulation/kuka_iiwa`
- `rg -n "Simulator|integrator|time_step|contact|run_|output" examples systems multibody manipulation`
- Pair runtime issues with nearest test coverage before changing integrator/contact settings.

## Implementation entry points
- `examples/hydroelastic/spatula_slip_control/spatula_slip_control.cc` | hydroelastic runtime assembly and controls.
- `bindings/pydrake/multibody/run_installed_mesh_to_model.py` | installed mesh-to-model script used in simulation pipelines.
- `multibody/benchmarking/acrobot.cc` | benchmark simulation path for multibody dynamics.
- `multibody/benchmarking/iiwa_relaxed_pos_ik.cc` | optimization-heavy runtime benchmark path.
- `manipulation/kuka_iiwa/build_iiwa_control.cc` | iiwa control diagram composition.
- `systems/analysis/simulator.cc` | simulator stepping/event execution core.
- `systems/primitives/discrete_time_integrator.h` | discrete-time integrator API.
- `systems/primitives/discrete_time_integrator.cc` | discrete-time integrator implementation.
- `systems/analysis/runge_kutta3_integrator.h` | RK3 integrator behavior anchor.
- `systems/analysis/runge_kutta5_integrator.h` | RK5 integrator behavior anchor.
- `multibody/fem/discrete_time_integrator.h` | FEM discrete-time integrator API.
- `multibody/fem/discrete_time_integrator.cc` | FEM-specific time integration path.

## Function-level behavior checks
- `systems/primitives/test/discrete_time_integrator_test.cc` | validates discrete-time integration behavior.
- `systems/primitives/test/discrete_time_delay_test.cc` | validates discrete-time signal delay behavior.
- `systems/analysis/test/runge_kutta3_integrator_test.cc` | validates RK3 behavior.
- `systems/analysis/test/initial_value_problem_test.cc` | validates IVP stepping semantics.
- `examples/acrobot/test/acrobot_plant_test.cc` | validates example plant dynamics behavior.
- `examples/rod2d/test/constraint_solver_test.cc` | validates constrained simulation behavior.
- `multibody/plant/test/discrete_step_memory_test.cc` | validates discrete-step state bookkeeping.
