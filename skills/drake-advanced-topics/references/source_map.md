# drake source map: Advanced Topics

Generated from source roots:
- `common`
- `manipulation`
- `bindings/pydrake`
- `systems/sensors`
- `geometry/render_gl`
- `lcm`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" common manipulation bindings/pydrake systems/sensors geometry/render_gl lcm`
- `rg -n "class|struct|def|namespace" common manipulation bindings/pydrake systems/sensors geometry/render_gl lcm`
- If a doc mentions a symbol, search that exact symbol first and inspect adjacent implementation and tests.

## Implementation entry points
- `common/find_resource.h` | resource lookup API surface.
- `common/find_resource.cc` | resource lookup implementation.
- `common/find_runfiles.h` | runfiles API surface.
- `common/find_runfiles.cc` | runfiles resolution implementation.
- `manipulation/util/make_arm_controller_model.h` | manipulation model helper API.
- `manipulation/util/make_arm_controller_model.cc` | helper implementation and assumptions.
- `bindings/pydrake/__init__.py` | pydrake package initialization flow.
- `bindings/pydrake/multibody/__init__.py` | multibody module import surface.
- `bindings/pydrake/visualization/model_visualizer.py` | pydrake visualization utility flow.
- `visualization/concatenate_images.h` | image composition API used in docs/asset workflows.
- `systems/sensors/lcm_image_array_to_images.cc` | image message conversion behavior.
- `systems/sensors/lcm_image_array_to_images.h` | image message conversion API surface.
- `geometry/render_gl/internal_opengl_includes.h` | render include contract.
- `lcm/drake_lcm_interface.h` | LCM abstraction interface.

## Function-level behavior checks
- `common/test/find_resource_test.cc` | validates resource lookup edge cases.
- `common/test/find_runfiles_test.cc` | validates runfiles resolution behavior.
- `systems/sensors/test/lcm_image_array_to_images_test.cc` | validates image array conversion semantics.
- `bindings/pydrake/visualization/test/model_visualizer_test.py` | validates visualizer Python API behavior.
- `geometry/render_gl/test/internal_opengl_context_test.cc` | validates render context setup invariants.
- `lcm/test/drake_lcm_interface_test.cc` | validates LCM interface contract behavior.
