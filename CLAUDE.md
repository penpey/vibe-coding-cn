# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

**vibe-coding-cn** is a Chinese Vibe Coding / AI pair-programming knowledge base (290+ Markdown files, 19 Skills, 4 case studies, 23 philosophy methodologies). It is a structured tutorial system, not a conventional code project. The core philosophy is **Pin-duck code (拼好码)**: reuse mature solutions, write only glue code.

The repo is organized around a **5-layer model**:
- **Prompt** — instructions for AI conversations (`prompts/`)
- **Skill** — reusable capability packages (`skills/`, each with `SKILL.md`)
- **Workflow** — executable development processes (`docs/playbooks/workflows/`)
- **Context** — persistent memory (`AGENTS.md`, `CLAUDE.md`, `llms.txt`)
- **Quality Gate** — hard constraints (`Makefile`, CI, scripts, schemas)

## Key Commands

```bash
make lint            # Markdown linting (requires: npm install -g markdownlint-cli)
make check-links    # Validate local Markdown links (requires: Python 3)
make test           # Quality gate = lint + check-links

# Prompt library converter: Excel ↔ Markdown ↔ JSONL
cd tools/prompts-library && pip install -r requirements.txt && python3 main.py

# Initialize git submodules (external tools)
git submodule update --init --recursive

# Full backup
bash scripts/backups/一键备份.sh
```

### CI/CD (`.github/workflows/ci.yml`)
Runs on push/PR to `develop` or `master`: markdown-lint + local link check + external link check.

## Architecture

### Core Directories
```
docs/concepts/          # Core theory: paradigm evolution, problem-solving, pin-duck code, programming tao
docs/concepts/philosophy/  # 23 philosophy methods with Python tooling mappings
docs/getting-started/   # Environment setup, learning roadmap
docs/references/        # Checklists: constraints, code review, common pitfalls, project templates
docs/playbooks/         # Workflows: auto-dev-loop, multi-agent swarm, GEO/SEO, tool configs
docs/case-studies/      # Real project logs: Polymarket, Fate Engine, OpenClaw, Telegram
skills/                 # 19 AI skills (each is a standalone capability package)
prompts/                # Prompt library index (cloud-linked)
tools/prompts-library/  # Python tool: Excel↔Markdown↔JSONL bidirectional conversion
tools/chat-vault/       # AI chat history archiver
metadata/               # Taxonomy, glossary, redirects, AI citation corpus
.gitmodules → tools/external/  # tmux, oh-my-tmux, Claude official skills, Skill Seekers
```

### File Conventions
- Docs, comments, logs: **Chinese**
- Code symbols: **English**, semantic naming
- Filenames: lowercase kebab-case or underscore
- Commit format: `feat|fix|docs|chore|refactor|test: scope - summary`

## Remote Repositories

- `origin` → `https://github.com/penpey/vibe-coding-cn` (fork — push destination)
- `upstream` → `https://github.com/tukuaiai/vibe-coding-cn` (original — pull updates)
- Sync master: `git checkout master && git pull upstream master`

## Active Branch: `learning`

This branch is the user's personal study environment. The `master` branch holds the unmodified source.

### Learning Mode
Current session operates as a **learning companion**:
- **Socratic teaching**: Claude questions → user answers → Claude validates → record → next round
- **4-step cycle**: concept input → Q&A interaction → hands-on practice → review & commit
- Original repo documents (`docs/`, `skills/`) are the learning material; `learning-notes/` tracks progress
- Progress tracked in `learning-notes/INDEX.md`; only marked complete on user confirmation

### Interaction Commands
| You say | I do |
|:---|:---|
| `继续` | Next knowledge point |
| `不懂` / `解释一下` | Log question, explain differently |
| `复习` / `总结一下` | Review notes |
| `我想练习` / `给我出题` | Give a practice task |
| `现在在哪` | Current progress & next step |
