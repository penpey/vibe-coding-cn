# CLAUDE.md

本文件为 Claude Code 提供本仓库的操作指南。

## 仓库简介

**vibe-coding-cn** 是中文 Vibe Coding / AI 结对编程的知识库（290+ 篇 Markdown、19 个 Skill、4 个实战案例、23 种哲学方法论）。它是一个结构化教程体系，不是常规代码项目。核心哲学是**拼好码**：优先复用成熟方案，只写必要的胶水代码。

仓库按 **5 层模型**组织：
- **Prompt** — AI 会话指令（`prompts/`）
- **Skill** — 可复用能力包（`skills/`，每个有独立的 `SKILL.md`）
- **Workflow** — 可执行开发流程（`docs/playbooks/workflows/`）
- **Context** — 持久上下文（`AGENTS.md`、`CLAUDE.md`、`llms.txt`）
- **Quality Gate** — 硬门禁（`Makefile`、CI、脚本、schema）

## 关键命令

```bash
make lint            # Markdown 格式检查（需 npm install -g markdownlint-cli）
make check-links    # 校验仓库内 Markdown 相对链接（需 Python 3）
make test           # 质量门禁 = lint + check-links

# 提示词格式转换工具：Excel ↔ Markdown ↔ JSONL
cd tools/prompts-library && pip install -r requirements.txt && python3 main.py

# 初始化 Git 子模块（外部工具）
git submodule update --init --recursive

# 完整项目备份
bash scripts/backups/一键备份.sh
```

### CI/CD（`.github/workflows/ci.yml`）
在 push/PR 到 `develop` 或 `master` 时触发：markdown-lint + 本地链接检查 + 外部链接检查。

## 架构速览

### 核心目录
```
docs/concepts/              核心理论：范式演进、问题求解、拼好码、编程之道
docs/concepts/philosophy/   23 种哲学方法论（含 Python 工具映射）
docs/getting-started/       环境配置、学习地图
docs/references/            检查清单：约束、审查、常见坑、项目模板
docs/playbooks/             工作流：自动开发闭环、多 Agent 蜂群、GEO/SEO、工具配置
docs/case-studies/          真实项目日志：Polymarket、Fate Engine、OpenClaw、Telegram
skills/                     19 个 AI Skill（每个是独立能力包）
prompts/                    提示词库索引（云端链接）
tools/prompts-library/      Python 工具：Excel↔Markdown↔JSONL 互转
tools/chat-vault/           AI 聊天记录保存工具
metadata/                   分类体系、术语表、重定向映射、AI 引用语料
.gitmodules → tools/external/  外部子模块：tmux、Claude 官方 Skills、Skill Seekers
```

### 文件规范
- 文档、注释、日志：**中文**
- 代码符号：**英文**，语义直白
- 文件名：小写中划线或下划线
- Commit 格式：`feat|fix|docs|chore|refactor|test: 范围 - 描述`

## 远程仓库

- `origin` → `https://github.com/penpey/vibe-coding-cn`（你的 fork，推送目标）
- `upstream` → `https://github.com/tukuaiai/vibe-coding-cn`（原仓库，拉取更新）
- 同步 master：`git checkout master && git pull upstream master`

## 当前分支：`learning`

本分支是用户的个人学习环境。`master` 分支保持原源代码不变。

### 学习模式
当前会话以**学习伴侣**角色运行：
- **苏格拉底式教学**：我提问 → 你回答 → 我判断 → 记录 → 下一轮
- **四步循环**：概念输入 → 问答互动 → 动手实践 → 复盘提交
- 学习材料使用原仓库文档（`docs/`、`skills/`）；`learning-notes/` 跟踪进度
- 进度记录在 `learning-notes/INDEX.md`，你确认后才标记完成

### 交互指令
| 你说 | 我做 |
|:---|:---|
| `继续` | 推进到下一个知识点 |
| `不懂` / `解释一下` | 记录疑问，换方式解释 |
| `复习` / `总结一下` | 调出笔记重新梳理 |
| `我想练习` / `给我出题` | 给一个实践任务 |
| `现在在哪` | 告知当前进度和下一步 |
