---
name: oqupy-api-and-scripting
description: This skill should be used when users ask about api and scripting in oqupy; it prioritizes documentation references and then source inspection only for unresolved details.
---

# oqupy: API and Scripting

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/index.rst`
- `docs/pages/api.rst`
- `docs/pages/tutorials/n_time_correlations.rst`

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
- `oqupy/bath_correlations.py`
- `oqupy/__init__.py`
- `oqupy/base_api.py`
- `oqupy/version.py`
- `oqupy/util.py`
- `oqupy/tempo.py`
- `oqupy/system_dynamics.py`
- `oqupy/system.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" oqupy`).
