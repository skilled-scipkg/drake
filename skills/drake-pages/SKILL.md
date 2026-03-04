---
name: drake-pages
description: This skill should be used when users ask about pages in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Pages

## High-Signal Playbook
### Route Conditions
- Use this skill for website/page-level documentation topics (`doc/_pages/*`), contributor help pages, and doc-generation guidance.
- Route to `drake-build-and-install` for package installation execution steps.
- Route to `drake-getting-started` for first-use onboarding and quickstart flow.
- Route to `drake-troubleshooting` when the request is mainly runtime/build failure diagnosis.

### Triage Questions
- Is the user asking about getting help, platform notes, editor setup, or docs generation?
- Which exact page path is in scope (`doc/_pages/<name>.md`)?
- Is the user an end user, contributor, or release/docs maintainer?
- Do they need Doxygen, Sphinx, or only content updates?
- Is the expected output a command sequence, a policy answer, or an escalation path?

### Canonical Workflow
1. Route to the exact page under `doc/_pages/` first (for example `getting_help.md`, `doxygen_instructions.md`, `sphinx_instructions.md`).
2. If page references another canonical instruction page, follow that chain next (for example docs generation instructions).
3. Answer with file-path-cited guidance, not paraphrased folklore.
4. For docs toolchain behavior details, escalate to the doxygen-related source and config files.
5. For ambiguous requests, ask for page path + user role before deep diving.

### Minimal Working Example
```bash
# Helpful diagnostics checklist from doc/_pages/getting_help.md
which bazel; bazel version
which cmake; cmake --version
git rev-parse --short HEAD

# Doxygen preview anchor from tools/workspace/doxygen_internal/README.md
bazel build //doc/doxygen_cxx:build
```

### Pitfalls and Fixes
- Skipping issue/discussion search before asking for help slows triage (`doc/_pages/getting_help.md`).
- Missing environment metadata (OS/install method/tool versions) leads to low-signal bug reports (`doc/_pages/getting_help.md`).
- `@system ... @endsystem` blocks must be valid YAML with required `name` key (`doc/_pages/doxygen_instructions.md`).
- Doxygen style changes can break Drake patches/CSS; update patch and CSS with each version bump (`tools/workspace/doxygen_internal/README.md`).

### Convergence and Validation Checks
- The response cites the exact `doc/_pages/*.md` file that defines policy.
- Help requests include OS, install channel, build system, and version details.
- Docs generation command finishes for the targeted site component.
- Escalation to source is limited to tooling internals, not user-level guidance.

### Source-Code Handoff
- Doxygen content group anchors: `geometry/geometry_doxygen.h`, `multibody/multibody_doxygen.h`, `common/cxx_doxygen.h`.
- Drake Doxygen build customizations: `doc/doxygen_cxx/Doxyfile_CXX.in`, `doc/doxygen_cxx/DoxygenLayout.xml`, `doc/doxygen_cxx/header.html.patch`, `doc/doxygen_cxx/doxygen_extra.css`.
- Doxygen binary upgrade tooling: `tools/workspace/doxygen_internal/README.md`, `tools/workspace/doxygen_internal/build_binaries_with_docker`.

## Scope
- Handle questions about documentation grouped under the 'pages' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/_pages/emacs.md`
- `doc/_pages/doxygen_instructions.md`
- `doc/_pages/getting_help.md`
- `doc/_pages/unicode_tips_tricks.md`
- `doc/_pages/sphinx_instructions.md`
- `doc/_pages/credits.md`
- `doc/_pages/website_licenses.md`
- `doc/_pages/ubuntu.md`
- `doc/_pages/tm.md`
- `doc/_pages/platform_reviewer_checklist.md`
- `doc/_pages/mac.md`
- `doc/_pages/downstream_testing.md`

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
- `geometry/geometry_infrastructure_doxygen.h`
- `geometry/geometry_file_formats_doxygen.h`
- `geometry/geometry_doxygen.h`
- `solvers/mathematical_program_doxygen.h`
- `planning/planning_doxygen.h`
- `multibody/multibody_doxygen.h`
- `common/cxx_doxygen.h`
- `multibody/plant/simulation_and_solvers_doxygen.h`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).
