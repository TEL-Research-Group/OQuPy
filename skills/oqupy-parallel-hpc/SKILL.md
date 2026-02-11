---
name: oqupy-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in oqupy; it prioritizes documentation references and then source inspection only for unresolved details.
---

# oqupy: Parallel and HPC

## High-Signal Playbook
- Route the request:
  - "My TEMPO/PT-TEMPO run is too slow / how do I tune dt/tcut/epsrel?" -> use `oqupy-simulation-workflows` (especially `docs/pages/tutorials/parameters.rst`).
  - "How do I scale PT-TEBD (spin chains)?" -> use this skill + `docs/pages/tutorials/pt_tebd.rst` + `oqupy/pt_tebd.py`.
  - "Can I use GPU/JAX?" -> read `docs/pages/jax_features.rst` but validate against the current checkout (see below).
- What parallelism exists in this repo (OQuPy `0.5.0`):
  - TEMPO/PT-TEMPO are primarily single-process in Python; they may still benefit from threaded BLAS underneath NumPy/SciPy.
  - PT-TEBD has an explicit backend knob `backend_config={"parallel": ...}` to parallelize nearest-neighbor gate application via threads/processes (see `oqupy/pt_tebd.py` and `oqupy/backends/pt_tebd_backend.py`).
  - There is no built-in MPI interface in this checkout; for scaling across nodes, use your scheduler (job arrays / multiple tasks) over independent simulations.
- GPU/JAX reality check (important for accuracy):
  - `docs/pages/jax_features.rst` describes a `dev/jax` branch and symbols like `oqupy.backends.enable_jax_features` and `oqupy.backends.numerical_backend.py`.
  - In this checkout, those symbols/files are not present; treat GPU/JAX support as unavailable unless you explicitly switch to a JAX-enabled branch/tag and confirm the code exists.
  - Quick check: `rg -n "enable_jax_features|numerical_backend|OQUPY_BACKEND" oqupy`.
- Minimal working examples:
```python
# PT-TEBD parallelism knob (see oqupy/pt_tebd.py and oqupy/backends/pt_tebd_backend.py)
# Assumes: initial_augmented_mps, system_chain, process_tensors, pt_tebd_params defined.
import oqupy

pt_tebd = oqupy.PtTebd(
    initial_augmented_mps=initial_augmented_mps,
    system_chain=system_chain,
    process_tensors=process_tensors,
    parameters=pt_tebd_params,
    backend_config={"parallel": "multithread"},  # or "multiprocess"
)
results = pt_tebd.compute(num_steps=100, progress_type="bar")
```
- Pitfalls (HPC-specific):
  - Thread oversubscription: if you use PT-TEBD `"multithread"` *and* NumPy/SciPy uses threaded BLAS, you may get worse performance. On HPC, consider setting `OMP_NUM_THREADS=1`, `MKL_NUM_THREADS=1`, `OPENBLAS_NUM_THREADS=1` when you also parallelize at Python level.
  - `"multiprocess"` has higher overhead and requires picklable data; try `"multithread"` first unless profiling shows otherwise.

## Scope
- Handle questions about MPI/OpenMP/GPU execution, scaling, and batch systems.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/pages/jax_features.rst`
- `docs/pages/tutorials/pt_tebd.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `oqupy`

## Source entry points for unresolved issues
- `oqupy/pt_tebd.py`
- `oqupy/backends/pt_tebd_backend.py`
- `oqupy/__init__.py`
- `oqupy/base_api.py`
- `oqupy/version.py`
- `oqupy/util.py`
- `oqupy/tempo.py`
- `oqupy/system_dynamics.py`
- `oqupy/system.py`
- `oqupy/pt_tempo.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" oqupy`).
