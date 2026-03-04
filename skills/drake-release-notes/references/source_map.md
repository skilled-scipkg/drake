# drake source map: Release Notes

Generated from source roots:
- `tools/release_engineering`
- `tools/workspace`
- `doc/_release-notes`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" tools/release_engineering tools/workspace doc/_release-notes`
- `rg -n "release|notes|debian|docker|candidate" tools/release_engineering tools/workspace`
- For migration questions, tie tooling output back to exact release-note files.

## Implementation entry points
- `tools/release_engineering/relnotes.py` | release notes generation script.
- `tools/workspace/new_release.py` | dependency update and release prep helper.
- `tools/release_engineering/repack_deb.py` | Debian package repackaging flow.
- `tools/release_engineering/download_release_candidate.py` | release candidate fetch workflow.
- `tools/release_engineering/dev/push_release.py` | release publication helper.
- `tools/release_engineering/dev/push_docker.py` | Docker publication helper.
- `tools/release_engineering/debian/control.in` | Debian package metadata template.
- `tools/release_engineering/debian/changelog.in` | Debian changelog template.

## Function-level behavior checks
- `tools/workspace/bzlmod_sync_test.py` | validates workspace metadata sync assumptions.
- `tools/workspace/vendor_cxx_test.py` | validates vendor patch/update helper behavior.
