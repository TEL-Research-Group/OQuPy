---
name: oqupy-build-and-install
description: This skill should be used when users ask about build and install in oqupy; it prioritizes documentation references and then source inspection only for unresolved details.
---

# oqupy: Build and Install

## High-Signal Playbook
- Route the request:
  - "My simulation is slow / how do I tune parameters?" -> use `oqupy-simulation-workflows`.
  - "How do I run on a cluster / parallelize PT-TEBD?" -> also consult `oqupy-parallel-hpc`.
- Triage questions:
  - Are you installing from PyPI (`pip install oqupy`) or working from a source checkout?
  - Do you need editable installs (development) and test dependencies?
  - Are you on HPC where your NumPy/SciPy BLAS choice matters (MKL/OpenBLAS)?
- Canonical workflow:
  1. Confirm Python version requirement (>= 3.10) per `docs/pages/install.rst`.
  2. Install runtime dependencies from `requirements.txt` (NumPy/SciPy, `tensornetwork==0.4.3`, `h5py`, etc.).
  3. For source checkouts, install editable: `python -m pip install -e .` (uses `setup.py`).
  4. Sanity-check import/version: `python -c "import oqupy; print(oqupy.__version__)"` (expected `0.5.0` in this repo via `oqupy/version.py`).
  5. Run tests (if installed): `python -m pytest -q` (tests in `tests`).

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/pages/install.rst`
- `README.md`
- `DEVELOPMENT.md`
- `requirements.txt`

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
- `setup.py`
- `requirements.txt`
- `requirements_ci.txt`
- `tox.ini`
- `oqupy/version.py`
- `oqupy/__init__.py`
- `oqupy/base_api.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" oqupy`).
