# drake source map: API and Scripting

Generated from source roots:
- `bindings/pydrake`
- `systems`
- `multibody`
- `geometry`
- `tools/workspace`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" bindings/pydrake systems multibody geometry tools/workspace`
- `rg -n "class|def|struct|namespace" bindings/pydrake systems multibody geometry tools/workspace`
- Start with the bound symbol in `bindings/pydrake/*` and then trace into corresponding C++ implementation.

## Implementation entry points
- `bindings/pydrake/__init__.py` | package initialization and top-level behavior.
- `bindings/pydrake/all.py` | aggregate import surface and helper policy.
- `bindings/pydrake/common/module_py.cc` | common module binding registration.
- `bindings/pydrake/systems/framework_py.cc` | systems framework binding layer.
- `bindings/pydrake/systems/analysis_py.cc` | simulator/integrator binding layer.
- `bindings/pydrake/multibody/plant_py.cc` | multibody plant binding layer.
- `bindings/pydrake/geometry/geometry_py.cc` | geometry binding layer.
- `bindings/pydrake/multibody/_plant_extra.py` | Python-side multibody helpers.
- `bindings/pydrake/common/_common_extra.py` | Python-side common helpers.

## Function-level behavior checks
- `bindings/pydrake/test/all_each_import_test.py` | validates import surface consistency.
- `bindings/pydrake/test/parse_models_test.py` | validates parser-facing Python APIs.
- `bindings/pydrake/common/test/module_test.py` | validates common module behavior.
- `bindings/pydrake/systems/test/analysis_test.py` | validates analysis/simulator bindings.
- `bindings/pydrake/systems/test/primitives_test.py` | validates primitives binding semantics.
- `bindings/pydrake/multibody/test/plant_test.py` | validates multibody plant Python behavior.
- `bindings/pydrake/geometry/test/scene_graph_test.py` | validates geometry/scene graph binding behavior.
