# drake source map: Parallel and HPC

Generated from source roots:
- `tools/performance`
- `common`
- `systems/analysis`
- `systems/benchmarking`
- `multibody/benchmarking`
- `geometry/benchmarking`
- `solvers/test`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" tools/performance common systems/analysis systems/benchmarking multibody/benchmarking geometry/benchmarking`
- `rg -n "benchmark|parallel|openmp|realtime|threads" tools/performance common systems multibody geometry`
- Compare behavior across repeated runs under fixed settings before interpreting regressions.

## Implementation entry points
- `tools/performance/gflags_main.cc` | benchmark binary argument and startup handling.
- `tools/performance/benchmark_tool.py` | benchmark orchestration helper.
- `tools/performance/fixture_common.cc` | shared benchmark fixture behavior.
- `common/parallelism.h` | parallelism API/contract.
- `common/parallelism.cc` | parallelism implementation and policy.
- `systems/analysis/realtime_rate_calculator.h` | realtime-rate API for run performance.
- `systems/analysis/realtime_rate_calculator.cc` | realtime-rate implementation.
- `systems/benchmarking/framework_benchmarks.cc` | systems benchmark scenarios.
- `multibody/benchmarking/cassie.cc` | multibody benchmark workload.
- `geometry/benchmarking/render_benchmark.cc` | geometry benchmark workload.

## Function-level behavior checks
- `common/test/parallelism_test.cc` | validates parallelism API behavior.
- `common/test/openmp_test.cc` | validates OpenMP availability/behavior.
- `systems/analysis/test/realtime_rate_calculator_test.cc` | validates runtime rate calculations.
- `solvers/test/solve_in_parallel_test.cc` | validates parallel solve execution behavior.
