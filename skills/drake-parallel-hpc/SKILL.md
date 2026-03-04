---
name: drake-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in drake; it prioritizes documentation references and then source inspection only for unresolved details.
---

# drake: Parallel and HPC

## High-Signal Playbook
### Route Conditions
- Use this skill for performance benchmarking, parallel execution policy, and scaling runs on workstation/server hardware.
- Route to `drake-simulation-workflows` for per-simulation integrator/contact tuning.
- Route to `drake-tools` for build/release tooling internals.
- Route to `drake-troubleshooting` for broad failure triage.

### Triage Questions
- Are you optimizing throughput, latency, memory, or realtime rate?
- Is the workload single-run simulation, parameter sweep, or benchmark suite?
- Which backend is limiting: CPU parallelism, Python overhead, or solver/runtime config?
- Do you need reproducible benchmark artifacts (`--output_dir` etc.)?

### Canonical Workflow
1. Start with benchmark docs (`tools/performance/README.md`, `systems/benchmarking/README.md`, `multibody/benchmarking/README.md`).
2. Run a baseline benchmark with default flags.
3. Change one axis at a time (threads, repetitions, affinity, benchmark target).
4. Record outputs and machine metadata for fair comparison.
5. Escalate to source-level analysis only after stable reproduction.

### Minimal Working Example
```bash
bazel run //multibody/benchmarking:cassie_experiment -- --output_dir=trial1
bazel run //multibody/benchmarking:cassie -- --help
bazel run //systems/benchmarking:framework_benchmarks
```

### Pitfalls and Fixes
- Cross-machine benchmark comparisons are often misleading; compare runs from the same host/environment (`multibody/benchmarking/README.md`).
- Background load and CPU throttling can dominate variance; keep machine state controlled.
- Parallel scaling can regress silently when reproducibility metadata is missing.

### Convergence and Validation Checks
- Benchmark output files are produced and versioned by run conditions.
- Repeated runs under fixed settings have acceptable variance.
- Parallelism-sensitive checks (`openmp`, solver parallel tests) are passing.

### Source-Code Handoff
- Benchmark harness: `tools/performance/benchmark_tool.py`, `tools/performance/gflags_main.cc`, `tools/performance/fixture_common.cc`.
- Parallel policy primitives: `common/parallelism.h`, `common/parallelism.cc`.
- Runtime rate tracking: `systems/analysis/realtime_rate_calculator.h`, `systems/analysis/realtime_rate_calculator.cc`.
- Representative benchmark targets: `systems/benchmarking/framework_benchmarks.cc`, `multibody/benchmarking/cassie.cc`, `geometry/benchmarking/render_benchmark.cc`.

## Scope
- Handle questions about execution scaling and benchmark workflows.
- Keep advice measurable and experiment-driven.

## Primary documentation references
- `tools/performance/README.md`
- `systems/benchmarking/README.md`
- `multibody/benchmarking/README.md`
- `geometry/benchmarking/README.md`
- `doc/_pages/profiling.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If ambiguity remains after docs, inspect `references/source_map.md`.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `common/test/parallelism_test.cc`
- `common/test/openmp_test.cc`
- `systems/analysis/test/realtime_rate_calculator_test.cc`
- `solvers/test/solve_in_parallel_test.cc`

## Optional deeper inspection
- `tools/performance`
- `systems/benchmarking`
- `multibody/benchmarking`
- `geometry/benchmarking`
- `common`
- `systems/analysis`

## Source entry points for unresolved issues
- `tools/performance/gflags_main.cc`
- `tools/performance/benchmark_tool.py`
- `tools/performance/fixture_common.cc`
- `common/parallelism.h`
- `common/parallelism.cc`
- `systems/analysis/realtime_rate_calculator.h`
- `systems/analysis/realtime_rate_calculator.cc`
- `systems/benchmarking/framework_benchmarks.cc`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" tools/performance common systems multibody geometry`).
