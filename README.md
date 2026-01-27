# Claude Code 工程化实战 · 课程大纲

<p align="center">
  <a href="https://time.geekbang.org/column/intro/101053801"><img src="https://img.shields.io/badge/平台-极客时间-00b4ab?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyTDIgN2wxMCA1IDEwLTV6Ii8+PC9zdmc+" alt="极客时间"/></a>
  <a href="https://time.geekbang.org/column/intro/101053801"><img src="https://img.shields.io/badge/2026-首发专栏-ff6b35?style=for-the-badge" alt="2026首发"/></a>
  <a href="https://time.geekbang.org/column/intro/101053801"><img src="https://img.shields.io/badge/Claude_Code-工程化实战-7c3aed?style=for-the-badge&logo=anthropic&logoColor=white" alt="Claude Code"/></a>
</p>

<div align="center">

<a href="https://time.geekbang.org/column/intro/101053801"><img src="91-Pictures/课程Banner.jpg" alt="Claude Code 工程化实战 Banner" width="800"/></a>

🎯 **这是我为极客时间2026年制作的最新专栏，目标：快速掌握 Claude Code 高阶技能，进行工程化的 Agent 实战**

</div>

<p align="center">
  <img src="https://img.shields.io/badge/📅_上线日期-2026年1月28日-success?style=flat-square&labelColor=2d3748" alt="上线日期"/>
  <img src="https://img.shields.io/badge/状态-敬请期待_🔥-orange?style=flat-square" alt="敬请期待"/>
</p>

<h3 align="center">🚀 从工具使用者到 Agent 构建者的进阶之路</h3>

---

## 开篇词：开发者与智能体的共舞

我们正站在软件工程的转折点上。

过去，开发者写代码、跑测试、查日志、修 Bug——一切尽在掌控。如今，AI Agent 开始参与这场创造：它能读懂你的代码库，理解你的意图，甚至主动提出方案。

但这不是"人被替代"的故事，而是"人机协作"的新篇章。

<div align="center">
  <a href="https://time.geekbang.org/column/intro/101053801"><img src="91-Pictures/极客和AI.png" alt="极客和AI" width="800"/></a>
</div>

Claude Code 不只是一个更聪明的命令行工具。它是一个可编程、可扩展、可组合的 Agent 框架——你可以教它记住项目规范（Memory），拆分成多个专职角色（Sub-Agents），赋予它领域技能（Skills），让它在特定事件时自动响应（Hooks），甚至把它嵌入 CI/CD 流水线无人值守地运行（Headless）。

**这门课的目标：让你从 Claude Code 的"使用者"成长为"驾驭者"。**

你将学会：
- 如何设计 Agent 的"记忆"，让它真正理解你的项目
- 如何拆分任务给子代理，实现关注点分离
- 如何构建可复用的技能包，形成团队资产
- 如何用代码驱动 Agent，构建自动化工作流

这是一场开发者与智能体的共舞——你领舞，它跟随；你编排，它执行。

让我们开始。

---

## 第一部分：基础篇

### 第 1 讲：登高望远 · Claude Code 全景导览
Claude Code 不只是一个命令行助手，而是一个可扩展的 AI Agent 框架——理解其技术栈全貌是掌控它的第一步。

### 第 2 讲：过目不忘 · CLAUDE.md 记忆系统
让 Claude 记住你的项目规范、编码风格和团队约定，从每次重复说明到一次配置永久生效。

---

## 第二部分：子代理（Sub-Agents）专题

### 第 3 讲：分而治之 · 子代理核心概念
把"一个大脑"拆成多个"专职岗位"——理解隔离执行、权限边界和上下文管理的工程价值。

### 第 4 讲：明察秋毫 · 只读型子代理实战
**项目：代码审查员** — 用 `Read/Grep/Glob` 构建一个只能看、不能改的安全审计角色。

### 第 5 讲：去芜存菁 · 高噪声任务处理
**项目：测试运行器 & 日志分析器** — 让子代理去消化 500 行输出，只把结论带回主对话。

### 第 6 讲：众志成城 · 并行探索与流水线编排
**项目：多视角探索 & Bug 修复流水线** — 当任务可以并行或分阶段时，子代理如何协作。

---

## 第三部分：Skills 技能系统专题

### 第 7 讲：触类旁通 · SKILL.md 结构与触发机制
description 不是说明文档，而是触发器——掌握让 Claude 自动发现并加载技能的关键写法。

### 第 8 讲：循序渐进 · 渐进式披露架构设计
**项目：财务分析 Skill** — 目录页、章节、附录三层结构，把 token 利用率提升 98%。

### 第 9 讲：集大成者 · Skills 高级模式
**项目：API 生成器 Skill** — 结合模板、脚本和 allowed-tools，构建完整的领域能力包。

---

## 第四部分：扩展机制

### 第 10 讲：令行禁止 · Slash Commands 自定义命令
**项目：团队标准命令集** — 用 `/review`、`/deploy`、`/commit` 固化团队最佳实践。

### 第 11 讲：未雨绸缪 · Hooks 事件驱动自动化
**项目：安全钩子 & 质量钩子** — 在 Claude 执行工具前后插入检查，实现自动格式化、敏感词拦截等。

### 第 12 讲：海纳百川 · MCP 协议与外部工具连接
通过 Model Context Protocol 把数据库、API、第三方服务变成 Claude 可调用的工具。

---

## 第五部分：生产化与工程化

### 第 13 讲：无人值守 · Headless 模式与 CI/CD 集成
让 Claude Code 在 GitHub Actions 中静默运行——从交互式到全自动的工程化转型。

### 第 14 讲：庖丁解牛 · Agent SDK 基础
`query()` 和 `ClaudeSDKClient` 两种接口——用 Python/TypeScript 编程驱动 Claude 执行任务。

### 第 15 讲：得心应手 · Agent SDK 高级应用
**项目：自动化测试修复 Agent** — 自定义工具、Hooks 拦截、会话管理，构建生产级 AI Agent。

### 第 16 讲：化零为整 · Plugins 插件打包与分发
**项目：团队能力包** — 把 Commands、Skills、Agents、Hooks 组合成可复用的插件，实现团队资产沉淀与共享。

---

<p align="center">
  <a href="https://time.geekbang.org/column/intro/101053801">
    <img src="https://img.shields.io/badge/👉_点击这里开启课程之旅-极客时间-00b4ab?style=for-the-badge&labelColor=2d3748" alt="开启课程之旅"/>
  </a>
</p>

