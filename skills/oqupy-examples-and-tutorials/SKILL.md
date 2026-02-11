---
name: oqupy-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in oqupy; it prioritizes documentation references and then source inspection only for unresolved details.
---

# oqupy: Examples and Tutorials

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/pages/tutorials/pt_tempo.rst`
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
- `oqupy/tempo.py`
- `oqupy/pt_tempo.py`
- `oqupy/pt_tebd.py`
- `oqupy/backends/tempo_backend.py`
- `oqupy/backends/pt_tempo_backend.py`
- `oqupy/backends/pt_tebd_backend.py`
- `oqupy/__init__.py`
- `oqupy/base_api.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" oqupy`).
