---
name: oqupy-developer-guide
description: This skill should be used when users ask about developer guide in oqupy; it prioritizes documentation references and then source inspection only for unresolved details.
---

# oqupy: Developer Guide

## Scope
- Handle questions about developer architecture, extension points, and contribution workflow.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/pages/authors.rst`
- `docs/pages/contributing.rst`

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
- `oqupy/__init__.py`
- `oqupy/base_api.py`
- `oqupy/version.py`
- `oqupy/util.py`
- `oqupy/tempo.py`
- `oqupy/system_dynamics.py`
- `oqupy/system.py`
- `oqupy/pt_tempo.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" oqupy`).
