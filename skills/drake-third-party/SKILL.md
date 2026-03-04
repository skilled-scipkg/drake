---
name: drake-third-party
description: This skill should be used when users ask about third party in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Third Party

## High-Signal Playbook
### Route Conditions
- Use this skill for third-party licensing, dependency provenance, and external package integration references.
- Route to `drake-tools` for deep workspace tooling mechanics.
- Route to `drake-release-notes` for version-change communication.

### Triage Questions
- Is this a legal/compliance question, an upgrade/integration task, or both?
- Which dependency/package is in scope?
- Is the user editing docs-only records or source/tooling that enforces dependency state?

### Canonical Workflow
1. Start with `doc/third_party/*` docs and license files.
2. Identify dependency wiring in `tools/workspace` only when docs are insufficient.
3. Validate impact using targeted tests (`vendor_cxx`, dependency parse checks).

### Minimal Working Example
```bash
python3 tools/workspace/new_release.py --help
python3 tools/workspace/vendor_cxx.py --help
```

### Pitfalls and Fixes
- Updating dependency versions without updating license/provenance notes creates compliance drift.
- Mixing dependency metadata changes with unrelated simulation changes hides review risk.

### Convergence and Validation Checks
- License text and dependency metadata are mutually consistent.
- Targeted dependency/tooling checks pass for touched packages.

### Source-Code Handoff
- Workspace dependency registry: `tools/workspace/default.bzl`, `tools/workspace/mirrors.bzl`, `tools/workspace/metadata.py`, `tools/workspace/new_release.py`, `tools/workspace/vendor_cxx.py`.
- Third-party-facing runtime surfaces often touched by dependency updates: `visualization/concatenate_images.cc`, `systems/sensors/lcm_image_array_to_images.cc`.

## Scope
- Handle questions about third-party docs, legal notes, and integration references.

## Primary documentation references
- `doc/third_party/README.md`
- `doc/third_party/pylons/README.md`
- `doc/third_party/github-styling/README.md`
- `doc/third_party/dracula/README.md`
- `doc/third_party/images/GitHub-Mark.README.txt`
- `doc/third_party/pylons/LICENSE.txt`
- `doc/third_party/github-styling/LICENSE.txt`
- `doc/third_party/dracula/LICENSE.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.

## Tutorials and examples
- `doc/third_party`

## Test references
- `tools/workspace/vendor_cxx_test.py`
- `tools/workspace/drake_models/test/parse_test.py`
- `visualization/test/concatenate_images_test.cc`
- `systems/sensors/test/lcm_image_array_to_images_test.cc`

## Optional deeper inspection
- `tools/workspace`
- `doc/third_party`
- `visualization`
- `systems/sensors`

## Source entry points for unresolved issues
- `tools/workspace/default.bzl`
- `tools/workspace/mirrors.bzl`
- `tools/workspace/metadata.py`
- `tools/workspace/new_release.py`
- `tools/workspace/vendor_cxx.py`
- `visualization/concatenate_images.cc`
- `systems/sensors/lcm_image_array_to_images.cc`
- `tools/workspace/drake_models/repository.bzl`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" doc/third_party tools/workspace visualization systems/sensors`).
