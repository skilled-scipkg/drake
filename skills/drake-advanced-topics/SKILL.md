---
name: drake-advanced-topics
description: This skill consolidates low-volume Drake topics (common, developer-guide, images, includes, manipulation, pydrake licensing) into one docs-first routing node.
---

# drake: Advanced Topics

## Scope
- Use this skill when a request maps to one of the collapsed low-doc areas: common resource lookup, contributor agreement/legal text, image asset notes, include fragments, manipulation overview, or pydrake license text.
- Keep responses short and route to a higher-signal skill when the request broadens into build, simulation, or API usage.

## Route the request
- `common/test/find_resource_test_data.txt`: resource lookup and `FindResource`-style questions.
- `doc/third_party/pylons/CONTRIBUTORS.txt`: contributor agreement/legal provenance text.
- `doc/images/drake-dragon.README.txt`: website/image asset conversion notes.
- `doc/_includes/toc.md`: docs include fragment/table-of-contents plumbing.
- `manipulation/README.md`: top-level manipulation module overview.
- `doc/pydrake/LICENSE.TXT`: pydrake license text and compliance questions.

## Primary documentation references
- `common/test/find_resource_test_data.txt`
- `doc/third_party/pylons/CONTRIBUTORS.txt`
- `doc/images/drake-dragon.README.txt`
- `doc/_includes/toc.md`
- `manipulation/README.md`
- `doc/pydrake/LICENSE.TXT`

## Workflow
- Start from the exact primary doc above that matches the request.
- If detail is missing, inspect `references/doc_map.md` for consolidated inventory.
- Escalate to `references/source_map.md` only when behavior details (implementation, symbols, APIs) are required.
- Route out to `drake-build-and-install`, `drake-inputs-and-modeling`, `drake-simulation-workflows`, or `drake-api-and-scripting` when the request exits these narrow topics.

## Source entry points for unresolved issues
- `common/find_resource.h`
- `common/find_resource.cc`
- `manipulation/util/make_arm_controller_model.h`
- `manipulation/util/make_arm_controller_model.cc`
- `bindings/pydrake/__init__.py`
- `bindings/pydrake/multibody/__init__.py`
- `visualization/concatenate_images.h`
- `systems/sensors/lcm_image_array_to_images.h`
- `geometry/render_gl/internal_opengl_includes.h`
- `lcm/drake_lcm_interface.h`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" bindings cmake common examples geometry lcm lcmtypes manipulation math multibody perception planning solvers systems tools tutorials visualization`).
