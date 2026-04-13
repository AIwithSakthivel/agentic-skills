---
name: python-science
description: Build deployable Python data-science features for customer use cases. Use when turning scripts, notebooks, evaluation flows, providers, or LLM/data workflows into SCM-ready modules with feature folders, src/tests/logs/results/prompt_templates, delivery README, internal workbook, and how-to notebooks.
---

# Python Science

Use this skill when the work is a real deliverable that belongs in source control, not a one-off script or notebook.

## Default Outcome

- Prefer a feature package for substantial or customer-facing work.
- Default feature layout:

```text
feature/<feature_name>/
  README.md
  workbook/
  prompt_templates/
  src/
  tests/
  results/
  logs/
  data/
  how_to_use_<feature>.ipynb
```

- Keep delivery README separate from the internal workbook.
- Always place prompts in `prompt_templates/`.
- Always create `logs/` and `results/`.
- Always create `how_to_use_<feature>.ipynb` that initializes the feature and runs it with sample data paths.

## Operating Rules

- Understand the existing repo first. If the repo already has a stronger package convention, preserve it and map these defaults into that structure.
- Prefer modular Python packages over monolithic scripts. Common modules include `config.py`, `models.py`, `provider.py` or `pipeline.py`, `prompt_loader.py`, domain modules, writers, and validators.
- Wrap LLM, DB, API, or filesystem-heavy behavior behind small interfaces so tests can stub or mock them.
- Move durable logic out of notebooks and into `src/`. Use notebooks for onboarding, invocation, and quick validation only.
- For delivery work, do not leave long-lived prompts inline in Python modules.
- Validate the new path before retiring legacy scripts or old artifact locations.

## Logging And Traceability

- `logs/` and `results/` must exist for every substantial feature.
- Maintain an internal workbook with timestamped entries for material implementation and validation steps.
- If log requirements are not specified and you are in Plan Mode, ask what should be logged before finalizing the plan.
- If log requirements are not specified and you are not in Plan Mode, use this default baseline and state the assumption:
  - run start and end
  - input and output artifact paths
  - row, record, or file counts
  - major pipeline stage completion
  - warnings and errors
  - model and prompt usage for LLM-backed features

## Docs And Notebook Rules

- `README.md` is delivery-facing: feature purpose, inputs, outputs, dependencies, public API, and usage.
- Workbook is internal: design notes, decisions, timestamped work log, validation notes, and future follow-ups.
- `how_to_use_<feature>.ipynb` should show:
  - imports and setup
  - config initialization
  - invocation with data paths
  - inspection of primary outputs
- Keep the notebook deterministic and usage-focused, not exploratory.

## Validation Pattern

- Run syntax or import validation for new Python modules.
- Add focused unit tests for parsing, config, I/O, or business logic.
- Add a mocked integration path when external services exist.
- Summarize what was validated and what was not.

## When Not To Use

- Tiny one-off Python fixes
- Pure EDA or notebook exploration with no productization request
- General math or statistics questions that do not need feature structure

## References

- For feature folder conventions: read `references/feature-pattern.md`
- For README, workbook, and logging separation: read `references/docs-and-logbook.md`
- For Python validation flow: read `references/validation-pattern.md`
- For LLM-backed feature structure: read `references/llm-feature-pattern.md`

## Typical Requests

- Turn this experiment script into a deployable Python feature.
- Build a customer use-case module with tests, prompts, logs, results, and a usage notebook.
- Refactor this evaluation or provider workflow into a modular feature package.
