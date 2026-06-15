# Claude Code Skills

> Custom skills for [Claude Code](https://claude.ai/code) that turn the CLI into a domain-aware engineering assistant. Each skill is a `SKILL.md` file that shapes how Claude approaches a category of work — choose your specialty and invoke it with `$skill-name`.

**[▶ Live Demo](https://aiwithsakthivel.github.io/claude-code-skills/)** &nbsp;|&nbsp; **[AIwithSakthivel](https://github.com/AIwithSakthivel)**

---

## Skills in this repo

| Skill | Description | Invoke |
|-------|-------------|--------|
| [frontend-skill](./frontend-skill/SKILL.md) | Frontend development specialist — React, Vue, Angular, a11y, performance, responsive UI | `$frontend-skill` |
| [python-science](./python-science/SKILL.md) | Python data-science feature builder — scripts/notebooks → SCM-ready modules with tests, prompts, logs | `$python-science` |

---

## What is a Claude Code Skill?

A skill is a `SKILL.md` file placed in your Claude Code skills directory. When you prefix a prompt with `$skill-name`, Claude loads the skill's context — its operating rules, architecture patterns, and quality checklist — before generating a response.

```
your-prompt: $frontend-skill Build a responsive data table with accessible sorting
```

Claude then responds as a focused frontend specialist, applying the skill's accessibility checklist, performance guidelines, and testing expectations automatically.

---

## Quick start

### 1. Clone this repo

```bash
git clone https://github.com/AIwithSakthivel/claude-code-skills.git
```

### 2. Copy skills into Claude Code

```bash
# Default skills directory for Claude Code
cp -r claude-code-skills/frontend-skill ~/.claude/skills/
cp -r claude-code-skills/python-science  ~/.claude/skills/
```

### 3. Invoke in any prompt

```bash
# In your terminal with Claude Code running:
$frontend-skill Build a modal dialog with focus trap and keyboard dismiss
$python-science  Turn this evaluation script into a deployable feature with tests
```

---

## Skill reference

### `frontend-skill`

Guides modern frontend implementation. Covers:

- Component-driven architecture (React / Vue / Angular / vanilla)
- Responsive layouts and CSS design tokens
- Accessibility — keyboard nav, ARIA, focus management, contrast
- Performance — bundle splitting, render optimization, image sizing
- Testing — unit, integration, E2E, accessibility assertions

**Invoke:** `$frontend-skill <your request>`

---

### `python-science`

Turns scripts and notebooks into production-ready Python feature packages. Covers:

- SCM-ready feature layout: `src/`, `tests/`, `prompt_templates/`, `logs/`, `results/`
- Modular Python — `config.py`, `models.py`, `pipeline.py`, `prompt_loader.py`
- LLM-backed feature structure with prompt management
- Logging baseline: run timestamps, artifact paths, row counts, model usage
- How-to notebooks for onboarding and validation

**Invoke:** `$python-science <your request>`

---

## Demo UI

The [live demo](https://aiwithsakthivel.github.io/claude-code-skills/) is a static single-page app (`index.html`) styled to match the Claude web interface. It shows each skill handling a realistic engineering request with a typing-animation response.

To run locally:

```bash
# No build step needed — just open in a browser
open index.html
```

---

## HuggingFace

The demo UI is also hosted as a [HuggingFace Space](https://huggingface.co/spaces/AIwithSakthivel/claude-code-skills) (static HTML Space). The SKILL.md files are Claude Code-specific context files; they are not model weights or inference APIs — but the demo shows their output in an interactive format.

---

## Repo structure

```
claude-code-skills/
├── index.html                    ← Live demo UI (GitHub Pages)
├── README.md
├── frontend-skill/
│   ├── SKILL.md                  ← Skill definition
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

MIT — use these skills in your own Claude Code setup freely.

---

*Built by [AIwithSakthivel](https://github.com/AIwithSakthivel) · Powered by [Claude Code](https://claude.ai/code)*
