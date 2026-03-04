---
name: drake-getting-started
description: This skill should be used when users ask about getting started in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Getting Started

## High-Signal Playbook
### Route Conditions
- Use this skill for first-day orientation, quickstart path selection, and "what should I run first?" questions.
- Route to `drake-build-and-install` for detailed channel/toolchain decisions.
- Route to `drake-simulation-workflows` for runtime/integration controls once setup is done.
- Route to `drake-pages` for docs policy/help-page specifics.

### Triage Questions
- Are you a first-time user, a downstream integrator, or a Drake contributor?
- Do you need Python tutorials, C++ development, or both?
- Are you installing binaries (`pip`/`apt`/`tar.gz`) or building from source?
- Which platform/version are you on relative to supported configurations?
- Do you want to run tutorials locally, examples locally, or both?
- If blocked, what exact command and environment produced the error?

### Canonical Workflow
1. Start with install and platform tables in `doc/_pages/installation.md`.
2. Pick one install path and complete it before exploring alternates.
3. Run tutorials path (`tutorials/README.md`) for fastest Python validation.
4. For contributors, follow Bazel developer path in `doc/_pages/bazel.md`.
5. Use `doc/index.md` for curated links to APIs, tutorials, examples, and help channels.
6. When requesting help, include the metadata checklist from `doc/_pages/getting_help.md`.

### Minimal Working Example
```bash
# Quick Python path (tutorials/README.md + doc/_pages/pip.md)
python3 -m venv env
env/bin/pip install drake
source env/bin/activate
python3 -m pydrake.tutorials

# Contributor path (doc/_pages/bazel.md)
git clone --filter=blob:none https://github.com/RobotLocomotion/drake.git
drake/setup/install_prereqs --developer
cd drake
bazel build //examples/acrobot:run_passive
```

### Pitfalls and Fixes
- Unsupported OS/Python/compiler combinations cause undefined behavior; verify tables before debugging (`doc/_pages/installation.md`).
- Missing `PYTHONPATH` or environment activation breaks local tutorial launch (`tutorials/README.md`, `doc/_pages/from_binary.md`, `doc/_pages/apt.md`).
- Renaming checkout away from `drake` degrades some IDE integrations (`doc/_pages/bazel.md`).
- For help requests, missing version/install metadata slows diagnosis (`doc/_pages/getting_help.md`).

### Convergence and Validation Checks
- Tutorials launch successfully via `python3 -m pydrake.tutorials`.
- At least one reference example target builds/runs locally.
- User can name their install channel and exact Drake version.
- User has the right escalation channel (GitHub issue vs GitHub discussion).

### Source-Code Handoff
- Dependency and module wiring: `MODULE.bazel`, `tools/workspace/default.bzl`, `tools/workspace/README.md`.
- Early contact-solver internals (if onboarding into multibody contact): `multibody/contact_solvers/icf/icf_solver.h`, `multibody/contact_solvers/icf/icf_solver.cc`.
- Python binding package roots: `bindings/pydrake/__init__.py`, `bindings/pydrake/systems/__init__.py`.

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/index.md`
- `tools/workspace/README.md`
- `multibody/contact_solvers/icf/README.md`
- `doc/_pages/installation.md`
- `doc/_pages/vim.md`
- `doc/_pages/sublime_text.md`
- `doc/_pages/developers.md`
- `doc/_pages/buildcop.md`
- `doc/_pages/bazel.md`
- `doc/_pages/reviewable.md`
- `doc/_pages/unit_testing_instructions.md`

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
- `MODULE.bazel`
- `tools/workspace/default.bzl`
- `bindings/generated_docstrings/multibody_contact_solvers_icf.h`
- `multibody/contact_solvers/icf/icf_solver_parameters.h`
- `multibody/contact_solvers/icf/icf_solver.h`
- `multibody/contact_solvers/icf/icf_solver.cc`
- `multibody/contact_solvers/icf/icf_model.h`
- `multibody/contact_solvers/icf/icf_model.cc`
- `bindings/pydrake/__init__.py`
- `bindings/pydrake/systems/__init__.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).
