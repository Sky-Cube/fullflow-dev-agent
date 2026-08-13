# FullFlow DevAgent 贡献指南

感谢你愿意为本项目贡献!🎉 这是一个基于提示词的 Claude Code 智能体体系,每一份贡献——一个新 Skill、一条更严谨的审查清单、一处翻译修正——都会让整条研发流水线对所有人更强。

[English Contributing Guide → CONTRIBUTING.md](CONTRIBUTING.md)

## 贡献方式

1. **新增 Skill**——最有价值的贡献,见[如何新增 Skill](#如何新增-skill)
2. **新增 Sub-Agent**——当某个完整职责领域缺失时
3. **改进现有内容**——打磨 Skill 的自检清单、修正错误规则、更新过时实践
4. **修复文档与翻译**——英文与中文 README 同步维护

## 设计规范(强制)

保持体系一致性,请严格遵守。

### 命名规范

- 目录与文件名:小写 `kebab-case` 英文(如 `code-standard-check`)
- frontmatter `name`:中文名,与 `README.zh-CN.md` 清单**一字不差**
- 禁止对已有条目改名、合并、缩写

### Agent 文件(`.claude/agents/*.md`)

```yaml
---
name: <中文名称,与清单一字不差>
description: <一句话:职责 + 何时使用>
tools: <可选:工具白名单;审查类建议只读工具>
---
```

正文必备章节:身份定位 / 核心职责 / 绑定 Skill / 职责边界 / 输入规范 / 输出规范 / 异常处理。

层级约束:
- Sub-Agent **只有执行权**:prompt 中必须禁止调用 Agent 工具
- Sub-Agent 之间禁止互相调用;跨领域需求上报总控中转
- 审查/审计类 Agent 建议使用只读工具白名单

### Skill 文件(`.claude/skills/<name>/SKILL.md`)

```yaml
---
name: <中文名称,与清单一字不差>
description: <一句话:用途 + 触发时机>
---
```

正文必须采用五段式:适用场景 / 执行步骤 / 规范要点 / 输出模板 / 自检清单。保持 40-70 行,单一职责,无跨业务耦合。

内容规则(与全局 CLAUDE.md 规范对齐):
- 不编造 API、版本号、法条;不确定项标注「需验证」/「以官方文档为准」
- 审查/审计类 Skill 必须要求每条结论附证据
- 安全类 Skill 必须要求留痕与脱敏
- 测试类 Skill 必须要求如实呈现结果,禁止粉饰

## 如何新增 Skill

1. 以现有 Skill 为模板(如 `code-standard-check`),创建 `.claude/skills/<kebab-name>/SKILL.md`
2. 填写 frontmatter + 五段式,保持 40-70 行
3. 在**两份** README 中登记:向 `README.md`(英文)与 `README.zh-CN.md`(中文)的 Skill 清单各加一行,注明归属 Sub-Agent
4. 同步更新归属 Sub-Agent 的「绑定 Skill」表(`.claude/agents/`)

## 如何新增 Sub-Agent

1. 以现有 Sub-Agent 为模板,创建 `.claude/agents/<name>-sub.md`
2. 声明职责范围、绑定 Skill、输入输出契约、禁止事项
3. 在对应主 Agent 名下登记到两份 README
4. 若引入新 Skill,按上一节流程补充

## 提交流程

1. Fork 本仓库
2. 创建特性分支(`git checkout -b skill/my-new-skill`)
3. 修改内容,每个 PR 聚焦一件事
4. 填写 PR 模板(内含自检清单)
5. 提交 PR,维护者将按上述规范评审

## 行为准则

所有参与者须遵守我们的[行为准则](CODE_OF_CONDUCT.md):互相尊重、建设性讨论、友好交流。
