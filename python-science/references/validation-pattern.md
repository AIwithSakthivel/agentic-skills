# Validation Pattern

Default validation order for Python feature work:

1. syntax or import validation
2. focused unit tests
3. mocked integration test when external systems exist
4. only then retire legacy scripts, paths, or artifact locations

Use this pattern:

- Validate source modules first.
- Test the smallest stable interfaces: parsers, config objects, prompt loaders, report writers, path handling, serializers.
- For LLM, DB, or API features, use stubs or mocks for the main integration test.
- If live external validation is not run, say so explicitly.

Handoff should always state:

- what was validated
- what was not validated
- any assumptions used during validation
