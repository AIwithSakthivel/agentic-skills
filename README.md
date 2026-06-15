# Agentic Skills

> Plug-and-play skill definitions that turn any AI coding assistant into a domain-aware specialist. Each skill is a `SKILL.md` file — drop it into your assistant's skills directory, invoke it with `$skill-name`, and your assistant adopts that skill's operating rules, patterns, and quality checklists.

**[▶ Live Demo](https://aiwithsakthivel.github.io/agentic-skills/)** &nbsp;|&nbsp; **[AIwithSakthivel](https://github.com/AIwithSakthivel)** &nbsp;|&nbsp; **[HuggingFace Space](https://huggingface.co/spaces/AIwithSakthivel/agentic-skills)**

---

## Skills

| Skill | What it does | Invoke |
|-------|-------------|--------|
| [frontend-skill](./frontend-skill/SKILL.md) | Frontend specialist — React, Vue, Angular, accessibility, responsive UI, performance, component testing | `$frontend-skill` |
| [sci-experiment](./sci-experiment/SKILL.md) | Scientific experiment structure — hypothesis-first, reproducible, with configs, notebooks, src modules, baselines, and research documentation | `$sci-experiment` |

---

## What is a skill?

A skill is a `SKILL.md` file that defines how your AI assistant should approach a domain. When you prefix a prompt with `$skill-name`, the assistant loads the skill's context — its operating rules, patterns, and quality checklist — before responding.

```
$sci-experiment Set up a reproducible experiment to test hypothesis X on dataset Y
```

The assistant responds as a focused scientific experiment specialist, applying the hypothesis structure, reproducibility rules, config conventions, and research documentation pattern from that skill.

Works with any AI coding assistant that supports skill or context files.

---

## Quick start

### 1. Clone

```bash
git clone https://github.com/AIwithSakthivel/agentic-skills.git
```

### 2. Copy skills into your assistant's skills directory

```bash
cp -r agentic-skills/frontend-skill ~/.your-assistant/skills/
cp -r agentic-skills/sci-experiment  ~/.your-assistant/skills/
```

### 3. Invoke in any prompt

```bash
$frontend-skill Build a modal dialog with focus trap and keyboard dismiss
$sci-experiment  Set up an experiment to test whether feature X improves AUC on this dataset
```

---

## Skill reference

### `frontend-skill`

Guides modern frontend implementation with maintainable structure, predictable behaviour, accessibility, and performance.

**Covers:**
- Component-driven architecture (React / Vue / Angular / vanilla JS)
- Responsive layouts and CSS design tokens
- Accessibility — keyboard nav, ARIA, focus management, colour contrast
- Performance — code splitting, render optimisation, image sizing
- Testing — unit, integration, E2E, accessibility assertions

**Invoke:** `$frontend-skill <your request>`

---

### `sci-experiment`

Guides data scientists through designing and running reproducible scientific experiments — from hypothesis to findings.

**Covers:**
- Hypothesis-first structure: question, method, baseline, success criterion, findings
- Experiment layout: `notebooks/`, `src/`, `configs/`, `data/raw`, `results/`, `environment.yml`
- Config management — all parameters (seeds, hyperparameters, paths) in `configs/`, never hardcoded
- Notebook / src separation — explore in notebooks, extract stable logic to `src/`
- Reproducibility checklist — seed pinning, environment lock, deterministic data processing
- Research brief (`README.md`) as the primary deliverable
- LLM-backed experiment support via `configs/prompts/` and a provider interface

**Invoke:** `$sci-experiment <your request>`

---

## Demo UI

The [live demo](https://aiwithsakthivel.github.io/agentic-skills/) is a static single-page app (`index.html`) that shows each skill handling a realistic request with an animated response. No build step — just open in a browser.

```bash
open index.html
```

---

## HuggingFace

Also available as a [HuggingFace Space](https://huggingface.co/spaces/AIwithSakthivel/agentic-skills) (static HTML). The `SKILL.md` files are context definitions, not model weights — but the interactive demo shows their effect in a familiar interface.

---

## Repo structure

```
agentic-skills/
├── index.html                       ← Live demo UI (GitHub Pages)
├── README.md
├── frontend-skill/
│   ├── SKILL.md
│   └── agents/openai.yaml
└── sci-experiment/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
        ├── experiment-pattern.md
        ├── research-docs.md
        ├── validation-pattern.md
        └── llm-experiment-pattern.md
```

---

## License

MIT — use, fork, and extend freely.

---

*Built by [AIwithSakthivel](https://github.com/AIwithSakthivel)*
