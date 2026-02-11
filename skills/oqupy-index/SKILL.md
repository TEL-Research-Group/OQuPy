---
name: oqupy-index
description: This skill should be used when users ask how to use oqupy and the correct generated documentation skill must be selected before going deeper into source code.
---

# oqupy Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.
- Performance routing:
  - Convergence/performance knobs for TEMPO/PT-TEMPO/PT-TEBD (dt/tcut/dkmax/epsrel, PT reuse, file-backed process tensors) -> `oqupy-simulation-workflows`.
  - Parallel execution and scaling (PT-TEBD parallel backend config, cluster job patterns) -> `oqupy-parallel-hpc`.

## Generated topic skills
- `oqupy-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `oqupy-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `oqupy-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `oqupy-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `oqupy-developer-guide`: Developer Guide (developer architecture, extension points, and contribution workflow)
- `oqupy-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `oqupy-parallel-hpc`: Parallel and HPC (MPI/OpenMP/GPU execution, scaling, and batch systems)
- `oqupy-advanced-topics`: Advanced Topics (sharing/citation/bibliography/graphics-style docs and other low-frequency docs topics)

## Documentation-first inputs
- `docs`

## Tutorials and examples roots
- `examples`
- `tutorials`

## Test roots for behavior checks
- `tests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, search the topic skill `references/doc_map.md`.
- If documentation still leaves ambiguity, open `references/source_map.md` inside the same topic skill and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" oqupy`).

## Source directories for deeper inspection
- `oqupy`
