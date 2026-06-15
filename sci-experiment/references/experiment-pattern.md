# Experiment Pattern

Use an experiment package when the work has one or more of these traits:

- A defined question or hypothesis to test
- Results that need to be reproducible by someone else
- More than one analysis step or source module
- Outputs (metrics, plots, artefacts) that need to be versioned or shared
- Work that builds on a previous experiment or will be cited by a future one

## Default layout

```text
experiment/<experiment_name>/
  README.md                      ← research brief (question, method, findings)
  notebooks/
    01_explore.ipynb              ← EDA, data understanding
    02_analysis.ipynb             ← main experiment and results
  src/
    data_loader.py
    transforms.py
    model.py
    metrics.py
    visualise.py
  configs/
    experiment.yaml               ← seeds, hyperparameters, paths
  data/
    raw/                          ← immutable original inputs
    processed/                    ← derived, reproducible from raw
  results/
    figures/
    tables/
    artefacts/
  logs/
  tests/
  environment.yml                 ← pinned dependency versions
```

## Rules

- `configs/` is the single source of truth for all parameters — seeds, paths, thresholds, model settings.
- `data/raw/` is immutable. Never write to it after initial acquisition.
- `src/` contains all reusable logic extracted from notebooks. Notebooks import from `src/`, not the reverse.
- `tests/` covers the stable `src/` modules — transforms, metrics, loaders, serialisers.
- `results/` is write-only during a run. Never edit result files manually.
- `environment.yml` must pin exact versions of every dependency that affects numerical output.

## Adaptation rule

If the repository already has an experiment structure (e.g. MLflow project layout, a research monorepo), preserve it and apply these conventions inside that structure instead of forcing a rewrite.
