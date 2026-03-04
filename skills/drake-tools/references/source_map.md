# drake source map: Tools

Generated from source roots:
- `tools/wheel`
- `tools/workspace`
- `tools/install`
- `tools/release_engineering`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" tools/wheel tools/workspace tools/install tools/release_engineering`
- `rg -n "wheel|workspace|release|doxygen|mkdoc|install" tools/wheel tools/workspace tools/install tools/release_engineering`
- Prefer touching tool-specific scripts/configs before changing downstream consumers.

## Implementation entry points
- `tools/wheel/wheel_builder/main.py` | wheel build orchestration entrypoint.
- `tools/wheel/wheel_builder/linux.py` | Linux wheel build logic.
- `tools/wheel/wheel_builder/macos.py` | macOS wheel build logic.
- `tools/workspace/new_release.py` | dependency/release helper.
- `tools/workspace/default.bzl` | baseline workspace dependency wiring.
- `tools/workspace/mirrors.bzl` | mirror resolution path.
- `tools/workspace/doxygen_internal/repository.bzl` | doxygen toolchain repository wiring.
- `tools/workspace/mkdoc_internal/mkdoc.py` | C++ API docstring extraction tool.
- `tools/workspace/mkdoc_internal/libclang_setup.py` | libclang configuration for doc extraction.
- `tools/workspace/vtk_internal/data_to_header.py` | VTK codegen helper used in upgrades.

## Function-level behavior checks
- `tools/wheel/test/tests/sanity-test.py` | validates wheel runtime sanity.
- `tools/wheel/test/tests/libs-test.py` | validates wheel library packaging.
- `tools/workspace/vtk_internal/test/data_to_header_test.cc` | validates VTK header generation helper.
- `tools/workspace/mkdoc_internal/test/mkdoc_comment_test.py` | validates mkdoc comment parsing.
- `tools/workspace/vendor_cxx_test.py` | validates vendoring helper behavior.
- `tools/workspace/bzlmod_sync_test.py` | validates module/workspace sync helper behavior.
