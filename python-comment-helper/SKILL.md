---
name: python-comment-helper
description: improve python comments and docstrings through a shipping-quality documentation pass. use when the user asks to comment python code, add or revise module/class/function/method docstrings, clean up noisy comments, prepare code comments for codex or code review, convert comments to google style, or document source, helper, utility, service, or library files. focuses on useful documentation that explains intent, contracts, side effects, edge cases, and constraints while avoiding invented behavior or comments that restate code.
---

# Python Comment Helper

## Goal

Perform a shipping-quality documentation pass for Python code. Generic tools add comments; this skill improves documentation quality by adding only useful Google-style docstrings and comments, removing or avoiding noise, preserving behavior, and making unsupported assumptions explicit.

Use docstrings to document APIs. Use comments to explain intent. Avoid comments that simply restate code.

## Default Output

When reviewing or writing comments for Python code, produce:

1. Revised code snippets with module, class, function, or method docstrings where appropriate.
2. Inline or block comments only where they explain non-obvious intent, constraints, side effects, tradeoffs, safety assumptions, compatibility issues, or performance choices.
3. A concise documentation pass summary when useful, especially after editing a full file.

Prefer editing the user's code directly over giving abstract advice when code is provided.

## Core Standard

Use this hierarchy:

- Use a module docstring at the top of a shipped Python file to explain the file's responsibility and scope.
- Use class docstrings for public classes and non-obvious internal classes.
- Use function and method docstrings for public APIs, complex behavior, non-obvious side effects, validation, exceptions, or returned values.
- Skip docstrings for tiny private helpers when the function name and type hints are self-explanatory.
- Use inline or block comments only for non-obvious intent, tradeoffs, workarounds, security assumptions, compatibility constraints, or performance choices.
- Delete, avoid, or flag comments that merely translate Python into English.

## Anti-Invention Rule

Never invent business purpose, product intent, side effects, persistence behavior, security guarantees, performance guarantees, API contracts, ownership, or operational assumptions that are not supported by the code or by user-provided context.

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

## Docstring Format

Use Google-style docstring sections when they add value:

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

## Module Docstrings

For shipped files, add a top-level docstring that explains responsibility and scope:

```python
"""Local HTTP server for the Redwood DST demo UI.

The server exposes static demo assets and a small JSON API backed by the local
demo database. It is intended for local development only and binds to localhost.
"""
```

Avoid filename-only docstrings such as `"""server.py."""`.

## Class Docstrings

Document what the class represents and any important attributes or lifecycle behavior:

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
| Public classes | Have class docstrings explaining responsibility and key attributes. |
| Public functions/methods | Have docstrings when behavior, inputs, returns, exceptions, or side effects matter. |
| Private helpers | Skip comments/docstrings when names and type hints are enough. |
| Inline comments | Explain intent, tradeoffs, workarounds, security, compatibility, or performance. |
| Redundant comments | Remove comments that only paraphrase code. |
| Accuracy | Do not document behavior, intent, or guarantees that the code does not support. |
| TODOs | Include owner or tracking reference and a concrete action. |
| Style | Use clear sentences, consistent punctuation, and no stale comments. |

## Documentation Pass Summary

After revising a file, include a short summary when it helps the user review the change:

```text
Documentation pass summary:
- Added a module docstring describing the file responsibility.
- Added docstrings for public APIs with useful Args/Returns/Raises sections.
- Added inline comments only for non-obvious runtime or safety assumptions.
- Avoided redundant comments for self-explanatory code.
- Flagged ambiguous intent instead of inventing behavior.
```

Do not include a numeric score unless the user explicitly asks for one.

## Response Rules

- Be practical and code-first.
- Keep added comments minimal but useful.
- Preserve the user's existing code behavior unless they ask for refactoring.
- When the user asks for Google practice, say the guidance is inspired by Google's public Python style guide rather than claiming access to internal Google practices.
- Do not invent intent or guarantees not supported by the code or user context.
- Do not add citations unless web browsing was used in the current response.
