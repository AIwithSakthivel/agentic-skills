---
title: Agentic Skills
emoji: 🎯
colorFrom: red
colorTo: purple
sdk: static
pinned: false
---

# Agentic Skills

> Plug-and-play skill definitions that turn any AI coding assistant into a domain-aware specialist. Each skill is a `SKILL.md` file — drop it into your assistant's skills directory, invoke it with `$skill-name`, and your assistant adopts that skill's operating rules, patterns, and quality checklists.

**[▶ Live Demo](https://aiwithsakthivel.github.io/agentic-skills/)** &nbsp;|&nbsp; **[AIwithSakthivel](https://github.com/AIwithSakthivel)** &nbsp;|&nbsp; **[HuggingFace Space](https://huggingface.co/spaces/AIwithSakthivel/agentic-skills)**

---

## Skills

| Skill | What it does | Invoke |
|-------|-------------|--------|
| [frontend-skill](./frontend-skill/SKILL.md) | Frontend specialist — React, Vue, Angular, accessibility, responsive UI, performance, component testing | `$frontend-skill` |
| [sci-experiment](./sci-experiment/SKILL.md) | Scientific experiment structure — hypothesis-first, reproducible, with configs, notebooks, src modules, baselines, and research documentation | `$sci-experiment` |
| [concept-tutor](./concept-tutor/SKILL.md) | Research-grounded science tutor — intuition to formalism, readable formula cards, derivations, paper references, enterprise tradeoffs, and self-assessment for data scientists and ML practitioners | `$concept-tutor` |
| [repo-concept-explainer](./repo-concept-explainer/SKILL.md) | Repository-grounded concept explainer — traces implementation, data, tests, and architecture to explain what a concept means inside a specific codebase, with formulas, standalone examples, and design context | `$repo-concept-explainer` |
| [python-comment-helper](./python-comment-helper/SKILL.md) | Shipping-quality Python documentation pass — Google-style module, class, and function docstrings, useful inline comments, noise removal, and anti-invention discipline for code review | `$python-comment-helper` |

---

## What is a skill?

A skill is a `SKILL.md` file that defines how your AI assistant should approach a domain. When you prefix a prompt with `$skill-name`, the assistant loads the skill's context — its operating rules, patterns, and quality checklist — before responding.

```
$concept-tutor Teach me cross-entropy loss
```

The assistant responds as a focused research science tutor, applying the lesson structure, formula card pattern, research reference rules, and self-assessment gate from that skill.

Works with any AI coding assistant that supports skill or context files.

---

## Quick start

### 1. Clone

```bash
git clone https://github.com/AIwithSakthivel/agentic-skills.git
```

### 2. Copy skills into your assistant's skills directory

```bash
cp -r agentic-skills/frontend-skill           ~/.your-assistant/skills/
cp -r agentic-skills/sci-experiment           ~/.your-assistant/skills/
cp -r agentic-skills/concept-tutor            ~/.your-assistant/skills/
cp -r agentic-skills/repo-concept-explainer   ~/.your-assistant/skills/
cp -r agentic-skills/python-comment-helper    ~/.your-assistant/skills/
```

### 3. Invoke in any prompt

```bash
$frontend-skill           Build a modal dialog with focus trap and keyboard dismiss
$sci-experiment           Set up an experiment to test whether feature X improves AUC on this dataset
$concept-tutor            Teach me attention mechanisms
$repo-concept-explainer   Explain how embedding similarity is computed in this repo
$python-comment-helper    Add Google-style docstrings and prepare this module for code review
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

### `concept-tutor`

Turns your AI assistant into a rigorous, research-grounded science tutor for advanced technical learners — especially data scientists and ML practitioners targeting research and production roles.

**Covers:**
- Intuition-first lessons that move through formalism, derivation, and enterprise application
- Readable formula cards — purpose, plain-English meaning, symbol definitions, read-aloud translation, memory hooks, tiny numeric examples, sensitivity intuition, and common mistakes
- Research trail — seminal papers, top-conference work (NeurIPS, ICML, ICLR, KDD, ACL), surveys, canonical textbooks
- Enterprise lens — accuracy vs latency vs cost, build vs buy, offline vs online metrics, governance, monitoring, and production reliability
- Self-assessment gate — 5–10 questions per lesson covering recall, intuition, formalism, assumptions, derivation, application, comparison, failure modes, research literacy, and enterprise judgment
- Active learning — retrieval questions, derivation exercises, numerical worked examples, paper-reading prompts, implementation tasks

**Use when:** learning, reviewing, studying, practicing, or deeply evaluating any ML, statistics, data science, NLP, retrieval, causal inference, MLOps, or applied science concept.

**Invoke:** `$concept-tutor <your request>`

---

### `repo-concept-explainer`

Explains technical concepts grounded in the actual repository under analysis — source files, tests, configs, datasets, schemas, sample data, prompts, metrics, and architecture.

**Covers:**
- Repo-first investigation: builds a quick repo map, traces definitions and callers, inspects data samples and test fixtures
- Evidence discipline — separates direct repo evidence from reasoned inference; never invents behavior or formulas the repo doesn't support
- Data-grounded examples — uses real or representative sample data to show how the concept acts in context
- Formula pattern — maps each mathematical term back to the implementation, config, or metric in the codebase
- Standalone exercise — minimal command, snippet, or unit-test shape so the learner can isolate and verify the concept independently
- Design role — explains why the concept exists, what depends on it, and what breaks if it changes

**Use when:** understanding what a concept means inside a specific repo, tracing an algorithm, explaining a design choice, or verifying how a feature works with real or fixture data.

**Invoke:** `$repo-concept-explainer <your request>`

---

### `python-comment-helper`

Performs a shipping-quality documentation pass on Python code. Adds Google-style docstrings at module, class, and function level where they matter. Adds inline comments only for non-obvious intent, tradeoffs, workarounds, or safety constraints. Removes noise and never invents behavior or guarantees not supported by the code.

**Covers:**
- Module docstrings explaining file responsibility and scope
- Class docstrings with `Attributes` section for public and non-obvious internal classes
- Function and method docstrings with `Args`, `Returns`, and `Raises` sections when they add value
- Skip heuristic — omits docstrings for tiny private helpers when name and type hints are self-explanatory
- Inline comments explaining the _why_: intent, tradeoffs, workarounds, security assumptions, compatibility constraints, performance choices
- Anti-invention discipline — never documents behavior, guarantees, or business intent not supported by the code
- Documentation pass summary after revising a file

**Use when:** commenting Python code, preparing a module for code review, converting comments to Google style, cleaning up noisy comments, or documenting source, helper, utility, service, or library files.

**Invoke:** `$python-comment-helper <your request>`

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
├── index.html                          ← Live demo UI (GitHub Pages)
├── README.md
├── frontend-skill/
│   ├── SKILL.md
│   └── agents/openai.yaml
├── sci-experiment/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── experiment-pattern.md
│       ├── research-docs.md
│       ├── validation-pattern.md
│       └── llm-experiment-pattern.md
├── concept-tutor/
│   ├── SKILL.md
│   └── agents/openai.yaml
├── repo-concept-explainer/
│   ├── SKILL.md
│   └── agents/openai.yaml
└── python-comment-helper/
    ├── SKILL.md
    └── agents/openai.yaml
```

---

## License

MIT — use, fork, and extend freely.

---

*Built by [AIwithSakthivel](https://github.com/AIwithSakthivel)*
