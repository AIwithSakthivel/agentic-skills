# LLM Experiment Pattern

For experiments that use a language model as part of the analysis — e.g. using an LLM to label data, extract information, generate hypotheses, evaluate outputs, or run a prompt-based benchmark.

## Key principles

- Treat the LLM as a stochastic external service — isolate it behind a provider interface so you can swap models, mock it in tests, and log its behaviour
- Store all prompts in `configs/prompts/` or a dedicated `prompt_templates/` directory — never inline in Python
- Temperature, model name, max tokens, and sampling parameters belong in `configs/`, not hardcoded
- Log every LLM call: model name, prompt name or hash, input token count, output token count, latency, any retry or failure

## Directory addition for LLM experiments

```text
experiment/<experiment_name>/
  ...
  configs/
    experiment.yaml
    prompts/
      extract.txt
      evaluate.txt
  src/
    prompt_loader.py
    llm_provider.py          ← wraps the API client; all experiments call this
    ...
```

## Module responsibilities

- `prompt_loader.py` — loads prompt text from file, substitutes variables, returns a string. No model calls here.
- `llm_provider.py` — wraps the API client, handles retries, rate limits, and error logging. Returns raw model output.
- Domain modules (analysers, evaluators, parsers) call `llm_provider`, never the API client directly.

## Reproducibility constraints for LLM experiments

- Set `temperature=0` (or the model's equivalent) for deterministic outputs when reproducibility matters
- Log the exact model version, not just the model family — model updates change outputs
- If non-deterministic outputs are intentional (e.g. sampling diversity), log the seed and document that results will vary
- Cache LLM outputs where re-running is expensive; store cached responses alongside results

## Testing pattern

- Unit-test `prompt_loader.py` with fixture templates — verify variable substitution
- Mock `llm_provider.py` in all unit and integration tests — never call the real API in automated tests
- Validate outputs with deterministic fixtures: given a known LLM response, does the downstream parser produce the expected result?
- If live API validation is run, say so explicitly and log the model version used
