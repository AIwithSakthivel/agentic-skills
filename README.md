# Agentic Skills

> Plug-and-play skill definitions that turn any AI coding assistant into a domain-aware engineering specialist. Each skill is a `SKILL.md` file — drop it into your assistant's skills directory, invoke it with `$skill-name`, and your assistant adopts that skill's operating rules, architecture patterns, and quality checklists.

**[▶ Live Demo](https://aiwithsakthivel.github.io/agentic-skills/)** &nbsp;|&nbsp; **[AIwithSakthivel](https://github.com/AIwithSakthivel)** &nbsp;|&nbsp; **[HuggingFace Space](https://huggingface.co/spaces/AIwithSakthivel/agentic-skills)**

---

## Skills

| Skill | What it does | Invoke |
|-------|-------------|--------|
| [frontend-skill](./frontend-skill/SKILL.md) | Frontend specialist — React, Vue, Angular, accessibility, responsive UI, performance, component testing | `$frontend-skill` |
| [python-science](./python-science/SKILL.md) | Data-science feature builder — turns scripts/notebooks into SCM-ready packages with tests, prompts, logs, and usage notebooks | `$python-science` |

---

## What is a skill?

A skill is a `SKILL.md` file that defines how your AI assistant should approach a domain. When you prefix a prompt with `$skill-name`, the assistant loads the skill's context — its operating rules, architecture patterns, and quality checklist — before generating a response.

```
$frontend-skill Build a responsive data table with accessible sorting
```

The assistant responds as a focused frontend specialist, automatically applying the accessibility checklist, performance guidelines, and testing expectations from that skill.

Works with any AI coding assistant that supports skill/context files (Codex, and others).

---

## Quick start

### 1. Clone

```bash
git clone https://github.com/AIwithSakthivel/agentic-skills.git
```

### 2. Copy skills into your assistant's skills directory

```bash
cp -r agentic-skills/frontend-skill ~/.your-assistant/skills/
cp -r agentic-skills/python-science  ~/.your-assistant/skills/
```

### 3. Invoke in any prompt

```bash
$frontend-skill Build a modal dialog with focus trap and keyboard dismiss
$python-science  Turn this evaluation script into a deployable feature with tests
```

---

## Skill reference

### `frontend-skill`

Guides modern frontend implementation with maintainable structure, predictable behavior, accessibility, and performance.

**Covers:**
- Component-driven architecture (React / Vue / Angular / vanilla JS)
- Responsive layouts and CSS design tokens
- Accessibility — keyboard nav, ARIA, focus management, color contrast
- Performance — code splitting, render optimisation, image sizing
- Testing — unit, integration, E2E, accessibility assertions

**Invoke:** `$frontend-skill <your request>`

---

### `python-science`

Turns scripts and notebooks into production-ready Python feature packages with full traceability.

**Covers:**
- SCM-ready feature layout: `src/`, `tests/`, `prompt_templates/`, `logs/`, `results/`
- Modular Python — `config.py`, `models.py`, `pipeline.py`, `prompt_loader.py`
- LLM-backed feature structure with external prompt management
- Logging baseline: run timestamps, artifact paths, row counts, model usage
- Onboarding notebooks (`how_to_use_<feature>.ipynb`)

**Invoke:** `$python-science <your request>`

---

## Demo UI

The [live demo](https://aiwithsakthivel.github.io/agentic-skills/) is a static single-page app (`index.html`) that shows each skill handling a realistic engineering request with an animated AI response. No build step — just open in a browser.

```bash
open index.html
```

---

## HuggingFace

Also available as a [HuggingFace Space](https://huggingface.co/spaces/AIwithSakthivel/agentic-skills) (static HTML). The `SKILL.md` files are context definitions, not model weights — but the interactive demo shows their output in a familiar interface.

---

## Repo structure

```
agentic-skills/
├── index.html                    ← Live demo UI (GitHub Pages)
├── README.md
├── frontend-skill/
│   ├── SKILL.md
│   └── agents/openai.yaml
└── python-science/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
        ├── feature-pattern.md
        ├── docs-and-logbook.md
        ├── llm-feature-pattern.md
        └── validation-pattern.md
```

---

## License

MIT — use, fork, and extend freely.

---

*Built by [AIwithSakthivel](https://github.com/AIwithSakthivel)*
