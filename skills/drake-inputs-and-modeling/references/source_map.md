# drake source map: Inputs and Modeling

Generated from source roots:
- `multibody/parsing`
- `multibody/plant`
- `geometry`
- `systems/rendering`
- `examples/multibody`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" multibody/parsing multibody/plant geometry systems/rendering examples/multibody`
- `rg -n "ModelDirectives|Parser|geometry|contact|Finalize" multibody/parsing multibody/plant`
- For parser/modeling questions, inspect parsing implementation and corresponding parser tests together.

## Implementation entry points
- `multibody/parsing/model_directives.h` | directives schema and API surface.
- `multibody/parsing/model_directives.cc` | directives data model implementation.
- `multibody/parsing/process_model_directives.h` | directive execution API.
- `multibody/parsing/process_model_directives.cc` | directive execution implementation.
- `multibody/parsing/detail_dmd_parser.cc` | YAML directives parser internals.
- `multibody/parsing/detail_urdf_geometry.cc` | URDF geometry parsing behavior.
- `multibody/parsing/detail_sdf_geometry.cc` | SDF geometry parsing behavior.
- `multibody/plant/force_density_field_declare_system_resources.cc` | force-density resource declaration path.
- `multibody/plant/internal_geometry_names.cc` | geometry naming policy in plant internals.
- `geometry/render/render_material.h` | render material API surface.
- `geometry/render/render_material.cc` | material/render property mapping.
- `geometry/proximity/mesh_distance_boundary.h` | geometry boundary API surface.
- `geometry/proximity/mesh_distance_boundary.cc` | mesh boundary behavior implementation.
- `systems/rendering/multibody_position_to_geometry_pose.cc` | plant-to-geometry pose bridge.

## Function-level behavior checks
- `multibody/parsing/test/model_directives_test.cc` | validates directive schema behavior.
- `multibody/parsing/test/process_model_directives_test.cc` | validates directive execution semantics.
- `multibody/parsing/test/detail_urdf_geometry_test.cc` | validates URDF geometry parsing behavior.
- `multibody/parsing/test/detail_sdf_geometry_test.cc` | validates SDF geometry parsing behavior.
- `multibody/plant/test/internal_geometry_names_test.cc` | validates geometry naming resolution.
- `multibody/plant/test/multibody_plant_hydroelastic_test.cc` | validates contact/geometry integration behavior.
- `examples/multibody/strandbeest/test/run_with_motor_test.py` | validates end-to-end modeled example behavior.
