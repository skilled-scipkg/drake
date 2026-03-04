---
name: drake-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Examples and Tutorials

## High-Signal Playbook
### Route Conditions
- Use this skill for runnable demos, notebook-driven exploration, and "show me a working baseline" requests.
- Route to `drake-inputs-and-modeling` for model-authoring decisions.
- Route to `drake-simulation-workflows` for integrator/contact runtime tuning.
- Route to `drake-api-and-scripting` for Python binding semantics.

### Triage Questions
- Is the user asking for C++ examples, Python tutorials, or both?
- Which behavior is needed first: control, contact, visualization, or optimization?
- Should the run be headless or visualized (Meldis/MeshCat)?
- Is reproducibility required (fixed flags/seeds, saved outputs)?

### Canonical Workflow
1. Start from one known-good README (`examples/acrobot/README.md`, `examples/quadrotor/README.md`, `examples/hydroelastic/ball_plate/README.md`).
2. Launch visualizer first if required by the example docs.
3. Run the default command before modifying flags.
4. Adjust one parameter group at a time (controller gains, contact model, realtime rate).
5. Validate behavior against corresponding tests in `examples/**/test` or tutorial checks.

### Minimal Working Example
```bash
bazel run //tools:meldis -- --open-window &
bazel run //examples/acrobot:run_swing_up
bazel run //examples/quadrotor:run_quadrotor_lqr
python3 -m pydrake.tutorials
```

### Pitfalls and Fixes
- Starting from a custom model before validating a stock example slows debugging.
- For hydroelastic demos, contact model and contact surface representation flags strongly affect behavior (`examples/hydroelastic/ball_plate/README.md`).
- Some demos rely on optional solvers/dependencies (for example SNOPT in specific acrobot trajectories).
- Notebook launches can fail when environment variables and Python env are mismatched (`tutorials/README.md`).

### Convergence and Validation Checks
- At least one C++ example and one Python tutorial run successfully.
- Visualization appears and updates at expected rates.
- Related `examples/**/test` checks for the chosen example pass or are logically consistent.

### Source-Code Handoff
- Acrobot behavior: `examples/acrobot/run_swing_up.cc`, `examples/acrobot/spong_sim.cc`.
- Quadrotor behavior: `examples/quadrotor/run_quadrotor_lqr.cc`, `examples/quadrotor/quadrotor_plant.cc`.
- Hydroelastic demo assembly: `examples/hydroelastic/ball_plate/ball_plate_run_dynamics.cc`, `examples/hydroelastic/ball_plate/make_ball_plate_plant.cc`.
- Notebook launcher path: `bindings/pydrake/tutorials.py`, `tools/jupyter/jupyter_bazel.py`.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Prefer runnable command paths over abstract explanations.

## Primary documentation references
- `tutorials/README.md`
- `examples/acrobot/README.md`
- `examples/quadrotor/README.md`
- `examples/hydroelastic/ball_plate/README.md`
- `examples/kuka_iiwa_arm/README.md`
- `examples/hardware_sim/README.md`
- `tools/jupyter/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use example/test source files for behavior verification.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `examples/**/test`
- `tutorials/test`
- `bindings/pydrake/examples/test`

## Optional deeper inspection
- `examples`
- `tutorials`
- `bindings/pydrake`
- `systems`
- `multibody`

## Source entry points for unresolved issues
- `examples/acrobot/run_swing_up.cc`
- `examples/acrobot/spong_sim.cc`
- `examples/quadrotor/run_quadrotor_lqr.cc`
- `examples/quadrotor/quadrotor_plant.cc`
- `examples/hydroelastic/ball_plate/ball_plate_run_dynamics.cc`
- `examples/hydroelastic/ball_plate/make_ball_plate_plant.cc`
- `bindings/pydrake/tutorials.py`
- `tools/jupyter/jupyter_bazel.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" examples tutorials bindings/pydrake`).
