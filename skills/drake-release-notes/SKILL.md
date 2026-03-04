---
name: drake-release-notes
description: This skill should be used when users ask about release notes in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Release Notes

## High-Signal Playbook
### Route Conditions
- Use this skill for version-to-version deltas, migration impact, and release engineering note generation.
- Route to topic skills when the user needs deep technical changes in one subsystem.

### Triage Questions
- Which version range is in scope?
- Are they asking about breaking changes, feature additions, or packaging shifts?
- Do they need human-facing summary or scripted release-note generation?

### Canonical Workflow
1. Start with `doc/_release-notes/release_notes.md` index.
2. Read both endpoints and intermediate releases in scope.
3. Extract concrete breaking changes and behavior-affecting notes.
4. For automation questions, inspect release tooling in `references/source_map.md`.

### Minimal Working Example
```bash
python3 tools/release_engineering/relnotes.py --help
python3 tools/workspace/new_release.py --help
```

### Pitfalls and Fixes
- Reading only one endpoint misses phased deprecations across several releases.
- Historical notes (2015/2016) are archival and should not replace modern release docs.

### Convergence and Validation Checks
- Version range and breaking changes are explicitly enumerated.
- Any tooling output is tied to the exact checked-out source revision.

### Source-Code Handoff
- Release note generation and package prep: `tools/release_engineering/relnotes.py`, `tools/release_engineering/repack_deb.py`, `tools/release_engineering/download_release_candidate.py`.
- Release workflow scripts: `tools/release_engineering/dev/push_release.py`, `tools/release_engineering/dev/push_docker.py`, `tools/workspace/new_release.py`.

## Scope
- Handle questions about release deltas and release process behavior.

## Primary documentation references
- `doc/_release-notes/release_notes.md`
- `doc/_release-notes/v1.50.0.md`
- `doc/_release-notes/v1.49.0.md`
- `doc/_release-notes/v1.48.0.md`
- `doc/_release-notes/end_of_support.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.

## Tutorials and examples
- `doc/_release-notes`

## Test references
- `tools/workspace/bzlmod_sync_test.py`
- `tools/workspace/vendor_cxx_test.py`

## Optional deeper inspection
- `tools/release_engineering`
- `tools/workspace`
- `doc/_release-notes`

## Source entry points for unresolved issues
- `tools/release_engineering/relnotes.py`
- `tools/workspace/new_release.py`
- `tools/release_engineering/repack_deb.py`
- `tools/release_engineering/download_release_candidate.py`
- `tools/release_engineering/dev/push_release.py`
- `tools/release_engineering/dev/push_docker.py`
- `tools/release_engineering/debian/control.in`
- `tools/release_engineering/debian/changelog.in`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" tools/release_engineering tools/workspace doc/_release-notes`).
