# Contributing to FullFlow DevAgent

Thank you for your interest in contributing! 🎉 This project is a prompt-based agent system for Claude Code, and every contribution — a new skill, a better review checklist, a translation fix — makes the whole pipeline stronger for everyone.

[中文贡献指南 → CONTRIBUTING.zh-CN.md](CONTRIBUTING.zh-CN.md)

## Ways to Contribute

1. **Add a new Skill** — the most valuable contribution. See [How to add a new Skill](#how-to-add-a-new-skill)
2. **Add a new Sub-Agent** — when a whole responsibility area is missing
3. **Improve existing content** — sharpen a skill's checklists, fix a flawed rule, update outdated practices
4. **Fix documentation & translations** — both English and Chinese READMEs are maintained

## Design Conventions (mandatory)

These keep the system coherent — please follow them exactly.

### Naming

- Directory & file names: lowercase `kebab-case`, English only (e.g. `code-standard-check`)
- `frontmatter name`: the Chinese name, matching the inventory in `README.zh-CN.md` character-for-character
- No renaming, merging, or abbreviating existing entries

### Agent files (`.claude/agents/*.md`)

```yaml
---
name: <中文名称,与清单一字不差>
description: <一句话:职责 + 何时使用>
tools: <可选:工具白名单;审查类建议只读工具>
---
```

Body must contain these sections: 身份定位 / 核心职责 / 绑定 Skill / 职责边界 / 输入规范 / 输出规范 / 异常处理.

Hierarchy rules:
- Sub-agents have **execution rights only** — their prompts must forbid calling the Agent tool
- Sub-agents never call each other; cross-domain work escalates to the orchestrator
- Review/audit-type agents should use read-only tool allowlists

### Skill files (`.claude/skills/<name>/SKILL.md`)

```yaml
---
name: <中文名称,与清单一字不差>
description: <一句话:用途 + 触发时机>
---
```

Body must use the five-section structure: 适用场景 / 执行步骤 / 规范要点 / 输出模板 / 自检清单. Keep it 40–70 lines, single responsibility, no cross-domain coupling.

Content rules (aligned with the global CLAUDE.md standards):
- Never fabricate APIs, version numbers, or legal provisions — mark uncertain items 「需验证」/「以官方文档为准」
- Review/audit skills must require evidence for every conclusion
- Security skills must require audit trails and redacted samples
- Testing skills must require truthful reporting (no whitewashing)

## How to Add a New Skill

1. Create `.claude/skills/<kebab-name>/SKILL.md` following an existing skill as template (e.g. `code-standard-check`)
2. Fill the frontmatter + five sections; keep 40–70 lines
3. Register it in **both** READMEs: add a row to the Skill Inventory in `README.md` (English) and `README.zh-CN.md` (Chinese), including its owner sub-agent
4. Update the owner sub-agent's 绑定 Skill table in `.claude/agents/`

## How to Add a New Sub-Agent

1. Create `.claude/agents/<name>-sub.md` following an existing sub-agent as template
2. Declare its scope, bound skills, input/output contracts, and prohibitions
3. Register it in both READMEs under the correct master agent
4. If it introduces new skills, add them per the section above

## Submission Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b skill/my-new-skill`)
3. Make your changes, keeping each PR focused on one thing
4. Fill in the PR template (self-check checklist included)
5. Submit the PR — maintainers will review against the conventions above

## Code of Conduct

All participants are expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md). Be respectful, be constructive, be kind.
