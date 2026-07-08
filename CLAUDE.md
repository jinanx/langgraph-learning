# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A personal learning repo for **LangGraph**, structured as a 12-demo progression (see README "学习顺序"). The user is the author `jinanx` and uses this repo to study LangGraph concepts incrementally. Code is exploratory — prioritize clarity and progressive complexity over production hardening.

**License:** MIT (Copyright 2026 jinanx)

## Toolchain

- **Python:** 3.14 (pinned via `.python-version`)
- **Package manager:** [`uv`](https://docs.astral.sh/uv/) — `uv.lock` is the source of truth, not `pyproject.toml` alone
- **Editor:** 4 spaces, LF line endings, UTF-8, final newline (`.editorconfig`)

### Common commands

```bash
uv sync                          # install deps from uv.lock
uv run main.py                   # run the placeholder entry point
uv run py examples/graph_demo.py   # run an example directly
uv add <pkg>                     # add a runtime dependency
uv add --dev <pkg>               # add a dev dependency (lint/test/docs)
```

There is **no** lint, test, or build command wired up yet — `tests/` and `app/` are empty scaffolds. If asked to set them up, prefer `ruff` + `pytest` + `mkdocs-material` (matches the user's stack and the approved GitHub automation plan).

## Architecture (the big picture)

The repo has four parallel trees, each with a distinct role — keep them separate:

| Path | Role | Lifetime |
|---|---|---|
| `examples/NN_topic.py` | **Minimal, single-concept** demos — one file per Demo01–12. | Frozen at the moment of writing; should never accumulate dependencies on later demos. |
| `app/` | **Cumulative project** — the polished version that grows across all demos. Each demo adds/changes one module: `state.py` → `graph.py` → `nodes.py` → `router.py` → `tools.py` → `memory.py` → `prompts.py` → `config.py`. | Continuously evolved; at any point reflects "everything learned so far." |
| `shared/` | **Cross-cutting utilities** (`shared/llm.py`, `shared/utils.py`) used by both `app/` and `examples/`. | Grows slowly; treat as the only place code is shared between the two trees. |
| `docs/NN-Topic.md` | **Learning notes** in Chinese, one markdown per demo. | Written alongside the example; mirrors the same numbering as `examples/`. |

### Key invariants

- **Examples never import from `app/`.** `examples/` must stay self-contained and minimal — that's the whole point of having them. If you need to reuse code in an example, lift it into `shared/` instead.
- **`app/` may import from `shared/`,** but not the other way around.
- **Demo numbering must stay in sync** between `examples/`, `docs/`, and the README's "学习顺序" list. If you add a Demo13, all three move together.

## Environment

LLM access requires three env vars (see `.env.example`):

```
OPENAI_API_KEY=
OPENAI_BASE_URL=
MODEL=
```

`.env` is git-ignored. Copy `.env.example` to `.env` and fill in values before running anything that touches an LLM.

## Things to know before editing

- This is **not** a library — don't add `__init__.py` re-exports or API stability concerns. Files are scripts organized by topic.
- The user writes in Chinese; mirror that in any new docs/comments unless asked otherwise.
- There is no pre-commit hook, no CI, no release process yet. Don't add them silently — surface as a question if relevant.
- Empty directories (`app/`, `shared/`, `tests/`, `docs/`) are intentional placeholders for future demos. Don't delete or fill them in without confirming which demo is next.
