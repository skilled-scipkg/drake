---
name: drake-simulation-workflows
description: This skill should be used when users ask about simulation workflows in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Simulation Workflows

## High-Signal Playbook
### Route Conditions
- Use this skill for end-to-end run loops: diagram/system composition, simulator stepping, integrator/contact controls, and output/replay.
- Route to `drake-inputs-and-modeling` for model parsing/composition questions before runtime.
- Route to `drake-api-and-scripting` for Python-specific API ergonomics.
- Route to `drake-troubleshooting` when convergence/runtime failures dominate.

### Triage Questions
- Which example or system is closest to the user goal (acrobot, hydroelastic, deformable, iiwa)?
- Is the plant continuous/discrete, and what time-step policy is desired?
- Which contact model and surface representation are being used?
- Is visualization through Meldis or in-process MeshCat required?
- What outputs are needed (YAML/log files, benchmark output directories, recordings)?
- Is reproducibility needed across runs or machines?

### Canonical Workflow
1. Start from a known runnable example (`examples/acrobot/README.md`, `examples/hydroelastic/ball_plate/README.md`, `examples/multibody/deformable/README.md`).
2. Launch the recommended visualizer path first (Meldis or MeshCat per example docs).
3. Run with default settings, then inspect `--help` options for controlled parameter sweeps.
4. Adjust one dominant runtime knob at a time: step size, realtime rate, contact model, or contact surface representation.
5. Capture outputs using built-in paths (`--output_dir` for benchmarking, YAML output in acrobot stochastic example).
6. For replay workflows, use MeshCat recording/publish path noted in spatula example docs.

### Minimal Working Example
```bash
# examples/acrobot/README.md + examples/hydroelastic/ball_plate/README.md
bazel run //tools:meldis -- --open-window &
bazel run //examples/acrobot:run_swing_up
bazel run //examples/hydroelastic/ball_plate:ball_plate_run_dynamics \
  -- --simulator_target_realtime_rate=0.01

# multibody/benchmarking/README.md
bazel run //multibody/benchmarking:cassie_experiment -- --output_dir=trial1
```

### Pitfalls and Fixes
- Using `triangle` contact surfaces can trigger convergence failures; reduce `--mbp_discrete_update_period` when needed (`examples/hydroelastic/spatula_slip_control/README.md`).
- Switching to point contact can show unphysical oscillations in some scenarios; compare hydroelastic vs point intentionally (`examples/hydroelastic/ball_plate/README.md`).
- Some demos require specific backends for full playback (MeshCat recording in spatula example), not just Meldis (`examples/hydroelastic/spatula_slip_control/README.md`).
- `run_swing_up_traj_optimization` requires SNOPT and will fail without it (`examples/acrobot/README.md`).
- Benchmark comparisons are machine-dependent; only compare runs from the same machine/environment (`multibody/benchmarking/README.md`).

### Convergence and Validation Checks
- Re-run with modest step-size changes and check that qualitative behavior is consistent.
- Verify contact-model-sensitive behaviors persist across repeated runs.
- Confirm benchmark output files are produced and tagged to the right environment.
- Validate visualization path (Meldis vs MeshCat playback) matches the example.

### Source-Code Handoff
- Simulation/integrator internals: `systems/primitives/discrete_time_integrator.h`, `systems/analysis/runge_kutta3_integrator.h`, `systems/analysis/runge_kutta5_integrator.h`.
- FEM stepping: `multibody/fem/discrete_time_integrator.h`, `multibody/fem/discrete_time_integrator.cc`.
- Example runtime assembly: `examples/hydroelastic/spatula_slip_control/spatula_slip_control.cc`, `multibody/benchmarking/acrobot.cc`.
- iiwa control composition: `manipulation/kuka_iiwa/build_iiwa_control.h`, `manipulation/kuka_iiwa/build_iiwa_control.cc`.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `multibody/benchmarking/README.md`
- `examples/kuka_iiwa_arm/README.md`
- `examples/acrobot/README.md`
- `examples/rod2d/README.md`
- `examples/hydroelastic/ball_plate/README.md`
- `examples/multibody/rolling_sphere/README.md`
- `examples/multibody/deformable/README.md`
- `examples/hydroelastic/spatula_slip_control/README.md`
- `examples/hydroelastic/python_nonconvex_mesh/README.md`
- `examples/hydroelastic/python_ball_paddle/README.md`
- `tools/jupyter/README.md`
- `tutorials/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `examples`
- `manipulation`
- `multibody`
- `systems`
- `tools`
- `common/test`
- `geometry/test`
- `lcm/test`
- `lcmtypes/test`
- `math/test`
- `perception/test`
- `planning/test`
- `solvers/test`
- `tutorials/test`
- `visualization/test`
- `bindings/pydrake/test`
- `doc/doxygen_cxx/test`

## Optional deeper inspection
- `bindings`
- `cmake`
- `common`
- `examples`
- `geometry`
- `lcm`
- `lcmtypes`
- `manipulation`
- `math`
- `multibody`
- `perception`
- `planning`
- `solvers`
- `systems`
- `tools`
- `tutorials`
- `visualization`

## Source entry points for unresolved issues
- `examples/hydroelastic/spatula_slip_control/spatula_slip_control.cc`
- `bindings/pydrake/multibody/run_installed_mesh_to_model.py`
- `systems/primitives/discrete_time_integrator.h`
- `systems/primitives/discrete_time_integrator.cc`
- `multibody/fem/discrete_time_integrator.h`
- `multibody/fem/discrete_time_integrator.cc`
- `multibody/benchmarking/iiwa_relaxed_pos_ik.cc`
- `multibody/benchmarking/acrobot.cc`
- `systems/analysis/runge_kutta3_integrator.h`
- `systems/analysis/runge_kutta5_integrator.h`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).
