---
name: oqupy-simulation-workflows
description: This skill should be used when users ask about simulation workflows in oqupy; it prioritizes documentation references and then source inspection only for unresolved details.
---

# oqupy: Simulation Workflows

## High-Signal Playbook
- Route the request:
  - Parameter/convergence tuning for TEMPO/PT-TEMPO (dt/tcut/dkmax/epsrel, dkmax anomaly, `unique=True`) -> use this skill + `docs/pages/tutorials/parameters.rst`.
  - Time-dependent systems and reuse across many Hamiltonians/controls -> PT-TEMPO workflow in `docs/pages/tutorials/pt_tempo.rst`.
  - Spin chains / many-body with environments -> PT-TEBD workflow in `docs/pages/tutorials/pt_tebd.rst` + parallel knobs in `oqupy/pt_tebd.py`.
  - Cluster execution / parallelism questions -> also consult `oqupy-parallel-hpc`.
- Triage questions (answer before optimizing):
  - Which method: TEMPO, PT-TEMPO, PT-TEBD, mean-field TEMPO?
  - Single run vs many runs over different controls/parameters (prefer PT-TEMPO + reuse)?
  - What time window and time resolution do you need (`start_time`, `end_time`, target `dt`)?
  - What is the bath memory timescale (how big does `tcut` need to be)?
  - What observable(s) define "converged enough"?
  - Are you limited by RAM (bond dimensions / PT size) or wall time (SVD/compressions)?
- Canonical workflow (performance-first, correctness-preserving):
  1. Start from a minimal runnable model (system, bath, initial state) using `docs/pages/tutorials/quickstart.rst`.
  2. Get a *starting point* for compute parameters with `oqupy.guess_tempo_parameters(...)` (see `docs/pages/tutorials/parameters.rst`), then plan a convergence sweep.
  3. Establish a reasonable memory cutoff (`tcut` or `dkmax`) first; cost scales roughly linearly with `dkmax` (see `docs/pages/tutorials/parameters.rst`).
  4. With `tcut` fixed, converge `dt` (Trotter error) and `epsrel` (compression error). Expect smaller `dt` and smaller `epsrel` to increase runtime.
  5. If bath coupling has degeneracies, try `unique=True` for speedups (see `docs/pages/tutorials/parameters.rst` and `oqupy/tempo.py` / `oqupy/pt_tempo.py`).
  6. If you need many different system Hamiltonians/controls with the *same* bath: compute a process tensor once via `oqupy.pt_tempo_compute(...)`, then reuse it in `oqupy.compute_dynamics(...)` (see `docs/pages/tutorials/pt_tempo.rst`).
  7. For large PTs, write them to disk during computation via `process_tensor_file=...` (HDF5) and/or reuse them later via `oqupy.import_process_tensor(...)` (see `oqupy/pt_tempo.py` and `oqupy/process_tensor.py`).
  8. For chains, compute the needed process tensor(s) and run `oqupy.PtTebd(...)` (see `docs/pages/tutorials/pt_tebd.rst`).
  9. For batch sweeps, reduce overhead with `progress_type="silent"` (TEMPO/PT-TEMPO/compute_dynamics).
- Minimal working examples:
```python
# TEMPO with parameter guessing (docs/pages/tutorials/parameters.rst)
import oqupy

sx = oqupy.operators.sigma("x")
sz = oqupy.operators.sigma("z")
system = oqupy.System(0.5 * 1.0 * sx)
corr = oqupy.PowerLawSD(alpha=0.3, zeta=1, cutoff=5.0, cutoff_type="exponential")
bath = oqupy.Bath(0.5 * sz, corr)

t0, t1 = 0.0, 15.0
guess = oqupy.guess_tempo_parameters(bath=bath, start_time=t0, end_time=t1, tolerance=1e-2)
params = oqupy.TempoParameters(dt=guess.dt, dkmax=guess.dkmax, epsrel=guess.epsrel)
rho0 = oqupy.operators.spin_dm("z+")

dyn = oqupy.tempo_compute(system, bath, rho0, t0, t1, parameters=params, unique=True, progress_type="bar")
```

```python
# PT-TEMPO to HDF5 + reuse for many systems (docs/pages/tutorials/pt_tempo.rst)
# Assumes: system, bath, params, rho0, t0, t1 already defined.
import oqupy

_ = oqupy.pt_tempo_compute(
    bath=bath, start_time=t0, end_time=t1, parameters=params,
    process_tensor_file="pt.hdf5", overwrite=True, progress_type="bar",
)
pt = oqupy.import_process_tensor("pt.hdf5")  # file-backed PT, avoids recomputation

dyn = oqupy.compute_dynamics(
    system=system, initial_state=rho0, start_time=t0,
    process_tensor=pt, progress_type="silent",
)
```
- Pitfalls (common performance killers):
  - `tcut=None` / `dkmax=None` disables the finite-memory approximation and can become infeasible for long runs (see `docs/pages/tutorials/parameters.rst`).
  - Smaller `dt` increases step count; for fixed `tcut`, it also increases `dkmax = tcut/dt`, often amplifying cost more than expected (see `docs/pages/tutorials/parameters.rst`).
  - PT-TEMPO can require *different* parameter convergence than TEMPO; do not assume TEMPO convergence implies PT convergence (see `docs/pages/tutorials/parameters.rst`).
  - "dkmax anomaly": some cases run slower for intermediate `dkmax`; if you hit this, start from `dkmax=None` and work *downwards* (see `docs/pages/tutorials/parameters.rst`).
  - For time-dependent systems, keep an eye on `subdiv_limit` / `liouvillian_epsrel` if propagator integration dominates (see `docs/pages/tutorials/parameters.rst` and `oqupy/system.py`).
- Convergence/validation checklist (quick, practical):
  - Increase `tcut` (or `dkmax`) until observables stop changing on your time window.
  - Halve `dt` and compare; if it changes, you are Trotter-error limited.
  - Decrease `epsrel` by 10x and compare; if it changes, you are truncation-error limited.
  - Inspect bond dimensions (TEMPO/PT-TEMPO/PT-TEBD) for runaway growth; that is usually the first indicator of infeasibility.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/pages/tutorials/parameters.rst`
- `docs/pages/tutorials/quickstart.rst`
- `docs/pages/tutorials/pt_tempo.rst`
- `docs/pages/tutorials/pt_tebd.rst`
- `docs/pages/modules.rst`

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
- `oqupy/tempo.py`
- `oqupy/pt_tempo.py`
- `oqupy/system_dynamics.py`
- `oqupy/process_tensor.py`
- `oqupy/pt_tebd.py`
- `oqupy/__init__.py`
- `oqupy/base_api.py`
- `oqupy/version.py`
- `oqupy/util.py`
- `oqupy/backends/tempo_backend.py`
- `oqupy/backends/pt_tempo_backend.py`
- `oqupy/backends/pt_tebd_backend.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" oqupy`).
