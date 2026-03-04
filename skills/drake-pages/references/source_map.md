# drake source map: Pages

Generated from source roots:
- `doc/doxygen_cxx`
- `doc/pydrake`
- `tools/workspace/doxygen_internal`
- `tools/workspace/mkdoc_internal`
- `common`
- `geometry`
- `multibody`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" doc/doxygen_cxx doc/pydrake tools/workspace/doxygen_internal tools/workspace/mkdoc_internal`
- `rg -n "doxygen|sphinx|layout|css|header|toc" doc tools/workspace`
- For docs-generation issues, inspect both generator tooling and the corresponding page policy doc.

## Implementation entry points
- `doc/doxygen_cxx/Doxyfile_CXX.in` | core Doxygen configuration template.
- `doc/doxygen_cxx/DoxygenLayout.xml` | generated docs structural layout.
- `doc/doxygen_cxx/header.html.patch` | Drake-specific Doxygen header customization.
- `doc/doxygen_cxx/doxygen_extra.css` | Drake docs style overrides.
- `doc/pydrake/conf.py` | pydrake Sphinx configuration.
- `doc/pydrake/build.py` | pydrake docs build entrypoint.
- `tools/workspace/doxygen_internal/repository.bzl` | pinned Doxygen toolchain wiring.
- `tools/workspace/doxygen_internal/build_binaries_with_docker` | Doxygen binary build helper.
- `tools/workspace/mkdoc_internal/mkdoc.py` | C++ docstring extraction path.
- `tools/workspace/mkdoc_internal/libclang_setup.py` | libclang setup used by doc extraction.
- `geometry/geometry_infrastructure_doxygen.h` | geometry doxygen infrastructure grouping.
- `geometry/geometry_file_formats_doxygen.h` | geometry file-format docs grouping.
- `geometry/geometry_doxygen.h` | geometry doxygen top-level grouping.
- `solvers/mathematical_program_doxygen.h` | solvers doxygen grouping.
- `planning/planning_doxygen.h` | planning doxygen grouping.
- `multibody/multibody_doxygen.h` | multibody doxygen grouping.
- `common/cxx_doxygen.h` | common C++ docs grouping.
- `multibody/plant/simulation_and_solvers_doxygen.h` | simulation/solver docs grouping.

## Function-level behavior checks
- `doc/doxygen_cxx/test/system_doxygen_test.py` | validates system docs generation behavior.
- `tools/workspace/mkdoc_internal/test/mkdoc_comment_test.py` | validates doc comment extraction behavior.
- `tools/workspace/vtk_internal/test/data_to_header_test.cc` | validates generated header pipeline utility behavior.
