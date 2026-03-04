# drake source map: Build and Install

Generated from source roots:
- `.`
- `setup`
- `tools/install`
- `tools/wheel`
- `tools/workspace`
- `cmake`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" CMakeLists.txt MODULE.bazel setup tools/install tools/wheel tools/workspace cmake`
- `rg -n "install|wheel|cmake|bazel|python" setup tools/install tools/wheel tools/workspace cmake`
- Validate behavior against install/wheel tests before proposing environment-level workarounds.

## Implementation entry points
- `CMakeLists.txt` | top-level CMake integration contract.
- `MODULE.bazel` | Bazel module and dependency topology.
- `setup/install_prereqs` | prerequisite installer entrypoint.
- `tools/install/libdrake/drake-config.cmake.in` | downstream `find_package(Drake)` config template.
- `tools/install/libdrake/generate_version.cmake` | install-time version stamping.
- `tools/workspace/cmake_configure_file.py` | CMake-style configure emulation utility.
- `tools/workspace/default.bzl` | external workspace defaults.
- `tools/workspace/pybind11/pybind11-config.cmake` | pybind11 CMake package integration for source builds.
- `tools/workspace/pybind11/pybind11-config-version.cmake` | pybind11 CMake version compatibility checks.
- `tools/wheel/wheel_builder/main.py` | wheel orchestration entrypoint.
- `tools/wheel/wheel_builder/linux.py` | Linux wheel path.
- `tools/wheel/wheel_builder/macos.py` | macOS wheel path.

## Function-level behavior checks
- `tools/install/test/installer_test.py` | validates installer orchestration behavior.
- `tools/install/libdrake/test/find_package_drake_install_test.py` | validates CMake package discoverability.
- `tools/install/libdrake/test/drake_python_dir_install_test.py` | validates Python install layout.
- `tools/install/libdrake/test/rpath_install_test.py` | validates runtime linker path behavior.
- `tools/wheel/test/tests/sanity-test.py` | validates wheel basic import/runtime behavior.
- `tools/wheel/test/tests/libs-test.py` | validates bundled library resolution.
- `tools/wheel/test/tests/pyi-install-test.py` | validates Python typing artifact installation.
