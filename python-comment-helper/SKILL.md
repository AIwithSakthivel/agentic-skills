---
name: python-comment-helper
description: improve python comments and docstrings through a shipping-quality documentation pass. use when the user asks to comment python code, add or revise module/class/function/method docstrings, clean up noisy comments, prepare code comments for codex or code review, convert comments to google style, or document source, helper, utility, service, or library files. focuses on code-grounded documentation that explains intent, contracts, side effects, edge cases, and constraints while avoiding invented behavior, filler docstrings, and comments that restate code.
---

# Python Comment Helper

## Goal

Perform a shipping-quality documentation pass for Python code. Generic tools add comments; this skill improves documentation quality by adding only useful Google-style docstrings and comments, removing or avoiding noise, preserving behavior, and making unsupported assumptions explicit.

Use docstrings to document APIs. Use comments to explain intent. Avoid comments that simply restate code. Prefer clear, code-grounded documentation over polished but vague wording.

## Default Output

When the user provides Python code, edit the code directly unless they ask only for advice. Return the revised code first, then include a short documentation pass summary when useful.

When reviewing or writing comments for Python code, produce:

1. Revised code snippets with module, class, function, or method docstrings where appropriate.
2. Inline or block comments only where they explain non-obvious intent, constraints, side effects, tradeoffs, safety assumptions, compatibility issues, or performance choices.
3. A concise documentation pass summary after editing a full file or meaningful snippet.

Do not only add comments. Improve documentation quality by removing, replacing, or avoiding comments that are redundant, stale, vague, or unsupported by the code.

## Core Standard

Use this hierarchy:

- Use a module docstring at the top of a shipped Python file to explain the file's responsibility and scope.
- Use class docstrings for public classes and non-obvious internal classes.
- Use function and method docstrings for public APIs, complex behavior, non-obvious side effects, validation, exceptions, returned values, or branch-specific behavior.
- Skip docstrings for tiny private helpers when the function name and type hints are self-explanatory.
- Use inline or block comments only for non-obvious intent, tradeoffs, workarounds, security assumptions, compatibility constraints, or performance choices.
- Delete, avoid, or flag comments that merely translate Python into English.

## Code-Grounded Documentation Rules

Every docstring must be grounded in behavior visible from the code or context supplied by the user.

Do not write polished but generic docstrings. Avoid vague phrases such as:

- "initializes the instance"
- "handles the request"
- "processes the data"
- "manages runtime configuration"
- "validates dependencies"
- "performs the operation"
- "returns the result"

Replace vague wording with the actual contract visible in the code: what is read, created, delegated, mutated, returned, skipped, raised, or preserved.

For public functions and methods, document the useful contract:

- What the function does.
- Important arguments when their role is not obvious.
- The return value when meaningful.
- Special branches such as empty input, fallbacks, skipped work, mutation, retries, external calls, caching, lazy imports, or error paths.
- Side effects such as file writes, network calls, state mutation, logging, environment-variable reads, or LLM/tool calls. When a function mutates multiple external objects in place (e.g. both a result object and a state object), name the mutations explicitly in the docstring even if the summary line is a one-liner — a reader must not have to read the body to discover that external state changed.

If a function has a meaningful branch, document the branch. For example, if empty input avoids state mutation or external calls, say that in the docstring rather than only adding an inline comment.

### Dict returns, string enums, and mutation side effects

These three patterns are the most common places where a one-liner is insufficient but a naive pass will leave sections out.

**Dict returns with domain-specific keys** — `-> dict` in the type hint tells a reader nothing about the keys. Always add a `Returns:` section that lists the keys.

Bad:
```python
def run_job(name: str, config: dict) -> dict:
    """Runs the named job and returns execution metadata."""
```

Better:
```python
def run_job(name: str, config: dict) -> dict:
    """Runs the named job and returns execution metadata.

    Returns:
        Dict with keys: job_id, status, start_time, end_time,
        output_path, error_message.
    """
```

**String enum parameters with a ValueError** — when a function raises `ValueError` to enforce valid string choices, that exception IS the documentation of the input contract. Always surface it in `Raises:`.

Bad:
```python
def export(data: list, fmt: str) -> bytes:
    """Exports data in the requested format."""
```

Better:
```python
def export(data: list, fmt: str) -> bytes:
    """Exports data in the requested format.

    Raises:
        ValueError: If fmt is not one of: json, csv, parquet.
    """
```

**Multiple external mutations** — when a function mutates more than one external object in place, the one-liner cannot carry the full side-effect contract. Name the mutated objects explicitly.

Bad:
```python
def close_session(session, registry) -> None:
    """Closes the session and removes it from the registry."""
```

Better:
```python
def close_session(session, registry) -> None:
    """Closes the session and removes it from the registry.

    Mutates session.status to "closed" and removes the session
    entry from registry in place.
    """
```

### Name the mechanism, not just the outcome

When a function's ranking, inference, scoring, or transformation algorithm is what maintainers need to understand, name it in the summary line rather than describing only the output.

Bad:

```python
"""Ranks EDUs for retrieval."""
```

Better:

```python
"""Ranks EDUs by token overlap with indexed slot-fact text."""
"""Ranks EDUs by exact slot/entity matches and session continuity."""
```

The better versions tell a reader *how* to reason about the scores, which matters for debugging and modification.

### Verb precision

Choose verbs that reflect the nature of the operation, not just its output:

- **Infers** — output is derived through logic or heuristics, not fetched directly.
- **Rebuilds** — clears and repopulates state entirely, not an incremental update.
- **Creates** — brings data structures into existence; prefer over "initializes" for `__init__` on data-holding classes.
- **Returns** — simple reads and pure transformations.
- **Combines** — merges inputs into a new output.

The verb is often the most information-dense word in the summary line. Choose it deliberately.

### Domain compression

Use precise domain terms without paraphrasing them. Readers of domain code gain more from "reciprocal-rank fusion" or "sparse and symbolic retrieval" than from a prose explanation of those terms. Do not replace domain vocabulary with generic descriptions to appear accessible — that degrades precision without improving clarity.

## Anti-Invention Rule

Never invent business purpose, product intent, side effects, persistence behavior, security guarantees, performance guarantees, API contracts, ownership, lifecycle behavior, operational assumptions, validation, caching, idempotency, thread-safety, or storage behavior that is not supported by the code or by user-provided context.

Be especially careful with words such as "validated", "secure", "safe", "optimized", "cached", "persistent", "thread-safe", "idempotent", "production-ready", "runtime configuration", and "database-safe". Use them only when the code clearly implements that behavior or the user supplies that context.

When behavior is clear from code, document the actual behavior precisely. When intent is ambiguous, either use neutral wording or call out the uncertainty in the documentation pass summary instead of guessing.

Bad:

```python
def normalize_name(name: str) -> str:
    """Normalizes a customer name for database-safe storage."""
    return name.strip().lower()
```

Better:

```python
def normalize_name(name: str) -> str:
    """Returns the name with surrounding whitespace removed and lowercase applied."""
    return name.strip().lower()
```

The bad version invents customer and storage intent. The better version documents only what the code does.

Bad:

```python
def __init__(self, llm, loader=None) -> None:
    """Initializes the instance with validated dependencies and runtime configuration."""
```

Better:

```python
def __init__(self, llm, loader=None) -> None:
    """Initializes a session with the language model and API loader dependencies."""
```

The bad version invents validation and uses filler wording. The better version documents the visible dependency contract.

## Docstring Format

Default to a single summary sentence ending with a period. Add `Args`, `Returns`, and `Raises` sections only when the summary line genuinely cannot carry the contract — not because the function has multiple parameters or returns a value. A tight one-liner is better than a padded multi-section docstring.

Prefer a one-liner even for complex public methods when parameter names and type hints already convey meaning:

```python
"""Ranks EDUs by token overlap with indexed slot-fact text."""
```

Use sections when:

- A parameter's role is not obvious from its name and type hint alone.
- The return value has special conditions, a non-obvious type, or multiple outcomes.
- An exception is reliably raised by operations the function explicitly performs.

When sections are warranted, use Google style:

```python
def get_port(env_var: str = "REDWOOD_DEMO_PORT", default: int = 8788) -> int:
    """Returns the configured server port.

    Args:
        env_var: Name of the environment variable containing the port.
        default: Port to use when the environment variable is unset.

    Returns:
        The validated TCP port.

    Raises:
        ValueError: If the configured value is not a valid port number.
    """
```

Only include sections that are actually useful. Do not add empty or redundant `Args`, `Returns`, or `Raises` sections.

Add `Args` when a parameter's role is not obvious from its name and type hint alone — not simply because the function has multiple parameters or optional behavior. Always add `Args` for untyped parameters (e.g. bare `llm`) where the expected interface is not inferable, and for string parameters that accept only specific values (string enums).

Add `Returns` when any of these are true:
- The return type is `dict` and the keys are domain-specific (a reader cannot know the key names from the signature alone).
- The return type is a typed schema, dataclass, or named tuple whose relevant fields are not obvious.
- There is a special-case return: early `None`, an empty-string sentinel, a fallback value, or a non-mutating short-circuit.
- The return type hint alone (`-> dict`, `-> list`, `-> str`) does not tell a reader what to expect from the value.

Add `Raises` when:
- A `ValueError` or similar exception documents valid string choices for a parameter — this is the primary documentation of the valid input set, not an implementation detail.
- An exception is explicitly raised or reliably implied by an operation the function intentionally performs.
Do not invent exceptions that the code does not raise.

## Module Docstrings

For shipped files, add a top-level docstring that explains responsibility and scope. Module docstrings always use multi-line format: a summary sentence on the first line, a blank line, an elaboration body, and the closing `"""` on its own line. Never compress a module docstring onto a single line.

Never:

```python
"""Indexes slot facts from episodic memories for sparse and symbolic retrieval."""
```

Always:

```python
"""Indexes slot facts from episodic memories for sparse and symbolic retrieval.

Builds three lookup tables keyed by EDU, (slot, value) pair, and entity value,
plus a per-fact token set for sparse BM25-style scoring. Provides sparse and
symbolic ranking methods and a reciprocal-rank fusion utility for combining them.
"""
```

The structure is:

- **Summary line** (line 1): what the file is responsible for, ending with a period.
- **Blank line**.
- **Elaboration** (1–3 sentences): the key data structures, algorithms, entry points, or constraints not captured in the summary.
- **Closing `"""`** on its own line.

A module with more than ~50 lines or more than three public methods should not have a summary-only docstring. The docstring's weight should feel proportional to the complexity it represents.

Avoid filename-only docstrings such as `"""server.py."""`.

A good module docstring answers at least one of these:

- What responsibility does this file own?
- What larger component does it support?
- What kind of state, IO, API, or service boundary does it coordinate?
- What important usage constraint is visible from the code?

When a module and its primary class describe overlapping concerns, differentiate by scope: the module docstring names the data source, external dependency, or broader purpose; the class docstring names the indexing unit, ownership structure, or usage entry points.

## Class Docstrings

Document what the class represents, what it owns, and what it delegates. Include important attributes or lifecycle behavior when useful.

```python
class DemoConfig:
    """Runtime configuration for the Redwood demo server.

    Attributes:
        port: Local HTTP port used by the demo server.
        db_path: Path to the SQLite database file.
        sciences_root: Root directory containing science module assets.
    """
```

Do not repeat the class name in prose unless it clarifies domain meaning.

For wrapper or coordinator classes, prefer describing ownership and delegation:

```python
class MultiTurnSession:
    """Coordinates a multi-turn dialogue session.

    The session owns the mutable dialogue state and delegates turn-level intent,
    slot, and API-call tracking to `StateTracker`.
    """
```

For index, store, registry, or cache classes whose `__init__` creates lookup structures rather than injecting dependencies, document the data structures created and their initial state — not the parameter list:

```python
def __init__(self) -> None:
    """Creates empty lookup tables for slot facts, entities, and fact tokens."""
```

Name the categories of structures, not a generic count:

- Good: `"for slot facts, entities, and fact tokens"`
- Bad: `"with five internal dictionaries"`

## Function and Method Docstrings

For each public or non-obvious function/method, document behavior, important inputs, return value, exceptions, and side effects.

Good:

```python
def load(self) -> DemoConfig:
    """Loads configuration from the environment and validates derived paths.

    Returns:
        A validated demo configuration.

    Raises:
        FileNotFoundError: If the science module root does not exist.
        ValueError: If a configured port or path is invalid.
    """
```

Good:

```python
def process_turn(self, utterance: str, episodic_context: str = "") -> TurnResult:
    """Processes one user utterance against the current dialogue state.

    Empty utterances return a non-mutating continuation response instead of
    invoking the tracker or language model.

    Args:
        utterance: User input for the current turn.
        episodic_context: Optional contextual information available for this turn.

    Returns:
        The turn result produced from the current state and utterance.
    """
```

Usually skip:

```python
def _is_valid_port(port: int) -> bool:
    return 1 <= port <= 65535
```

## Inline and Block Comments

Write comments that explain why the code is shaped this way:

```python
# Bind to localhost only; this demo server is not hardened for remote traffic.
server = ThreadingHTTPServer(("127.0.0.1", port), Handler)
```

Avoid comments that restate the next line:

```python
# Create server.
server = ThreadingHTTPServer(("127.0.0.1", port), Handler)
```

Use inline or block comments for:

- Non-obvious decisions.
- Workarounds.
- Safety or security assumptions visible from code.
- Performance tradeoffs.
- Compatibility constraints.
- Why behavior intentionally differs from the obvious implementation.

Do not add inline comments for every branch. Prefer a function docstring for the public contract and one targeted inline comment only where it prevents a future maintainer from changing intentional behavior.

## Formatting During Documentation Passes

Preserve behavior. Do not refactor logic unless the user asks.

When returning revised code, it is acceptable to normalize obviously dense formatting around edited code so the result is reviewable. For example, split long argument lists or `return SomeObject(...)` calls across lines when the original formatting hurts readability. Do not rename symbols, reorder logic, change imports, or alter control flow unless requested.

## TODO Comments

Make TODOs attributable and actionable:

```python
# TODO(sakthivel): Replace environment parsing with argparse before CLI release.
```

If a tracker ID is known, prefer including it:

```python
# TODO(b/123456789): Support IPv6 binding for local demo server.
```

Avoid vague TODOs such as `# TODO: fix later`.

## Review Checklist

Use this checklist when auditing code for shipping readiness:

| Area | Standard |
|---|---|
| Module | Has a useful top-level docstring explaining file purpose. |
| Public classes | Have class docstrings explaining responsibility, ownership, delegation, and key attributes when useful. |
| Public functions/methods | Have docstrings when behavior, inputs, returns, exceptions, side effects, or special branches matter. |
| Private helpers | Skip comments/docstrings when names and type hints are enough. |
| Inline comments | Explain intent, tradeoffs, workarounds, security, compatibility, or performance. |
| Redundant comments | Remove comments that only paraphrase code. |
| Accuracy | Do not document behavior, intent, validation, guarantees, or side effects that the code does not support. |
| Specificity | Replace vague filler with code-grounded contracts. |
| TODOs | Include owner or tracking reference and a concrete action. |
| Style | Use clear sentences, consistent punctuation, and no stale comments. |

## Documentation Pass Summary

After revising a file, include a short summary when it helps the user review the change:

```text
Documentation pass summary:
- Added a module docstring describing the file responsibility.
- Added docstrings for public APIs with useful Args/Returns/Raises sections.
- Documented special behavior such as empty-input handling or skipped external calls.
- Added inline comments only for non-obvious runtime or safety assumptions.
- Avoided or replaced vague claims such as validation, caching, or security when unsupported.
- Flagged ambiguous intent instead of inventing behavior.
- Preserved runtime behavior.
```

Do not include a numeric score unless the user explicitly asks for one.

## Response Rules

- Be practical and code-first.
- Keep added comments minimal but useful.
- Prefer precise, code-grounded docstrings over broad, generic, polished-sounding text.
- Preserve the user's existing code behavior unless they ask for refactoring.
- Edit provided code directly when the user asks to comment code.
- Add `Args`, `Returns`, and `Raises` only when they improve the reader's understanding.
- Document meaningful special branches and side effects.
- Remove or avoid redundant comments that restate code.
- When behavior or intent is ambiguous, use neutral wording or mention the ambiguity in the summary.
- When the user asks for Google practice, say the guidance is inspired by Google's public Python style guide rather than claiming access to internal Google practices.
- Do not invent intent or guarantees not supported by the code or user context.
- Do not add citations unless web browsing was used in the current response.
