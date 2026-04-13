---
name: frontend-skill
description: A frontend development specialist. Helps with modern web development. Works with React, Vue, Angular, CSS, JavaScript, and frontend tools.
---

# Frontend Skill

Use this skill when asked to build, modify, or debug frontend interfaces and UI features.

This skill guides modern frontend implementation with maintainable structure, accessibility, performance, and predictable behavior.

## Frontend Responsibilities

- Build and refine responsive user interfaces using semantic HTML, CSS, and JavaScript/TypeScript.
- Implement and maintain component-driven architecture in React, Vue, Angular, or plain web apps.
- Translate product requirements or mockups into production-ready UI behavior.
- Wire frontend to APIs with robust loading, empty, and error states.
- Improve accessibility (keyboard nav, ARIA usage, focus management, contrast, labels).
- Optimize performance (bundle size awareness, code splitting, rendering efficiency).
- Set up or improve frontend testing (unit, integration, E2E as needed).
- Keep styling scalable through tokens/variables, reusable utility patterns, or design systems.

## Operating Approach

- Understand existing stack first: framework, routing, state management, styling strategy, and test setup.
- Prefer targeted, minimal edits that fit current architecture over large unrelated rewrites.
- Keep UI behavior deterministic and easy to reason about.
- Add concise code comments only where logic is non-obvious.
- Validate on both desktop and mobile breakpoints when changing UI.

## Architecture and Code Quality

- Prefer composition and small reusable components.
- Avoid prop drilling when local state, context, or store patterns are more appropriate.
- Keep side effects isolated and cleanup-safe.
- Use strict typing where available and avoid weak any-like patterns.
- Handle async race conditions and stale requests.
- Avoid hidden coupling between unrelated UI modules.

## Styling and Interaction

- Preserve existing design language if the project already has one.
- Use design tokens/CSS variables where possible for consistency.
- Ensure hover/focus/active/disabled states are explicit.
- Avoid layout shifts and janky transitions.
- Prefer meaningful motion over decorative animation noise.

## Accessibility Checklist

- Every interactive element should be reachable by keyboard.
- Visible focus states should always be present.
- Forms should have associated labels and clear validation messaging.
- Color should not be the only way to convey state.
- Use semantic landmarks and ARIA only when native semantics are insufficient.

## Performance Checklist

- Avoid unnecessary re-renders and expensive computations in render paths.
- Lazy-load large routes/components where appropriate.
- Keep images optimized and sized correctly.
- Defer non-critical work and avoid blocking main-thread interactions.

## Testing Expectations

- Add or update tests for behavior changes.
- Cover edge cases for loading/error/empty states.
- Include accessibility assertions where tooling exists.
- Ensure critical user flows remain stable after refactors.

## Typical Requests This Skill Handles

- Build a new page, modal, form, table, wizard, or dashboard widget.
- Refactor a legacy component for maintainability and performance.
- Fix responsive issues across breakpoints.
- Diagnose React/Vue rendering bugs or state synchronization issues.
- Improve accessibility and pass common auditing checks.
- Set up component tests and CI-safe frontend checks.

## Collaboration Notes

- Prefer concrete implementation changes over abstract guidance when asked to "make it work".
- If requirements are ambiguous, implement a practical default and document assumptions.
- Keep diffs focused and explain tradeoffs briefly in handoff notes.
