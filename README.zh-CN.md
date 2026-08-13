<div align="center">

# 🚀 FullFlow DevAgent 全栈研发 Agent 与 Skill 体系

[![English](https://img.shields.io/badge/English-README-blue?style=flat-square)](README.md)
[![简体中文](https://img.shields.io/badge/简体中文-README.zh--CN-red?style=flat-square)](README.zh-CN.md)

**基于 Claude Code 的全链路软件开发智能体体系**

[![Author](https://img.shields.io/badge/Author-Sky--Cube-brightgreen?style=flat-square)](https://github.com/Sky-Cube)
[![Language](https://img.shields.io/badge/Language-Markdown-blue?style=flat-square)](https://github.com/Sky-Cube/fullflow-dev-agent)
[![Stars](https://img.shields.io/github/stars/Sky-Cube/fullflow-dev-agent?style=flat-square&color=yellow)](https://github.com/Sky-Cube/fullflow-dev-agent/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/Sky-Cube/fullflow-dev-agent?style=flat-square&color=orange)](https://github.com/Sky-Cube/fullflow-dev-agent/commits)
[![License](https://img.shields.io/github/license/Sky-Cube/fullflow-dev-agent?style=flat-square&color=purple)](LICENSE)

</div>

> 基于《Agent与Skill体系架构设计》落地为 Claude Code 原生机制(agents/*.md + skills/*/SKILL.md)。
> 本仓库即完整体系:`.claude/agents`(31 个 Agent)、`.claude/skills`(96 个 Skill)、`CLAUDE.md`(总控规则)。
> 安装方式:将本仓库 `.claude/` 目录与 `CLAUDE.md` 复制到目标项目根目录(项目级)或 `~/.claude/`(全局),总控规则随之生效。

> ⚠️ 本项目内容由 AI 辅助生成,使用前请评估其适用性。

## 一、体系总览

```
项目总控(主对话 + 本仓库 CLAUDE.md)
    │
    ├── 🟡 产品与需求主Agent ─────── 4 个 Sub-Agent / 15 个 Skill(链路最前端)
    ├── 🟢 全栈开发主Agent ───────── 5 个 Sub-Agent / 19 个 Skill
    ├── 🟣 质量管控主Agent ───────── 4 个 Sub-Agent / 15 个 Skill
    ├── 🟠 测试工程主Agent ───────── 4 个 Sub-Agent / 16 个 Skill
    ├── 🔵 运维交付主Agent ───────── 4 个 Sub-Agent / 15 个 Skill
    └── 🔴 安全合规主Agent(贯穿) ── 4 个 Sub-Agent / 16 个 Skill
```

- **正向链路**:产品需求 → 开发产出 → 质量评审 → 测试验收 → 运维交付,**每个环节安全合规贯穿校验**。
- **反向链路**:任一环节发现问题,由上级回退整改,总控跟踪闭环。
- **总量**:6 个一级主 Agent + 25 个二级 Sub-Agent + 96 个原子 Skill。

## 二、目录结构

```
fullflow-dev-agent/
├── CLAUDE.md                          # 总控规则(调度/门禁/熔断)
├── README.zh-CN.md                    # 本文件:体系说明与全量清单(中文)
└── .claude/
    ├── agents/                        # Agent 定义(文件名 kebab-case,frontmatter name 为中文)
    │   ├── product-master.md          # 6 个一级主 Agent(调度型,持有 Agent 工具)
    │   ├── dev-master.md
    │   ├── qa-master.md
    │   ├── test-master.md
    │   ├── ops-master.md
    │   ├── sec-master.md
    │   └── *-sub.md                   # 25 个二级 Sub-Agent(执行型,禁止互相调用)
    └── skills/                        # 原子 Skill(每个一个目录 + SKILL.md)
        └── <skill-name>/SKILL.md
```

## 三、Agent 全量清单(31 个)

### 🟡 产品与需求主Agent(product-master)

| 文件 | Agent 名称 | 职责一句话 |
|---|---|---|
| product-master.md | 产品与需求主Agent | 需求拆解、PRD 管控、原型交互统筹,研发链路最前端 |
| product-requirement-sub.md | 需求分析Sub-Agent | 需求调研、用户故事拆解、验收标准定义 |
| product-prd-sub.md | PRD与产品设计Sub-Agent | PRD 撰写、信息架构、功能规格、版本规划 |
| product-prototype-sub.md | 原型与交互Sub-Agent | 线框图、交互流程、Figma 设计稿、设计走查 |
| product-backlog-sub.md | 需求变更与优先级Sub-Agent | 变更评估、优先级排序、路线图规划 |

### 🟢 全栈&AI应用开发主Agent(dev-master)

| 文件 | Agent 名称 | 职责一句话 |
|---|---|---|
| dev-master.md | 全栈&AI应用开发主Agent | 统筹架构/前后端/AI工程化/中间件研发全流程 |
| dev-architecture-sub.md | 架构设计Sub-Agent | 技术选型、AI架构、数据库建模、接口协议 |
| dev-backend-sub.md | 后端开发Sub-Agent | 后端业务代码、脚手架、DB映射、大模型服务封装 |
| dev-frontend-sub.md | 前端开发Sub-Agent | 多端页面、组件库、前端工程化、AI交互组件 |
| dev-ai-engineering-sub.md | AI应用工程化Sub-Agent | RAG 全链路、Prompt 优化、Agent 编排、向量库调优 |
| dev-middleware-sub.md | 中间件与基础设施Sub-Agent | Redis 缓存、MQ 消息队列、API 网关配置 |

### 🟣 质量管控与代码审查主Agent(qa-master)

| 文件 | Agent 名称 | 职责一句话 |
|---|---|---|
| qa-master.md | 质量管控与代码审查主Agent | 独立把控代码质量、架构合规、技术债务 |
| qa-code-review-sub.md | 代码审查Sub-Agent | 编码规范、逻辑缺陷、性能隐患、AI代码专项审查 |
| qa-architecture-review-sub.md | 架构评审Sub-Agent | 架构合规、依赖分析、设计模式、技术债务量化 |
| qa-metrics-sub.md | 代码质量度量Sub-Agent | 圈复杂度、测试覆盖率、重复代码、质量趋势 |
| qa-tech-debt-sub.md | 技术债务管理Sub-Agent | 债务分级、偿还排序、重构方案推荐 |

### 🟠 测试工程主Agent(test-master)

| 文件 | Agent 名称 | 职责一句话 |
|---|---|---|
| test-master.md | 测试工程主Agent | 统筹功能/自动化/性能/AI专项测试 |
| test-functional-sub.md | 功能测试Sub-Agent | 用例生成、场景执行、缺陷分级、回归筛选 |
| test-automation-sub.md | 自动化测试Sub-Agent | 单元/接口/UI 自动化脚本与报告分析 |
| test-performance-sub.md | 性能压测Sub-Agent | 压测场景设计、执行、瓶颈分析、调优建议 |
| test-ai-special-sub.md | AI应用专项测试Sub-Agent | 准确性评测、幻觉检测、Prompt注入、RAG评测 |

### 🔵 运维与交付主Agent(ops-master)

| 文件 | Agent 名称 | 职责一句话 |
|---|---|---|
| ops-master.md | 运维与交付主Agent | 统筹 CI/CD、发布部署、监控排障、成本管控 |
| ops-cicd-sub.md | CI/CD流水线Sub-Agent | 流水线配置、镜像构建、多环境配置、流水线排障 |
| ops-deploy-sub.md | 发布与部署Sub-Agent | 发布方案、容器编排、环境初始化、一键回滚 |
| ops-monitor-sub.md | 监控与故障排查Sub-Agent | 监控大盘、日志分析、链路追踪、根因分析 |
| ops-cost-sub.md | 资源与成本管理Sub-Agent | 资源评估、降本方案、弹性伸缩配置 |

### 🔴 安全与合规主Agent(sec-master,全流程贯穿)

| 文件 | Agent 名称 | 职责一句话 |
|---|---|---|
| sec-master.md | 安全与合规主Agent | 全生命周期安全审计,一票否决权,直报总控 |
| sec-code-audit-sub.md | 代码安全审计Sub-Agent | SAST、组件漏洞、硬编码密钥、AI代码安全 |
| sec-infra-sub.md | 基础设施安全Sub-Agent | 基线检测、容器扫描、网络策略、权限最小化 |
| sec-data-sub.md | 数据安全与隐私Sub-Agent | 敏感数据识别、脱敏、传输存储加密、泄露评估 |
| sec-compliance-sub.md | 合规与风险评估Sub-Agent | 合规差距、风险分级、整改建议、审计报告 |

## 四、Skill 全量清单(96 个,已全部建成 ✅)

### 产品侧(15 个)

| Skill 名称 | 目录名(skills/ 下) | 归属 Sub-Agent | 状态 |
|---|---|---|---|
| 需求调研分析Skill | requirement-research | 需求分析 | ✅ |
| 用户故事拆解Skill | user-story-splitting | 需求分析 | ✅ |
| 验收标准定义Skill | acceptance-criteria | 需求分析 | ✅ |
| 竞品与市场分析Skill | competitor-analysis | 需求分析 | ✅ |
| PRD撰写Skill | prd-writing | PRD与产品设计 | ✅ |
| 信息架构设计Skill | information-architecture | PRD与产品设计 | ✅ |
| 功能规格说明Skill | functional-spec | PRD与产品设计 | ✅ |
| 版本规划Skill | version-planning | PRD与产品设计 | ✅ |
| 线框图设计Skill | wireframe-design | 原型与交互 | ✅ |
| 交互流程设计Skill | interaction-flow-design | 原型与交互 | ✅ |
| Figma设计稿生成Skill | figma-design-generation | 原型与交互 | ✅ |
| 设计走查Skill | design-walkthrough | 原型与交互 | ✅ |
| 需求变更评估Skill | requirement-change-assessment | 需求变更与优先级 | ✅ |
| 需求优先级排序Skill | requirement-prioritization | 需求变更与优先级 | ✅ |
| 路线图规划Skill | roadmap-planning | 需求变更与优先级 | ✅ |

### 开发侧(19 个)

| Skill 名称 | 目录名(skills/ 下) | 归属 Sub-Agent | 状态 |
|---|---|---|---|
| 全栈架构选型Skill | fullstack-architecture-selection | 架构设计 | ✅ |
| AI应用架构设计Skill | ai-architecture-design | 架构设计 | ✅ |
| 数据库建模Skill | database-modeling | 架构设计 | ✅ |
| 接口协议定义Skill | api-protocol-definition | 架构设计 | ✅ |
| 多语言代码生成Skill | code-generation | 后端开发 | ✅ |
| 框架脚手架搭建Skill | scaffold-setup | 后端开发 | ✅ |
| 数据库表映射开发Skill | orm-mapping | 后端开发 | ✅ |
| 大模型服务封装Skill | llm-service-wrapper | 后端开发 | ✅ |
| 多端页面生成Skill | multi-platform-page-generation | 前端开发 | ✅ |
| 组件库封装Skill | component-library | 前端开发 | ✅ |
| 前端工程化配置Skill | frontend-engineering-config | 前端开发 | ✅ |
| AI交互组件开发Skill | ai-interactive-components | 前端开发 | ✅ |
| RAG全链路搭建Skill | rag-pipeline | AI应用工程化 | ✅ |
| Prompt工程优化Skill | prompt-engineering | AI应用工程化 | ✅ |
| 智能Agent编排Skill | agent-orchestration | AI应用工程化 | ✅ |
| 向量库部署调优Skill | vector-db-tuning | AI应用工程化 | ✅ |
| 缓存策略设计实现Skill | cache-strategy | 中间件与基础设施 | ✅ |
| 消息队列规划开发Skill | mq-planning | 中间件与基础设施 | ✅ |
| API网关配置Skill | api-gateway-config | 中间件与基础设施 | ✅ |

### 质量侧(15 个)

| Skill 名称 | 目录名(skills/ 下) | 归属 Sub-Agent | 状态 |
|---|---|---|---|
| 编码规范检查Skill | code-standard-check | 代码审查 | ✅ |
| 代码逻辑缺陷审查Skill | code-defect-review | 代码审查 | ✅ |
| 性能隐患识别Skill | performance-hazard | 代码审查 | ✅ |
| AI代码专项审查Skill | ai-code-review | 代码审查 | ✅ |
| 架构合规性校验Skill | architecture-compliance | 架构评审 | ✅ |
| 依赖关系分析Skill | dependency-analysis | 架构评审 | ✅ |
| 设计模式评估Skill | design-pattern-evaluation | 架构评审 | ✅ |
| 技术债务量化Skill | tech-debt-quantification | 架构评审 | ✅ |
| 代码复杂度计算Skill | complexity-metrics | 代码质量度量 | ✅ |
| 测试覆盖率统计Skill | coverage-metrics | 代码质量度量 | ✅ |
| 重复代码检测Skill | duplicate-code-detection | 代码质量度量 | ✅ |
| 质量趋势分析Skill | quality-trend-analysis | 代码质量度量 | ✅ |
| 债务识别分级Skill | debt-identification-grading | 技术债务管理 | ✅ |
| 偿还优先级排序Skill | debt-repayment-priority | 技术债务管理 | ✅ |
| 重构方案推荐Skill | refactoring-plan | 技术债务管理 | ✅ |

### 测试侧(16 个)

| Skill 名称 | 目录名(skills/ 下) | 归属 Sub-Agent | 状态 |
|---|---|---|---|
| 测试用例自动生成Skill | test-case-generation | 功能测试 | ✅ |
| 业务场景测试执行Skill | business-scenario-testing | 功能测试 | ✅ |
| 缺陷分级报告Skill | defect-grading-report | 功能测试 | ✅ |
| 回归用例筛选Skill | regression-case-selection | 功能测试 | ✅ |
| 单元测试代码生成Skill | unit-test-generation | 自动化测试 | ✅ |
| 接口自动化脚本开发Skill | api-automation | 自动化测试 | ✅ |
| UI自动化脚本开发Skill | ui-automation | 自动化测试 | ✅ |
| 测试报告分析Skill | test-report-analysis | 自动化测试 | ✅ |
| 压测场景设计Skill | load-test-scenario-design | 性能压测 | ✅ |
| 压测脚本编写执行Skill | load-test-script | 性能压测 | ✅ |
| 性能瓶颈分析Skill | bottleneck-analysis | 性能压测 | ✅ |
| 优化建议输出Skill | optimization-advice | 性能压测 | ✅ |
| 回答准确性评测Skill | answer-accuracy-eval | AI专项测试 | ✅ |
| 幻觉检测Skill | hallucination-detection | AI专项测试 | ✅ |
| Prompt注入测试Skill | prompt-injection-testing | AI专项测试 | ✅ |
| RAG召回效果评测Skill | rag-evaluation | AI专项测试 | ✅ |

### 运维侧(15 个)

| Skill 名称 | 目录名(skills/ 下) | 归属 Sub-Agent | 状态 |
|---|---|---|---|
| 流水线配置Skill | pipeline-config | CI/CD流水线 | ✅ |
| 镜像构建打包Skill | image-build | CI/CD流水线 | ✅ |
| 多环境配置管理Skill | multi-env-config | CI/CD流水线 | ✅ |
| 流水线故障排查Skill | pipeline-troubleshooting | CI/CD流水线 | ✅ |
| 发布方案设计Skill | release-plan | 发布与部署 | ✅ |
| 容器编排部署Skill | k8s-deployment | 发布与部署 | ✅ |
| 环境初始化Skill | environment-init | 发布与部署 | ✅ |
| 一键回滚执行Skill | one-click-rollback | 发布与部署 | ✅ |
| 监控指标配置Skill | monitoring-metrics | 监控与故障排查 | ✅ |
| 日志分析定位Skill | log-analysis | 监控与故障排查 | ✅ |
| 链路追踪分析Skill | trace-analysis | 监控与故障排查 | ✅ |
| 根因分析Skill | root-cause-analysis | 监控与故障排查 | ✅ |
| 资源用量评估Skill | resource-usage-assessment | 资源与成本管理 | ✅ |
| 成本优化方案Skill | cost-optimization | 资源与成本管理 | ✅ |
| 弹性伸缩配置Skill | auto-scaling-config | 资源与成本管理 | ✅ |

### 安全侧(16 个)

| Skill 名称 | 目录名(skills/ 下) | 归属 Sub-Agent | 状态 |
|---|---|---|---|
| 静态安全测试SAST Skill | sast-scan | 代码安全审计 | ✅ |
| 组件漏洞扫描Skill | dependency-scan | 代码安全审计 | ✅ |
| 硬编码信息检测Skill | hardcoded-secret-detection | 代码安全审计 | ✅ |
| AI代码安全审计Skill | ai-code-security-audit | 代码安全审计 | ✅ |
| 基线安全检测Skill | baseline-security-check | 基础设施安全 | ✅ |
| 容器安全扫描Skill | container-security-scan | 基础设施安全 | ✅ |
| 网络策略配置Skill | network-policy-config | 基础设施安全 | ✅ |
| 权限最小化校验Skill | least-privilege-check | 基础设施安全 | ✅ |
| 敏感数据识别Skill | sensitive-data-identification | 数据安全与隐私 | ✅ |
| 数据脱敏方案Skill | data-masking | 数据安全与隐私 | ✅ |
| 传输存储加密Skill | data-encryption | 数据安全与隐私 | ✅ |
| 泄露风险评估Skill | data-leak-risk-assessment | 数据安全与隐私 | ✅ |
| 合规差距评估Skill | compliance-gap-assessment | 合规与风险评估 | ✅ |
| 风险等级划分Skill | risk-grading | 合规与风险评估 | ✅ |
| 整改建议输出Skill | remediation-plan | 合规与风险评估 | ✅ |
| 安全审计报告生成Skill | security-audit-report | 合规与风险评估 | ✅ |

## 五、调度与门禁使用说明

1. **委派方式**:总控在对话中通过 Agent 工具委派任务,可用 `subagent_type` 指定具体 Agent;任务清单用 TaskCreate/TaskUpdate 维护。
2. **一级主 Agent 是调度者**:接收总控任务 → 拆解 → 委派下属 Sub-Agent → 汇总验收 → 向上交付;不亲自执行业务动作。
3. **二级 Sub-Agent 是执行者**:只有执行权没有调度权(prompt 内禁止调用 Agent 工具);产出标准化交付物。
4. **Skill 是知识/流程规范**:通过 Skill 工具按需加载;Skill 全局可见,但仅限其归属 Sub-Agent 的职责场景使用,越界使用视为违规。
5. **门禁强制**:开发 → 质量评审 → 测试 → 运维,任一环节未过不得流转;安全合规动工前/交付后双重校验;高危运维需总控 + 安全双确认。

## 六、与架构设计文档的机制差异(诚实声明)

| 文档设想 | Claude Code 现实落地 |
|---|---|
| Agent 常驻进程 + 状态机 | Agent 为无状态会话,按需启动用后即弃;状态由总控 TaskList + 交付物文件模拟 |
| Skill 机制性绑定唯一 Sub-Agent | Skill 全局可见,以「归属声明 + prompt 约束 + 总控监督」实现 |
| Skill 为可执行代码文件 | Skill 为流程/规范提示(SKILL.md),需要时可内嵌脚本 |
| 禁止总控跨级调用二级 | 放宽为:默认经一级主 Agent 拆解;单一明确任务总控可直调二级,仍按主 Agent 口径验收 |
| 生成 ProjectControllerAgent.{py/java/ts} 代码框架 | 不生成,文档第三部分仅作设计参考 |

## 七、参与贡献

欢迎广大开发者参与共建:新增 Skill、补充 Sub-Agent、打磨审查清单、修正文档翻译。

- **贡献指南**:[CONTRIBUTING.zh-CN.md](CONTRIBUTING.zh-CN.md)([English](CONTRIBUTING.md))——含命名规范、文件模板、五段式要求、提交流程
- **PR/Issue 模板**:`.github/` 下已内置 PR 自检清单与新 Skill 提议模板
- **行为准则**:[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)

最简单的贡献方式:按照 `code-standard-check` 这类现有 Skill 的格式,新增一个你所在领域缺失的原子 Skill,提交 PR 即可。
