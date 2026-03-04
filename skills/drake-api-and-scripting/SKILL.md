---
name: drake-api-and-scripting
description: This skill should be used when users ask about api and scripting in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: API and Scripting

## High-Signal Playbook
### Route Conditions
- Use this skill for `pydrake` module discovery, binding semantics, script-level simulation setup, and API parity questions between C++ and Python.
- Route to `drake-inputs-and-modeling` for model authoring/parsing strategy.
- Route to `drake-simulation-workflows` for runtime stepping/contact tuning.
- Route to `drake-troubleshooting` when import/runtime failures dominate.

### Triage Questions
- Is the user writing Python, C++, Julia interop, or mixed workflows?
- Do they need quick prototyping (`pydrake.all`) or production-style explicit imports?
- Is the issue import-time, type/templating, binding coverage, or runtime behavior?
- Which module is in scope (`systems`, `multibody`, `geometry`, `solvers`)?

### Canonical Workflow
1. Start with `doc/_pages/python_bindings.md` and select the minimal module imports needed.
2. Validate local binding health (`python3 -c 'import pydrake.all'`).
3. Use tutorials/examples for known-good API call chains before custom code.
4. For missing/ambiguous behavior, inspect `references/source_map.md` implementation + tests.
5. Confirm parity with target language path (Python bindings vs C++ symbol).

### Minimal Working Example
```bash
python3 -c 'import pydrake.all; print("pydrake import ok")'
python3 -m pydrake.tutorials
```

```python
from pydrake.all import (
    AddMultibodyPlantSceneGraph, DiagramBuilder, Parser, Simulator)

builder = DiagramBuilder()
plant, _ = AddMultibodyPlantSceneGraph(builder, time_step=0.0)
Parser(plant).AddModels("drake/examples/pendulum/Pendulum.urdf")
plant.Finalize()
diagram = builder.Build()
Simulator(diagram)
```

### Pitfalls and Fixes
- `from pydrake.all import *` can create hard-to-debug symbol collisions; prefer explicit imports (`doc/_pages/python_bindings.md`).
- Conda setups are less regularly tested; include environment details in bug reports (`doc/_pages/python_bindings.md`).
- Template/scalar confusion (`Adder` vs `Adder_`) often causes type errors; verify scalar specialization first.
- Gym examples need external Python deps (`gymnasium`, `stable_baselines3`) not shipped by default (`bindings/pydrake/gym/README.md`).

### Convergence and Validation Checks
- `import pydrake` and `import pydrake.all` succeed in the target environment.
- Minimal diagram build/simulator construction runs without exceptions.
- The chosen module test file in `bindings/pydrake/**/test` covers the relevant behavior.

### Source-Code Handoff
- Core package/export surface: `bindings/pydrake/__init__.py`, `bindings/pydrake/all.py`.
- Binding glue by domain: `bindings/pydrake/common/module_py.cc`, `bindings/pydrake/systems/framework_py.cc`, `bindings/pydrake/systems/analysis_py.cc`, `bindings/pydrake/multibody/plant_py.cc`, `bindings/pydrake/geometry/geometry_py.cc`.
- Python-side helpers: `bindings/pydrake/multibody/_plant_extra.py`, `bindings/pydrake/common/_common_extra.py`.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses architectural first; go per-function only when asked.

## Primary documentation references
- `doc/_pages/python_bindings.md`
- `tutorials/README.md`
- `doc/_pages/julia_bindings.md`
- `bindings/pydrake/gym/README.md`
- `doc/_pages/code_style_guide.md`
- `tools/workspace/python/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `bindings/pydrake/test`
- `bindings/pydrake/common/test`
- `bindings/pydrake/systems/test`
- `bindings/pydrake/multibody/test`
- `bindings/pydrake/geometry/test`

## Optional deeper inspection
- `bindings`
- `systems`
- `multibody`
- `geometry`
- `solvers`
- `tools/workspace`

## Source entry points for unresolved issues
- `bindings/pydrake/__init__.py`
- `bindings/pydrake/all.py`
- `bindings/pydrake/common/module_py.cc`
- `bindings/pydrake/systems/framework_py.cc`
- `bindings/pydrake/systems/analysis_py.cc`
- `bindings/pydrake/multibody/plant_py.cc`
- `bindings/pydrake/geometry/geometry_py.cc`
- `bindings/pydrake/multibody/_plant_extra.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings systems multibody geometry`).
