---
name: drake-index
description: This skill should be used when users ask how to use drake and the correct generated documentation skill must be selected before going deeper into source code.
---

# drake Skills Index

## Route the request
- Always classify into exactly one primary topic skill first; route to a second skill only when the user crosses topic boundaries.
- Enforce docs-first: answer from topic `SKILL.md` and `references/doc_map.md` before any source-file inspection.
- Prefer workflow-level guidance first; do not start with per-symbol source analysis unless docs are ambiguous or the user asks.

## Routing matrix (first hop)
- `drake-build-and-install`: install channels, source builds, compilers, toolchains, wheels, environment setup.
- `drake-getting-started`: first-day onboarding, quickstart path, where to start.
- `drake-inputs-and-modeling`: URDF/SDF/directives, plant + scene setup, geometry/contact inputs.
- `drake-simulation-workflows`: runtime execution loops, stepping/integrators, outputs/replay.
- `drake-api-and-scripting`: pydrake/module entry points, binding usage, script-level API lookup.
- `drake-examples-and-tutorials`: runnable demos, tutorial notebooks, cookbook-like examples.
- `drake-troubleshooting`: failure signatures, diagnostics, validation checks, escalation.
- `drake-parallel-hpc`: MPI/OpenMP/GPU, scaling runs, scheduler-oriented questions.
- `drake-advanced-topics`: collapsed low-volume topics (common, developer-guide, images, includes, manipulation, pydrake licensing docs).
- `drake-pages`: website/help/editor/platform docs under `doc/_pages`.
- `drake-tools`: tooling internals under `tools/*` and workspace/release helpers.
- `drake-third-party`: third-party legal/integration and external package references.
- `drake-release-notes`: release delta tracking and version-change lookups.
- `drake-multibody`: multibody-focused reference docs outside modeling playbooks.

## Generated topic skills
- `drake-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `drake-inputs-and-modeling`: Inputs and Modeling (inputs, system setup, models, and physical parameterization)
- `drake-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `drake-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `drake-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `drake-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `drake-troubleshooting`: Troubleshooting (known issues, diagnostics, and debugging patterns)
- `drake-parallel-hpc`: Parallel and HPC (MPI/OpenMP/GPU execution, scaling, and batch systems)
- `drake-advanced-topics`: Advanced Topics (collapsed low-volume topics: common, developer-guide, images, includes, manipulation, pydrake licensing)
- `drake-pages`: Pages (documentation grouped under the 'pages' theme)
- `drake-tools`: Tools (documentation grouped under the 'tools' theme)
- `drake-third-party`: Third Party (documentation grouped under the 'third-party' theme)
- `drake-release-notes`: Release Notes (documentation grouped under the 'release-notes' theme)
- `drake-multibody`: Multibody (documentation grouped under the 'multibody' theme)

## Documentation-first inputs
- `doc`
- `skills/*/references/doc_map.md`

## Tutorials and examples roots
- `examples`
- `tutorials`

## Test roots for behavior checks
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

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, search the same topic `references/doc_map.md`.
- If docs still leave ambiguity, open the same topic `references/source_map.md` and inspect suggested entry points.
- Keep the escalation within the routed topic; do not switch topics mid-debug unless user intent changed.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).

## Source directories for deeper inspection
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
