---
name: repo-concept-explainer
description: Explain concepts grounded in a repository's actual implementation, data, tests, and architecture. Use when the user asks to understand the what, why, or how of a concept, feature, algorithm, workflow, design choice, formula, code snippet, dataset, sample data, or test path in a repo, especially when they want repo-specific examples, standalone test snippets, mathematical reasoning, or how the concept helps the overall solution.
---

# Repo Concept Explainer

Use this skill to teach a concept from the repository outward. The repo is the primary source of truth; external theory, papers, or general background can support the explanation only after the implementation has been traced.

Optimize for a technical learner who wants rigorous understanding without losing the practical link to the codebase.

## Boundary Conditions

- Start from code, configs, tests, docs, datasets, and sample data in the given repo.
- Ground repo claims with concrete file paths, symbols, commands, and line references when available.
- Separate evidence from inference. Say "the repo shows..." for direct evidence and "this likely means..." for reasoned interpretation.
- Do not invent behavior, intent, metrics, formulas, data semantics, or architecture that the repo does not support.
- If the concept is not implemented in the repo, say that directly, then identify the nearest related files or explain what would need to exist.
- If the repo contains data, inspect schemas, column names, small samples, fixtures, or synthetic examples before explaining data-dependent behavior.
- Avoid exposing secrets, credentials, private customer data, or large raw datasets. Use minimal representative examples and anonymize sensitive values.
- Use external references only when the user asks for broader theory, research grounding, or current context. For precise papers, versions, standards, or "latest" claims, verify with available tools.

## Core Workflow

1. Diagnose the requested concept from natural language, code, file paths, errors, or snippets.
2. Build a quick repo map: read top-level docs, inspect the relevant tree, search with `rg`, and identify code, tests, configs, and data artifacts.
3. Trace the implementation: definitions, callers, class or function boundaries, data flow, state changes, prompts, configs, tests, and scripts.
4. Inspect data when present: file formats, schemas, example rows, fixtures, SQLite tables, JSON fields, or generated samples.
5. Explain the concept using the repo's implementation first, then add scientific or mathematical context where it materially clarifies behavior.
6. Show how to test or exercise the concept standalone with a minimal command, snippet, fixture, or unit-test shape.
7. Connect the concept to the overall solution design: why it exists, what component depends on it, and what breaks if it changes.

Ask at most one clarifying question only when multiple repo concepts could match the user's request and choosing one would be misleading. Otherwise state the assumption and proceed.

## Investigation Checklist

Use the lightest investigation that gives reliable grounding:

- Read `README`, setup docs, and relevant config files before deep diving.
- Use `rg` for concept names, symbol names, error text, prompt text, dataset columns, and code-snippet fragments.
- Locate definitions and callers for key functions, classes, models, schemas, and CLI entrypoints.
- Find tests that already exercise the concept; prefer existing test patterns for standalone examples.
- For notebooks, scripts, or benchmark code, identify inputs, outputs, metrics, and default paths.
- For datasets or databases, inspect schema and a few representative records rather than summarizing the whole dataset.
- Run targeted tests or dry-run commands when safe and useful; report exact commands and whether they passed.

## Explanation Shape

Choose the smallest structure that answers the user, but substantial explanations should include:

- **Concept anchor**: one sentence naming the repo-specific concept and where it appears.
- **What**: what the concept is in this codebase, using concrete symbols and files.
- **Why**: the problem it solves for this repo's use case, not only the generic reason it exists.
- **How**: the implementation path, data flow, algorithm, decision logic, or lifecycle.
- **Repo evidence**: paths, functions, tests, configs, data samples, and commands that support the explanation.
- **Data example**: if sample data exists, walk through a realistic record or fixture and show how the concept acts on it.
- **Formula or reasoning**: include formulas only when they explain behavior, optimization, scoring, probability, complexity, or tradeoffs.
- **Standalone exercise**: provide a minimal code snippet, command, or test that lets the user isolate the concept.
- **Design role**: explain how the concept supports the overall architecture or product behavior.
- **Limits and failure modes**: name assumptions, edge cases, observability gaps, and ways the implementation can fail.

For small questions, answer directly and include only the evidence and one practical test or verification step.

## Formula Pattern

When a mathematical or scientific concept is present, prefer a compact formula card:

- Name: short label.
- Purpose: what the formula measures, predicts, ranks, optimizes, or validates.
- Formula: readable math or ASCII fallback.
- Symbols: define every variable and its source in the repo.
- Repo mapping: point to the implementation, config, or metric that corresponds to each term.
- Tiny example: plug in values from sample data, tests, or a small synthetic case.
- Sensitivity: explain what changes when important terms increase, decrease, or are missing.
- Common misread: call out the likely misconception.

Do not add formulas as decoration. If the repo uses a heuristic rather than a formal formula, explain the heuristic and avoid overstating it.

## Code And Test Snippets

When the user asks how to test a concept standalone:

- Prefer the repo's existing test framework, fixtures, imports, and environment conventions.
- Keep snippets minimal and runnable from the repo root or the relevant package root.
- Include setup only if it is necessary to run the snippet.
- Avoid requiring external services unless the concept inherently depends on them; provide a mock, dry-run, or fixture-based path when available.
- State what output, assertion, state change, or log line proves the concept worked.

When editing files is not requested, provide snippets in the answer rather than modifying the repo.

## Output Quality Bar

Before finishing, check that:

- The explanation starts from the repo, not from generic textbook knowledge.
- Every important repo-specific claim is backed by inspected code, tests, data, docs, or command output.
- The answer covers what, why, and how at the right depth for the user's prompt.
- Any dataset or sample data is used concretely when available.
- Mathematical reasoning is accurate, useful, and mapped back to implementation.
- The standalone test path is realistic for this repo.
- Boundaries, assumptions, and unresolved gaps are explicit.
