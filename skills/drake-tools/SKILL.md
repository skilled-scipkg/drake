---
name: drake-tools
description: This skill should be used when users ask about tools in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Tools

## High-Signal Playbook
### Route Conditions
- Use this skill for build/release tooling (`tools/wheel`, `tools/workspace`, Skylark macros) and dependency maintenance workflow.
- Route to `drake-build-and-install` for user-facing installation channel decisions.
- Route to `drake-pages` when the task is documentation-authoring policy rather than tooling internals.
- Route to `drake-troubleshooting` for broad runtime/build failure triage.

### Triage Questions
- Is the task wheel build/test, external dependency upgrade, or docs tooling upgrade?
- Are you running on Ubuntu (containerized wheel path) or macOS (host build path)?
- Do you need a release artifact, local debug build, or CI verification only?
- Are you changing internal workspace repos, Skylark macros, or tool wrappers?
- What validation is required (`lint`, wheel tests, doc build, or all)?

### Canonical Workflow
1. Start from exact tool README (`tools/wheel/README.rst`, `tools/workspace/README.md`, `tools/workspace/doxygen_internal/README.md`, `tools/skylark/README.md`).
2. Prepare developer prerequisites (`setup/install_prereqs --developer`) before tool operations.
3. Run the smallest command that reproduces/advances the workflow (wheel build, new_release report, doxygen build target).
4. Apply fixes in tool-specific scripts/configs, not in downstream consumers first.
5. Validate with the corresponding checks (`tools/wheel/test/*`, `bazel test --config lint //...`, `bazel build //doc/doxygen_cxx:build`).

### Minimal Working Example
```bash
# External upgrade scan (tools/workspace/README.md)
bazel run //tools/workspace:new_release

# Wheel build entrypoint (tools/wheel/README.rst)
bazel run //tools/wheel:builder -- 1.50.0

# Doxygen-only docs build (tools/workspace/doxygen_internal/README.md)
bazel build //doc/doxygen_cxx:build
```

### Pitfalls and Fixes
- Wheel builder includes local uncommitted changes by design; use a clean checkout for release artifacts (`tools/wheel/README.rst`).
- Wheel builds require writable `${HOME}` and `/tmp`; missing permissions cause opaque failures (`tools/wheel/README.rst`).
- macOS wheels need full host dependencies installed, unlike Ubuntu containerized path (`tools/wheel/README.rst`).
- Doxygen upgrade flow is supported on Ubuntu Noble only (`tools/workspace/doxygen_internal/README.md`).
- `new_release` patch conflicts may require removing stale `upstream` patches before rerun (`tools/workspace/README.md`).

### Convergence and Validation Checks
- Wheel build finishes and wheel tests pass from `tools/wheel/test/tests/*`.
- `bazel test --config lint //...` passes after workspace upgrades.
- Doxygen target builds and generated docs layout/styles are visually sane.
- Tool changes are scoped to the intended external/tool and are easy to revert independently.

### Source-Code Handoff
- Wheel orchestration: `tools/wheel/wheel_builder/main.py`, `tools/wheel/wheel_builder/linux.py`, `tools/wheel/wheel_builder/macos.py`.
- Wheel build/test scripts: `tools/wheel/image/build-wheel.sh`, `tools/wheel/test/test-wheel.sh`.
- Workspace upgrade tooling: `tools/workspace/new_release.py`, `tools/workspace/default.bzl`, `tools/workspace/mirrors.bzl`.
- Doxygen internals: `tools/workspace/doxygen_internal/repository.bzl`, `tools/workspace/doxygen_internal/build_binaries_with_docker`.
- Docstring extraction tooling: `tools/workspace/mkdoc_internal/mkdoc.py`, `tools/workspace/mkdoc_internal/libclang_setup.py`.

## Scope
- Handle questions about documentation grouped under the 'tools' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `tools/wheel/README.rst`
- `tools/workspace/doxygen_internal/README.md`
- `tools/README.md`
- `tools/skylark/README.md`
- `tools/workspace/stable_baselines3_internal/README.md`
- `tools/workspace/qdldl_internal/README.md`
- `tools/workspace/meshcat/README.md`
- `tools/workspace/mkdoc_internal/README.md`
- `tools/workspace/vtk_internal/gen/README.md`
- `tools/workspace/mosek/drake_mosek_redistribution.txt`

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
- `tools/wheel/wheel_builder/main.py`
- `tools/wheel/wheel_builder/linux.py`
- `tools/wheel/wheel_builder/macos.py`
- `tools/workspace/new_release.py`
- `tools/workspace/default.bzl`
- `tools/workspace/doxygen_internal/repository.bzl`
- `tools/workspace/mkdoc_internal/libclang_setup.py`
- `tools/workspace/mkdoc_internal/mkdoc.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).
