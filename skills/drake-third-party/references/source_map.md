# drake source map: Third Party

Generated from source roots:
- `doc/third_party`
- `tools/workspace`
- `visualization`
- `systems/sensors`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" doc/third_party tools/workspace visualization systems/sensors`
- `rg -n "license|third_party|vendor|repository|mirror" doc/third_party tools/workspace`
- For dependency questions, inspect workspace metadata and corresponding license/provenance docs together.

## Implementation entry points
- `tools/workspace/default.bzl` | dependency registration entrypoint.
- `tools/workspace/mirrors.bzl` | mirror and fetch policy definitions.
- `tools/workspace/metadata.py` | dependency metadata utilities.
- `tools/workspace/new_release.py` | dependency upgrade automation path.
- `tools/workspace/vendor_cxx.py` | C++ vendoring patch flow.
- `tools/workspace/drake_models/repository.bzl` | external models repository wiring.
- `visualization/concatenate_images.cc` | third-party image stack usage path.
- `systems/sensors/lcm_image_array_to_images.cc` | image message conversion path.

## Function-level behavior checks
- `tools/workspace/vendor_cxx_test.py` | validates vendoring helper behavior.
- `tools/workspace/drake_models/test/parse_test.py` | validates external model fetch/parse assumptions.
- `visualization/test/concatenate_images_test.cc` | validates image concatenation behavior.
- `systems/sensors/test/lcm_image_array_to_images_test.cc` | validates image array conversion behavior.
