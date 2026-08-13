# FullFlow DevAgent

**A full-chain software development agent system for Claude Code** — 6 master agents, 25 sub-agents, and 96 atomic skills covering product, development, quality, testing, operations, and security. From idea to production, with mandatory quality gates and a security layer that runs through every stage.

[中文文档 → README.zh-CN.md](README.zh-CN.md)

> ⚠️ This project's content was AI-assisted. Please evaluate its suitability before use.

## Highlights

- **4-tier hierarchy**: Orchestrator (main conversation) → 6 master agents → 25 sub-agents → 96 atomic skills
- **Full pipeline**: Requirements → Development → Quality review → Testing → Ops delivery
- **Enforced gates**: No review pass, no testing. No test pass, no release. Security & compliance checks at every hand-off
- **Pure prompts, zero code**: Everything is markdown prompt definitions (`.md` files) — nothing to compile, nothing to install
- **Works with any tech stack**: Agents are technology-agnostic; skills provide methodology

## Architecture

```
Project Orchestrator (main conversation + CLAUDE.md)
    │
    ├── 🟡 Product & Requirements Master Agent ── 4 sub-agents / 15 skills (front of the pipeline)
    ├── 🟢 Full-Stack & AI Dev Master Agent ───── 5 sub-agents / 19 skills
    ├── 🟣 Quality & Code Review Master Agent ─── 4 sub-agents / 15 skills
    ├── 🟠 Test Engineering Master Agent ──────── 4 sub-agents / 16 skills
    ├── 🔵 Ops & Delivery Master Agent ───────── 4 sub-agents / 15 skills
    └── 🔴 Security & Compliance Master Agent ─── 4 sub-agents / 16 skills (cross-cutting)
```

- **Forward flow**: requirements → development → quality review → test acceptance → ops delivery, with security & compliance verification at every stage
- **Reverse flow**: any problem found rolls back to the previous stage for rework; the orchestrator tracks closure
- **Totals**: 6 master agents + 25 sub-agents + 96 atomic skills

## Repository Layout

```
fullflow-dev-agent/
├── CLAUDE.md                          # Orchestrator rules (scheduling / gates / circuit breaking)
├── README.md                          # This file (English)
├── README.zh-CN.md                    # Full inventory in Chinese
├── LICENSE                            # MIT
└── .claude/
    ├── agents/                        # Agent definitions (31 files)
    │   ├── product-master.md          # 6 master agents (scheduling role, hold the Agent tool)
    │   ├── dev-master.md
    │   ├── qa-master.md
    │   ├── test-master.md
    │   ├── ops-master.md
    │   ├── sec-master.md
    │   └── *-sub.md                   # 25 sub-agents (execution role, must not call each other)
    └── skills/                        # Atomic skills (96 dirs, one SKILL.md each)
        └── <skill-name>/SKILL.md
```

## Installation

**Project-level (recommended):** copy `.claude/` and `CLAUDE.md` into the root of your project repo.

**Global:** copy `.claude/agents/` and `.claude/skills/` into `~/.claude/`, and merge `CLAUDE.md` into your global `~/.claude/CLAUDE.md`.

Agents and skills are then automatically discovered by Claude Code. Dispatch them by name, e.g. "Delegate to the Architecture Design Sub-Agent".

## Agent Inventory (31)

### 🟡 Product & Requirements Master Agent (`product-master`)

| File | Agent | Responsibility |
|---|---|---|
| product-master.md | Product & Requirements Master Agent | Requirements breakdown, PRD control, prototype & interaction orchestration |
| product-requirement-sub.md | Requirements Analysis Sub-Agent | Research, user story splitting, acceptance criteria |
| product-prd-sub.md | PRD & Product Design Sub-Agent | PRD writing, information architecture, functional specs, version planning |
| product-prototype-sub.md | Prototype & Interaction Sub-Agent | Wireframes, interaction flows, Figma designs, design walkthrough |
| product-backlog-sub.md | Change & Prioritization Sub-Agent | Change assessment, prioritization, roadmap planning |

### 🟢 Full-Stack & AI Dev Master Agent (`dev-master`)

| File | Agent | Responsibility |
|---|---|---|
| dev-master.md | Full-Stack & AI Dev Master Agent | Orchestrates architecture, frontend/backend, AI engineering, middleware |
| dev-architecture-sub.md | Architecture Design Sub-Agent | Tech selection, AI architecture, DB modeling, API protocols |
| dev-backend-sub.md | Backend Dev Sub-Agent | Backend code, scaffolding, DB mapping, LLM service wrappers |
| dev-frontend-sub.md | Frontend Dev Sub-Agent | Multi-platform pages, component library, build config, AI UI components |
| dev-ai-engineering-sub.md | AI Engineering Sub-Agent | RAG pipeline, prompt optimization, agent orchestration, vector DB tuning |
| dev-middleware-sub.md | Middleware & Infra Sub-Agent | Redis caching, message queues, API gateway config |

### 🟣 Quality & Code Review Master Agent (`qa-master`)

| File | Agent | Responsibility |
|---|---|---|
| qa-master.md | Quality & Code Review Master Agent | Independent quality gate for code, architecture, tech debt |
| qa-code-review-sub.md | Code Review Sub-Agent | Coding standards, logic defects, performance hazards, AI code review |
| qa-architecture-review-sub.md | Architecture Review Sub-Agent | Architecture compliance, dependency analysis, design patterns, debt metrics |
| qa-metrics-sub.md | Quality Metrics Sub-Agent | Cyclomatic complexity, coverage, duplicate code, quality trends |
| qa-tech-debt-sub.md | Tech Debt Sub-Agent | Debt grading, repayment prioritization, refactoring plans |

### 🟠 Test Engineering Master Agent (`test-master`)

| File | Agent | Responsibility |
|---|---|---|
| test-master.md | Test Engineering Master Agent | Orchestrates functional, automation, performance, AI-special testing |
| test-functional-sub.md | Functional Testing Sub-Agent | Test case generation, scenario execution, defect grading, regression |
| test-automation-sub.md | Test Automation Sub-Agent | Unit/API/UI automation scripts and report analysis |
| test-performance-sub.md | Performance Testing Sub-Agent | Load test design, execution, bottleneck analysis, tuning advice |
| test-ai-special-sub.md | AI Special Testing Sub-Agent | Accuracy evaluation, hallucination detection, prompt injection, RAG eval |

### 🔵 Ops & Delivery Master Agent (`ops-master`)

| File | Agent | Responsibility |
|---|---|---|
| ops-master.md | Ops & Delivery Master Agent | Orchestrates CI/CD, releases, monitoring, cost management |
| ops-cicd-sub.md | CI/CD Pipeline Sub-Agent | Pipeline config, image builds, multi-env config, pipeline troubleshooting |
| ops-deploy-sub.md | Release & Deploy Sub-Agent | Release plans, container orchestration, env init, one-click rollback |
| ops-monitor-sub.md | Monitoring & Troubleshooting Sub-Agent | Dashboards, log analysis, tracing, root cause analysis |
| ops-cost-sub.md | Resource & Cost Sub-Agent | Resource assessment, cost optimization, auto-scaling config |

### 🔴 Security & Compliance Master Agent (`sec-master`, cross-cutting)

| File | Agent | Responsibility |
|---|---|---|
| sec-master.md | Security & Compliance Master Agent | Lifecycle-wide security audit, veto power, reports to orchestrator |
| sec-code-audit-sub.md | Code Security Audit Sub-Agent | SAST, dependency vulnerabilities, hardcoded secrets, AI code security |
| sec-infra-sub.md | Infrastructure Security Sub-Agent | Baseline checks, container scans, network policies, least privilege |
| sec-data-sub.md | Data Security & Privacy Sub-Agent | Sensitive data identification, masking, encryption, leak risk |
| sec-compliance-sub.md | Compliance & Risk Sub-Agent | Compliance gaps, risk grading, remediation plans, audit reports |

## Skill Inventory (96)

| Skill | Directory | Owner Sub-Agent |
|---|---|---|
| Requirement Research Skill | requirement-research | Requirements Analysis |
| User Story Splitting Skill | user-story-splitting | Requirements Analysis |
| Acceptance Criteria Skill | acceptance-criteria | Requirements Analysis |
| Competitor & Market Analysis Skill | competitor-analysis | Requirements Analysis |
| PRD Writing Skill | prd-writing | PRD & Product Design |
| Information Architecture Skill | information-architecture | PRD & Product Design |
| Functional Spec Skill | functional-spec | PRD & Product Design |
| Version Planning Skill | version-planning | PRD & Product Design |
| Wireframe Design Skill | wireframe-design | Prototype & Interaction |
| Interaction Flow Design Skill | interaction-flow-design | Prototype & Interaction |
| Figma Design Generation Skill | figma-design-generation | Prototype & Interaction |
| Design Walkthrough Skill | design-walkthrough | Prototype & Interaction |
| Requirement Change Assessment Skill | requirement-change-assessment | Change & Prioritization |
| Requirement Prioritization Skill | requirement-prioritization | Change & Prioritization |
| Roadmap Planning Skill | roadmap-planning | Change & Prioritization |
| Full-Stack Architecture Selection Skill | fullstack-architecture-selection | Architecture Design |
| AI App Architecture Design Skill | ai-architecture-design | Architecture Design |
| Database Modeling Skill | database-modeling | Architecture Design |
| API Protocol Definition Skill | api-protocol-definition | Architecture Design |
| Multi-Language Code Generation Skill | code-generation | Backend Dev |
| Scaffold Setup Skill | scaffold-setup | Backend Dev |
| ORM Mapping Skill | orm-mapping | Backend Dev |
| LLM Service Wrapper Skill | llm-service-wrapper | Backend Dev |
| Multi-Platform Page Generation Skill | multi-platform-page-generation | Frontend Dev |
| Component Library Skill | component-library | Frontend Dev |
| Frontend Engineering Config Skill | frontend-engineering-config | Frontend Dev |
| AI Interactive Components Skill | ai-interactive-components | Frontend Dev |
| RAG Pipeline Skill | rag-pipeline | AI Engineering |
| Prompt Engineering Skill | prompt-engineering | AI Engineering |
| Agent Orchestration Skill | agent-orchestration | AI Engineering |
| Vector DB Tuning Skill | vector-db-tuning | AI Engineering |
| Cache Strategy Skill | cache-strategy | Middleware & Infra |
| Message Queue Planning Skill | mq-planning | Middleware & Infra |
| API Gateway Config Skill | api-gateway-config | Middleware & Infra |
| Coding Standard Check Skill | code-standard-check | Code Review |
| Code Defect Review Skill | code-defect-review | Code Review |
| Performance Hazard Detection Skill | performance-hazard | Code Review |
| AI Code Review Skill | ai-code-review | Code Review |
| Architecture Compliance Check Skill | architecture-compliance | Architecture Review |
| Dependency Analysis Skill | dependency-analysis | Architecture Review |
| Design Pattern Evaluation Skill | design-pattern-evaluation | Architecture Review |
| Tech Debt Quantification Skill | tech-debt-quantification | Architecture Review |
| Complexity Metrics Skill | complexity-metrics | Quality Metrics |
| Coverage Metrics Skill | coverage-metrics | Quality Metrics |
| Duplicate Code Detection Skill | duplicate-code-detection | Quality Metrics |
| Quality Trend Analysis Skill | quality-trend-analysis | Quality Metrics |
| Debt Identification & Grading Skill | debt-identification-grading | Tech Debt |
| Debt Repayment Priority Skill | debt-repayment-priority | Tech Debt |
| Refactoring Plan Skill | refactoring-plan | Tech Debt |
| Test Case Generation Skill | test-case-generation | Functional Testing |
| Business Scenario Testing Skill | business-scenario-testing | Functional Testing |
| Defect Grading & Reporting Skill | defect-grading-report | Functional Testing |
| Regression Case Selection Skill | regression-case-selection | Functional Testing |
| Unit Test Generation Skill | unit-test-generation | Test Automation |
| API Automation Skill | api-automation | Test Automation |
| UI Automation Skill | ui-automation | Test Automation |
| Test Report Analysis Skill | test-report-analysis | Test Automation |
| Load Test Scenario Design Skill | load-test-scenario-design | Performance Testing |
| Load Test Scripting Skill | load-test-script | Performance Testing |
| Bottleneck Analysis Skill | bottleneck-analysis | Performance Testing |
| Optimization Advice Skill | optimization-advice | Performance Testing |
| Answer Accuracy Evaluation Skill | answer-accuracy-eval | AI Special Testing |
| Hallucination Detection Skill | hallucination-detection | AI Special Testing |
| Prompt Injection Testing Skill | prompt-injection-testing | AI Special Testing |
| RAG Evaluation Skill | rag-evaluation | AI Special Testing |
| Pipeline Config Skill | pipeline-config | CI/CD Pipeline |
| Image Build Skill | image-build | CI/CD Pipeline |
| Multi-Env Config Skill | multi-env-config | CI/CD Pipeline |
| Pipeline Troubleshooting Skill | pipeline-troubleshooting | CI/CD Pipeline |
| Release Plan Skill | release-plan | Release & Deploy |
| K8s Deployment Skill | k8s-deployment | Release & Deploy |
| Environment Init Skill | environment-init | Release & Deploy |
| One-Click Rollback Skill | one-click-rollback | Release & Deploy |
| Monitoring Metrics Skill | monitoring-metrics | Monitoring & Troubleshooting |
| Log Analysis Skill | log-analysis | Monitoring & Troubleshooting |
| Trace Analysis Skill | trace-analysis | Monitoring & Troubleshooting |
| Root Cause Analysis Skill | root-cause-analysis | Monitoring & Troubleshooting |
| Resource Usage Assessment Skill | resource-usage-assessment | Resource & Cost |
| Cost Optimization Skill | cost-optimization | Resource & Cost |
| Auto-Scaling Config Skill | auto-scaling-config | Resource & Cost |
| SAST Scan Skill | sast-scan | Code Security Audit |
| Dependency Vulnerability Scan Skill | dependency-scan | Code Security Audit |
| Hardcoded Secret Detection Skill | hardcoded-secret-detection | Code Security Audit |
| AI Code Security Audit Skill | ai-code-security-audit | Code Security Audit |
| Baseline Security Check Skill | baseline-security-check | Infrastructure Security |
| Container Security Scan Skill | container-security-scan | Infrastructure Security |
| Network Policy Config Skill | network-policy-config | Infrastructure Security |
| Least Privilege Check Skill | least-privilege-check | Infrastructure Security |
| Sensitive Data Identification Skill | sensitive-data-identification | Data Security & Privacy |
| Data Masking Skill | data-masking | Data Security & Privacy |
| Data Encryption Skill | data-encryption | Data Security & Privacy |
| Data Leak Risk Assessment Skill | data-leak-risk-assessment | Data Security & Privacy |
| Compliance Gap Assessment Skill | compliance-gap-assessment | Compliance & Risk |
| Risk Grading Skill | risk-grading | Compliance & Risk |
| Remediation Plan Skill | remediation-plan | Compliance & Risk |
| Security Audit Report Skill | security-audit-report | Compliance & Risk |

## Scheduling & Gates

1. **Delegation**: the orchestrator delegates tasks via the Agent tool, optionally targeting a specific agent with `subagent_type`; task lists are tracked with TaskCreate/TaskUpdate
2. **Master agents schedule**: receive a task → break it down → delegate to sub-agents → consolidate & accept → deliver upward; they never perform the work themselves
3. **Sub-agents execute**: execution rights only, no scheduling rights (calling the Agent tool is forbidden in their prompts); they produce standardized deliverables
4. **Skills are methodology**: loaded on demand via the Skill tool; each skill belongs to one sub-agent's scope — using a skill outside its owner's scenarios is a violation
5. **Gates are mandatory**: development → quality review → testing → ops; no stage may be skipped; security & compliance checks happen before work starts and after delivery; high-risk ops require orchestrator + security double confirmation

## Honest Notes on Design vs. Claude Code Reality

| Original design assumption | How it actually works in Claude Code |
|---|---|
| Long-running agent processes with a state machine | Agents are stateless sessions, started on demand and discarded; state is simulated via orchestrator task lists + deliverable files |
| Skills mechanically bound to a single sub-agent | Skills are globally visible; ownership is enforced by declaration + prompt constraints + orchestrator oversight |
| Skills as executable code files | Skills are methodology prompts (SKILL.md); scripts can be embedded when needed |
| Orchestrator forbidden from calling sub-agents directly | Relaxed: by default tasks go through master agents; for single clearly-scoped tasks the orchestrator may call a sub-agent directly, still accepting against the master agent's criteria |
| Generate a ProjectControllerAgent.{py/java/ts} code framework | Not generated; that part of the original design doc serves as reference only |

## Contributing

Contributions are warmly welcome — new skills, sharper checklists, better rules, translations. See [CONTRIBUTING.md](CONTRIBUTING.md) for conventions and the submission workflow ([中文贡献指南](CONTRIBUTING.zh-CN.md)). All participants are expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## License

[MIT](LICENSE)
