---
name: oqupy-advanced-topics
description: This skill should be used for low-frequency documentation topics in oqupy (sharing, citation, bibliography, and style/graphics guidance); it prioritizes documentation references and only inspects source when needed.
---

# oqupy: Advanced Topics

## Scope
- Handle low-frequency, docs-centric topics:
  - project sharing and citation guidance
  - bibliography and BibTeX references
  - graphics/style guidance used in docs assets
- Keep this as a routing skill. For simulation, API, install, and performance questions, route to the dedicated core skills.

## Route the request
- Simulation setup/performance tuning -> `oqupy-simulation-workflows`
- Parallel/HPC execution -> `oqupy-parallel-hpc`
- API/code behavior -> `oqupy-api-and-scripting`
- Citation/sharing/branding/style docs -> stay in this skill

## Primary documentation references
- `docs/pages/sharing.rst`
- `docs/pages/how_to_cite.rst`
- `docs/pages/bibliography.rst`
- `docs/graphics/oqupy-style-guide.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the full inventory in this merged topic.
- Use source inspection only for unresolved implementation questions and start from `references/source_map.md`.
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
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" oqupy`).
