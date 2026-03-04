---
name: drake-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Inputs and Modeling

## High-Signal Playbook
### Route Conditions
- Use this skill for model construction/parsing, multibody setup, geometry attachment, and input parameterization.
- Route to `drake-simulation-workflows` for stepping/integration/runtime control details.
- Route to `drake-api-and-scripting` when the user needs Python binding call patterns.
- Route to `drake-troubleshooting` for persistent parse/runtime failure handling.

### Triage Questions
- Are models authored in URDF, SDFormat, or Model Directives YAML?
- Is this a single-model plant or a composed scene of many models?
- Do you need `SceneGraph` geometry and contact setup now, or later?
- Are there closed-chain or compliance requirements (bushings, constraints)?
- Which parameters are being tuned first (stiffness, damping, friction, mass/inertia)?
- Is the failure at parse time, finalize time, or simulation runtime?

### Canonical Workflow
1. Start from model-authoring docs and examples in `multibody/parsing/README_model_directives.md`, `examples/multibody/four_bar/README.md`, and `examples/multibody/strandbeest/README.md`.
2. For multi-file scenes, load directives and process into a plant instead of forcing one giant model file (`multibody/parsing/README_model_directives.md`).
3. Build with `AddMultibodyPlantSceneGraph` when geometry/collision are required.
4. Apply physically meaningful initial parameters (stiffness/damping/tolerances) before aggressive solver settings.
5. `Finalize()` plant only after all model/frame/weld directives are applied.
6. Validate with one runnable example and then sweep only 1-2 parameters at a time.

### Minimal Working Example
```cpp
// multibody/parsing/README_model_directives.md
ModelDirectives directives = LoadModelDirectives(
    FindResourceOrThrow("my_project/models/scene.dmd.yaml"));
DiagramBuilder<double> builder;
auto [plant, scene_graph] = AddMultibodyPlantSceneGraph<double>(&builder, 0.0);
ProcessModelDirectives(directives, &plant);
plant.Finalize();
```

```bash
# examples/multibody/four_bar/README.md
bazel run //examples/multibody/four_bar:passive_simulation -- --initial_velocity=1.0
```

### Pitfalls and Fixes
- Closed loops modeled with very stiff bushings can become numerically difficult; tune stiffness and damping together (`examples/multibody/four_bar/README.md`).
- Treating Model Directives names as flat strings causes frame/model scope mistakes; respect `::` scoping rules (`multibody/parsing/README_model_directives.md`).
- Forgetting to connect `SceneGraph` early leads to missing geometry/contact behavior.
- Changing many physical parameters at once hides root causes; run one-factor sweeps.
- For high stiffness models, smaller time steps and/or stronger damping are often needed for stable solves (`examples/multibody/four_bar/README.md`).

### Convergence and Validation Checks
- Parsed model graph matches intended hierarchy and scoped names.
- Constraint error and oscillation levels remain within target tolerances.
- Qualitative behavior remains consistent across small step-size changes.
- Geometry and contact visualization confirm expected collisions and frame placement.

### Source-Code Handoff
- Model directives API: `multibody/parsing/model_directives.h`, `multibody/parsing/model_directives.cc`.
- Directive execution path: `multibody/parsing/process_model_directives.h`, `multibody/parsing/process_model_directives.cc`.
- Parser geometry internals: `multibody/parsing/detail_urdf_geometry.h`, `multibody/parsing/detail_sdf_geometry.h`.
- Example implementation anchors: `examples/multibody/four_bar`, `examples/multibody/strandbeest`.

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/README.md`
- `examples/multibody/four_bar/README.md`
- `examples/multibody/strandbeest/README.md`
- `multibody/models/README.md`
- `examples/kuka_iiwa_arm/models/README.md`
- `doc/_release-notes/v1.9.0.md`
- `doc/_release-notes/v1.8.0.md`
- `doc/_release-notes/v1.7.0.md`
- `doc/_release-notes/v1.6.0.md`
- `doc/_release-notes/v1.50.0.md`
- `doc/_release-notes/v1.49.0.md`
- `doc/_release-notes/v1.47.0.md`

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
- `multibody/parsing/model_directives.h`
- `multibody/parsing/model_directives.cc`
- `multibody/parsing/process_model_directives.h`
- `multibody/parsing/process_model_directives.cc`
- `multibody/plant/force_density_field_declare_system_resources.cc`
- `geometry/render/render_material.h`
- `geometry/render/render_material.cc`
- `geometry/proximity/mesh_distance_boundary.h`
- `geometry/proximity/mesh_distance_boundary.cc`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).
