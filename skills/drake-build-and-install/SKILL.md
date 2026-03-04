---
name: drake-build-and-install
description: This skill should be used when users ask about build and install in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Build and Install

## High-Signal Playbook
### Route Conditions
- Use this skill for install channel choice, source builds, compiler/toolchain setup, and wheel/bindings packaging.
- Route to `drake-getting-started` for first-run onboarding after install.
- Route to `drake-api-and-scripting` for pydrake usage patterns after install succeeds.
- Route to `drake-troubleshooting` when the primary need is failure diagnosis across logs.

### Triage Questions
- Which OS, version, and CPU architecture are you on?
- Do you need Python-only usage, C++ linking, or both?
- Are you installing from `pip` / `apt` / `tar.gz` or building from source?
- Do you need proprietary solvers (for example Gurobi or SNOPT)?
- Are you using Bazel development workflow or CMake install workflow?
- Are you using Conda, system Python, or Homebrew Python?

### Canonical Workflow
1. Confirm supported platform/toolchain in `doc/_pages/installation.md` and `doc/_pages/from_source.md`.
2. Choose install path: `pip` (`doc/_pages/pip.md`), `apt` (`doc/_pages/apt.md`), direct binary (`doc/_pages/from_binary.md`), or source (`doc/_pages/from_source.md`).
3. Run exactly one path first; do not mix channels in the same environment.
4. For source builds, install prerequisites via `setup/install_prereqs` then use CMake wrapper flow (`doc/_pages/from_source.md`) or Bazel developer flow (`doc/_pages/bazel.md`).
5. Validate with one smoke check (`python3 -c "import pydrake"` or one `bazel run` example).
6. Escalate to `references/source_map.md` only for unresolved behavior details.

### Minimal Working Example
```bash
# Python quickstart (doc/_pages/pip.md)
python3 -m venv env
env/bin/pip install drake
source env/bin/activate
python3 -c "import pydrake; print('pydrake import ok')"

# Source install (doc/_pages/from_source.md)
git clone --filter=blob:none https://github.com/RobotLocomotion/drake.git
drake/setup/install_prereqs
mkdir drake-build && cd drake-build
cmake ../drake -DCMAKE_BUILD_TYPE=Release
cmake --build . -j"$(nproc)"
cmake --install .
```

### Pitfalls and Fixes
- Binary channels (`pip`, `apt`, `tar.gz`) do not include Gurobi support; build from source when Gurobi is required (`doc/_pages/installation.md`, `doc/_pages/apt.md`, `doc/_pages/pip.md`, `doc/_pages/from_binary.md`).
- Conda environments are not regularly tested; prefer system/Homebrew Python when debugging compatibility (`doc/_pages/installation.md`, `doc/_pages/pip.md`).
- On macOS direct downloads, use command-line download tools (for example `curl`) to avoid Gatekeeper friction (`doc/_pages/from_binary.md`).
- Clang 17+ on Linux needs `-fno-assume-unique-vtables` in project flags when linking against Drake (`doc/_pages/from_source.md`).
- Repeated `make install` can leave stale files; clean install trees when changing versions/options (`doc/_pages/from_source.md`).
- `make -j` has limited effect because Bazel runs underneath CMake wrapper; tune Bazel settings for OOM cases (`doc/_pages/from_source.md`).

### Convergence and Validation Checks
- `python3 -c "import pydrake"` succeeds in the target environment.
- At least one Drake example runs (`bazel run //examples/acrobot:run_passive` or equivalent).
- C++ downstream build finds `drake-config.cmake` and links successfully.
- Compiler / stdlib / Python versions match supported tables in `doc/_pages/installation.md`.

### Source-Code Handoff
- CMake wrapper behavior: `CMakeLists.txt`, `tools/install/libdrake/drake-config.cmake.in`.
- Version/config generation: `tools/install/libdrake/generate_version.cmake`, `tools/workspace/cmake_configure_file.py`.
- Dependency wiring: `MODULE.bazel`, `tools/workspace/default.bzl`, `tools/workspace/README.md`.
- Wheel packaging path: `tools/wheel/wheel_builder/main.py`, `tools/wheel/wheel_builder/linux.py`, `tools/wheel/wheel_builder/macos.py`.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/mass_spring_cloth/README.md`
- `examples/simple_gripper/README.md`
- `examples/planar_gripper/README.md`
- `examples/kinova_jaco_arm/README.md`
- `examples/hardware_sim/README.md`
- `examples/multibody/inclined_plane_with_body/README.md`
- `tools/release_engineering/dev/README.md`
- `examples/allegro_hand/joint_control/README.md`
- `tools/workspace/vtk_internal/README.md`
- `tools/release_engineering/README.md`
- `tools/workspace/crate_universe/README.md`
- `tools/install/dockerhub/noble/README.md`

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
- `CMakeLists.txt`
- `MODULE.bazel`
- `tools/install/libdrake/drake-config.cmake.in`
- `tools/install/libdrake/generate_version.cmake`
- `tools/workspace/cmake_configure_file.py`
- `tools/workspace/pybind11/pybind11-config.cmake`
- `tools/workspace/pybind11/pybind11-config-version.cmake`
- `tools/wheel/wheel_builder/main.py`
- `tools/wheel/wheel_builder/linux.py`
- `tools/wheel/wheel_builder/macos.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).
