# Feature Pattern

Use a feature package when the work has one or more of these traits:

- customer-facing or business-facing deliverable
- repeatable pipeline or provider workflow
- more than one source module
- prompts, logs, results, or docs need to be maintained
- the output belongs in SCM, not only in a notebook

Default layout:

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

Rules:

- `prompt_templates/` is the canonical prompt location.
- `logs/` and `results/` should exist even if initially empty.
- `src/` contains the reusable implementation, not notebook-only logic.
- `tests/` should cover the stable logic before old code paths are removed.
- `how_to_use_<feature>.ipynb` is required for substantial features.

Adaptation rule:

- If the repo already has a strong package structure, keep it and apply these conventions inside that structure instead of forcing a rewrite.
