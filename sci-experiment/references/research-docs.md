# Research Documentation Pattern

Keep the research brief, exploration notes, and run logs separate from each other.

## README.md — the research brief

Written before the experiment runs (hypothesis, method) and updated after (findings, next steps).

Must contain:

- Research question
- Hypothesis and expected outcome
- Method: data, approach, statistical test or model used
- Baseline: what you are comparing against
- Success criterion
- Key findings (after the experiment)
- Known caveats and open questions
- How to reproduce: environment setup, entry point, config to use

Do not mix internal design decisions or change history into the research brief.

## Notebooks — exploration and communication

- Use notebooks to explore, visualise, and communicate results narratively
- Number them: `01_explore`, `02_analysis`, `03_results`
- Each notebook has one purpose — do not combine EDA and modelling in one file
- Keep cells short; each cell should test or show one thing
- Import from `src/` — do not duplicate logic between a notebook and a module
- Clear outputs before committing; regenerable outputs are not source

## Run logs

- Log the full config at the start of every run
- Log each major stage with a timestamp: load, preprocess, train, evaluate
- Log key metrics as they are computed, not just at the end
- Log any skipped samples, violated assumptions, or unexpected data shapes
- Use `YYYY-MM-DD HH:MM:SS UTC` timestamp format consistently

Suggested log baseline for every run:

```
[start]   experiment=<name>  config=<config_path>
[data]    source=<path>  rows=<n>  features=<k>
[stage]   name=<stage>  duration=<s>
[metric]  name=<metric>  value=<v>  split=<train|val|test>
[end]     duration=<total_s>  output=<results_path>
```

## What not to do

- Do not store findings only in a notebook — put them in the README
- Do not commit large result files inline — save to `results/` and reference by path
- Do not use the README as a scratch pad — keep open questions in a separate notes file or notebook cell
