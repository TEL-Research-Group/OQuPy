# oqupy source map: Simulation Workflows

Generated from source roots:
- `oqupy`

Use this map only after exhausting the topic docs in `./doc_map.md`.

## Topic query tokens
- `add_correlation_time`
- `dynamics`
- `dkmax`
- `dt`
- `epsrel`
- `export`
- `guess_tempo_parameters`
- `integrator`
- `import_process_tensor`
- `modules`
- `pages`
- `pipeline`
- `process_tensor_file`
- `progress_type`
- `pt_tebd`
- `pt_tempo`
- `pt_tempo_compute`
- `PtTebd`
- `PtTebdParameters`
- `Tempo`
- `TempoParameters`
- `run`
- `simulation`
- `step`
- `time`
- `tcut`
- `unique`
- `workflow`
- `workflows`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" oqupy`
- `rg -n "class|def|struct|namespace" oqupy`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `oqupy/tempo.py` | score: 10 | matched tokens: Tempo, TempoParameters, guess_tempo_parameters, dt, dkmax, tcut, epsrel, unique
- `oqupy/pt_tempo.py` | score: 10 | matched tokens: pt_tempo, pt_tempo_compute, process_tensor_file, unique
- `oqupy/system_dynamics.py` | score: 10 | matched tokens: dynamics, compute_dynamics, progress_type
- `oqupy/process_tensor.py` | score: 10 | matched tokens: export, import_process_tensor
- `oqupy/pt_tebd.py` | score: 8 | matched tokens: pt_tebd, PtTebd, PtTebdParameters, backend_config
- `oqupy/backends/pt_tebd_backend.py` | score: 7 | matched tokens: pt_tebd, parallel
- `oqupy/backends/pt_tempo_backend.py` | score: 6 | matched tokens: pt_tempo, backend
- `oqupy/backends/tempo_backend.py` | score: 6 | matched tokens: tempo
- `oqupy/util.py` | score: 6 | matched tokens: progress_type
- `oqupy/dynamics.py` | score: 5 | matched tokens: dynamics
- `oqupy/bath_dynamics.py` | score: 5 | matched tokens: dynamics
- `oqupy/__init__.py` | fallback entry point
- `oqupy/base_api.py` | fallback entry point
- `oqupy/version.py` | fallback entry point
- `oqupy/system.py` | fallback entry point
- `oqupy/operators.py` | fallback entry point
- `oqupy/mps_mpo.py` | fallback entry point
- `oqupy/helpers.py` | fallback entry point
- `oqupy/gradient.py` | fallback entry point
- `oqupy/control.py` | fallback entry point
- `oqupy/config.py` | fallback entry point
- `oqupy/bath_correlations.py` | fallback entry point
- `oqupy/bath.py` | fallback entry point
- `oqupy/backends/__init__.py` | fallback entry point
- `oqupy/backends/node_array.py` | fallback entry point
