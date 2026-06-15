# Validation Pattern

Default validation order for scientific experiment work:

1. Validate `src/` modules in isolation (import, unit tests)
2. Validate data loading and transforms against known fixtures
3. Sanity-check statistical assumptions before running the full analysis
4. Run the full experiment on a small data slice first
5. Compare outputs against the stated baseline before reporting results
6. Only then archive or share the experiment

## Validate source modules first

- Test the smallest stable units: data loaders, transform functions, metric calculations, visualisation helpers
- Use deterministic fixtures — a small, known dataset whose expected output you can compute by hand or from a reference implementation
- If a transform changes a number, write a test that asserts the exact change

## Sanity-check statistical assumptions

Before running the main analysis, check:

- Data distributions are as expected (no unexpected nulls, outliers, or class imbalance)
- The baseline metric on the validation split is consistent with published or historical values
- Random seed produces the same split and the same initialisation on each run

## Scale before you commit

Run the full pipeline on a 10% or representative sample first:

- Catch shape errors, dtype mismatches, and configuration mistakes cheaply
- Verify the results directory is populated and named correctly
- Confirm the log is complete before committing to a full run

## Handoff states what was and was not validated

Every experiment handoff or README findings section must state:

- What was validated (tests passed, manual checks run, baseline confirmed)
- What was not validated (e.g. "not tested on the held-out test set", "live API not called in CI")
- Any assumptions made during validation (e.g. "assumed class balance is representative")
- Whether the full environment was reproduced or only the local dev environment was tested
