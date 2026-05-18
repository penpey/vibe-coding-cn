# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

**vibe-coding-cn** is a Chinese-language Vibe Coding / AI pair-programming knowledge base (290+ Markdown files). It is not a conventional code project — it is a structured tutorial system covering Prompt engineering, Skill design, Workflow automation, Context management, and Quality Gates for AI-assisted development.

The repository is organized around a **5-layer model**:
- **Prompt** — one-shot instructions for AI conversations
- **Skill** — reusable capability packages (19 skills in `skills/`)
- **Workflow** — executable processes for complex projects (`docs/playbooks/workflows/`)
- **Context** — persistent project memory (`AGENTS.md`, `CLAUDE.md`, `llms.txt`)
- **Quality Gate** — hard constraints via tests, CI, schema, scripts, checklists

## Key Commands

```bash
# Quality gates
make lint          # Markdown linting (requires: npm install -g markdownlint-cli)
make check-links  # Validate local Markdown links (requires: Python 3)
make test         # Run both lint + check-links

# Prompt library conversion tool
cd tools/prompts-library && pip install -r requirements.txt && python3 main.py
# Modes: Excel↔Markdown↔JSONL bidirectional conversion

# Git submodules (external tools)
git submodule update --init --recursive

# Project backup
bash scripts/backups/一键备份.sh
```

## Architecture

### Core Directories
```
docs/               # Knowledge base: concepts, getting-started, playbooks, references, case-studies
skills/             # 19 reusable AI skills (each has SKILL.md + optional references/)
prompts/            # Prompt library entry point (cloud-linked index)
tools/              # Utility tools: prompts-library, chat-vault, config, external submodules
metadata/           # Machine-readable: taxonomy, glossary, redirects, AI citation corpus
scripts/            # Automation: backup, link checking
assets/             # Static resources: images, templates, datasets
.github/workflows/  # CI: markdown-lint + link-checker (push/PR to develop/master)
```

### Key Principles
- **Pin-duck code (拼好码)**: reuse mature solutions, write only glue code for connection/orchestration/adaptation
- **Problem-solving 8-step model**: current state → goal state → gap → constraints → path → execute → verify → iterate
- **Harness Engineering**: use deterministic engineering controls (tests, CI, type checks, linters) to constrain LLM output — never trust AI self-verification

### File Conventions
- All documentation, comments, logs in Chinese
- Code symbols in English with semantic naming
- Lowercase kebab-case or underscore for filenames
- 2/4 space indentation, max 120 columns

## Commit Convention

```
feat|fix|docs|chore|refactor|test: scope - summary
```

## Remote Repositories

- `origin` → `https://github.com/penpey/vibe-coding-cn` (user's fork)
- `upstream` → `https://github.com/tukuaiai/vibe-coding-cn` (original repo)

Sync master from upstream: `git checkout master && git pull upstream master`

## Branch: learning (Active)

The `learning` branch is the user's personal study branch. Learning notes are saved in `learning-notes/`. The `master` branch holds the unmodified original source code.

### Learning Mode (current session)
This session is operating in **learning companion** mode:
- Socratic teaching: Claude asks questions, user answers, Claude validates
- Each learning session covers one knowledge point from the original repo
- Progress tracked in `learning-notes/INDEX.md`
- Only marked complete when user confirms understanding
