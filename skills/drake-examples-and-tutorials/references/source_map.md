# drake source map: Examples and Tutorials

Generated from source roots:
- `examples`
- `tutorials`
- `bindings/pydrake`
- `tools/jupyter`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" examples tutorials bindings/pydrake tools/jupyter`
- `rg -n "run_|main|Simulator|Diagram|Parser" examples tutorials bindings/pydrake`
- For behavior questions, inspect both example implementation and its corresponding `examples/**/test` file.

## Implementation entry points
- `examples/acrobot/run_swing_up.cc` | canonical control + simulation example loop.
- `examples/acrobot/spong_sim.cc` | schema-driven stochastic simulation flow.
- `examples/quadrotor/run_quadrotor_lqr.cc` | controller-driven quadrotor workflow.
- `examples/quadrotor/quadrotor_plant.cc` | quadrotor dynamics implementation.
- `examples/hydroelastic/ball_plate/ball_plate_run_dynamics.cc` | hydroelastic runtime assembly.
- `examples/hydroelastic/ball_plate/make_ball_plate_plant.cc` | plant/model builder for hydroelastic demo.
- `bindings/pydrake/tutorials.py` | tutorial launcher wiring.
- `tools/jupyter/jupyter_bazel.py` | Bazel-backed Jupyter startup integration.

## Function-level behavior checks
- `examples/acrobot/test/acrobot_plant_test.cc` | validates acrobot dynamics/plant behavior.
- `examples/acrobot/test/spong_sim_main_test.py` | validates stochastic scenario pipeline.
- `examples/quadrotor/test/quadrotor_dynamics_test.cc` | validates quadrotor dynamics behavior.
- `examples/quadrotor/test/quadrotor_plant_test.cc` | validates quadrotor plant semantics.
- `examples/rod2d/test/constraint_solver_test.cc` | validates constrained simulation behavior.
- `tutorials/test/notebook_lint_test.py` | validates tutorial notebook execution hygiene.
- `bindings/pydrake/examples/test/acrobot_test.py` | validates Python example wrapper behavior.
