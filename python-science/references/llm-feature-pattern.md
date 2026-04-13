# LLM Feature Pattern

For LLM-backed Python features:

- store prompts in `prompt_templates/`
- keep prompt loading separate from prompt usage
- isolate external clients behind a small provider or interface
- keep config and path handling explicit
- keep report writers, artifact writers, and analyzers separate

Common module split:

- `config.py`
- `models.py`
- `prompt_loader.py`
- `provider.py` or `pipeline.py`
- domain modules such as analyzers, parsers, writers, evaluators

Default logs for LLM-backed features:

- model name
- prompt or stage name
- input artifact path
- output artifact path
- row or record counts
- warnings, retries, and failures

Testing pattern:

- unit test prompt loading and path resolution
- mock the LLM for integration-style tests
- validate generated reports or outputs with deterministic fixtures
