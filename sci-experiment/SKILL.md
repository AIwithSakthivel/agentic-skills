---
name: sci-experiment
description: Structure, run, and document scientific experiments in Python. Use when designing a new experiment, analysing data, testing a hypothesis, evaluating models, or packaging research findings for team handoff or reproducibility.
---

# Sci-Experiment

Use this skill when the work is a scientific investigation — a question to answer, a hypothesis to test, a model to evaluate, or a dataset to understand. It is not for production systems, ETL pipelines, or application code.

## What This Skill Is For

Any work that follows the cycle of: **question → method → experiment → findings → iterate.**

- Exploratory data analysis (EDA)
- Hypothesis testing and statistical analysis
- Model development, training, and evaluation
- Ablation studies and controlled comparisons
- Literature-backed experiments with a defined baseline
- Research that needs to be reproduced by someone else

## Default Experiment Structure

```text
experiment/<experiment_name>/
  README.md                      ← research brief: question, method, findings
  notebooks/
    01_explore.ipynb              ← EDA, initial data understanding
    02_analysis.ipynb             ← main experiment, results, plots
  src/
    data_loader.py
    transforms.py
    model.py
    metrics.py
    visualise.py
  configs/
    experiment.yaml               ← all parameters, seeds, paths — nothing hardcoded
  data/
    raw/                          ← original, immutable inputs
    processed/                    ← derived, reproducible from raw
  results/
    figures/
    tables/
    artefacts/
  logs/
  tests/
    test_transforms.py
    test_metrics.py
  environment.yml                 ← pinned environment for reproducibility
```

## Operating Rules

- **Start with a question, not with code.** Write the hypothesis and success criterion in the README before writing the first line of code.
- **Configs own all parameters.** Seeds, hyperparameters, file paths, and thresholds live in `configs/`, never hardcoded in `src/` or notebooks.
- **Notebooks are for exploration and communication, not for logic.** Any function called more than once or reused across notebooks belongs in `src/`.
- **Every result needs a baseline.** Never report a metric without something to compare it against — a published result, a naive model, or the previous run.
- **Pin everything that affects reproducibility.** Random seeds, library versions, data snapshots, and model checkpoints.
- **Processed data must be derivable from raw.** Store the transformation code; do not commit large processed artefacts.
- **Preserve the raw data.** `data/raw/` is never modified in place.

## Hypothesis And Research Brief

The `README.md` in each experiment is the research brief. It must answer:

- **Question:** What are you trying to find out?
- **Hypothesis:** What do you expect and why?
- **Method:** What data, model, or statistical test will you use?
- **Baseline:** What does the current best or naive approach achieve?
- **Success criterion:** What result would confirm or refute the hypothesis?
- **Findings:** Filled in after the experiment — key result, whether hypothesis held, caveats.
- **Next steps:** What this experiment opens up or rules out.

## Config Management

- All experiment parameters go in `configs/experiment.yaml` (or `config.py` for code-only setups).
- Changing a hyperparameter is a config change, not a code change.
- Log the full config at experiment start so any run can be reproduced from its log.
- For multi-run sweeps, each run gets its own config snapshot saved alongside its results.

## Reproducibility Checklist

- [ ] Random seed set and logged in config
- [ ] Environment pinned (`environment.yml` or `requirements.txt` with exact versions)
- [ ] All file paths relative or parameterised — no absolute paths in code
- [ ] Processed data generation is scripted and deterministic
- [ ] Results directory timestamped or versioned per run
- [ ] Notebook outputs cleared before committing

## Results And Artefacts

- `results/figures/` — all plots saved programmatically, never screenshot
- `results/tables/` — metric tables as CSV or JSON, not copy-pasted into a document
- `results/artefacts/` — model checkpoints, fitted objects, serialised outputs
- Every result file name should encode what it is: `baseline_accuracy_by_split.csv`, not `output2.csv`
- Log every run: config used, start time, end time, key metrics

## Logging Baseline

Log at minimum:

- Experiment name and full config snapshot
- Data source, version, and sample or row counts
- Run start and end with wall-clock duration
- Each major stage: load, preprocess, train, evaluate
- Key metric values per stage or epoch
- Any warnings, skipped samples, or violated assumptions
- Environment: Python version, key library versions, hardware if relevant

## Notebook Rules

- Number notebooks to indicate sequence: `01_explore`, `02_model`, `03_results`
- Each notebook has one purpose — EDA is separate from modelling, modelling is separate from final results
- Notebooks should run top-to-bottom without errors on a fresh kernel
- Import from `src/` — do not re-implement logic inline in a notebook
- Do not commit large outputs (plots, dataframes) inline — save to `results/` and reference them

## Documentation Rules

- `README.md` is the research brief: the document a colleague reads to understand the experiment without running it
- Notebooks communicate findings visually and narratively
- `src/` functions are documented at the interface level: inputs, outputs, edge cases
- Keep internal design notes and open questions separate from the research brief

## Validation Before Handoff

1. Re-run the full notebook sequence from a clean environment and verify outputs match
2. Confirm the config snapshot produces the reported result deterministically
3. Check that `data/raw/` is untouched
4. Verify `tests/` pass for all `src/` modules
5. State explicitly what was validated, what was not, and any known caveats

## When Not To Use

- Production API, SDK, or library development
- Pure data engineering with no analytical question
- One-off queries or ad-hoc lookups with no findings to document
- General statistics questions that need no experimental structure

## References

- For experiment folder conventions: read `references/experiment-pattern.md`
- For research documentation and logging: read `references/research-docs.md`
- For validation and handoff: read `references/validation-pattern.md`
- For LLM-backed experiment structure: read `references/llm-experiment-pattern.md`

## Typical Requests

- Set up an experiment to test whether feature X improves model performance on dataset Y.
- Extract this EDA notebook into a reproducible experiment with configs and a research brief.
- Add baseline comparison and metric logging to this training script.
- Package this analysis so a colleague can reproduce it from scratch.
- Refactor this research notebook into testable `src/` modules with a clean notebook on top.
