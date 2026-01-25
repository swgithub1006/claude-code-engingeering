# Skills Q&A

## Q1: Claude Code 中的 Skills 是什么？与其他地方谈的 Skills 有什么关系？

### Claude Code 中 Skills 的定义

**Skills** 是 Claude Code 的"自动发现的能力包"——一种让 Claude **自动推理**何时使用何种专业能力的机制。

### 在 Claude Code 技术栈中的位置

```
Claude Code 技术栈
├── Plugins（顶层容器）
│   ├── Slash Commands（用户手动触发 /xxx）
│   ├── Skills（Claude 自动推理触发）  ← 这里
│   ├── MCP Servers（外部工具连接）
│   └── Hooks（事件驱动）
├── CLAUDE.md（记忆系统）
├── Sub-Agents（子代理）
└── Agent SDK（编程接口）
```

### Skills vs Commands 的核心区别

| 维度 | Commands | Skills |
|------|----------|--------|
| **触发方式** | 用户手动输入 `/command` | Claude **自动**推理判断 |
| **存放位置** | `.claude/commands/` | `skills/` 目录 |
| **主文件** | `*.md` | `SKILL.md`（固定名称） |
| **触发机制** | 精确匹配命令名 | LLM **语义推理**匹配 |

简单说：
- **Commands** = "你告诉 Claude 做什么"（显式触发）
- **Skills** = "Claude 知道什么时候该用什么能力"（隐式触发）

### Skills 的设计特点：渐进式披露

Skills 采用**按需加载**，节省 token：

1. **目录页**（~100 tokens）- 扫描所有 Skill 的 description
2. **章节**（<5k tokens）- 确定相关后，加载 SKILL.md
3. **附录**（按需）- 只有被引用的资源才加载

---

## Q2: 为什么其他 AI 工具和地方也在大谈特谈 Skills？

### "Skills" 是 AI Agent 领域的通用概念

**Skills 不是 Claude Code 独创的术语**，而是整个 AI Agent 生态系统中广泛使用的概念。不同平台对 Skills 的实现方式不同，但核心思想一致：

### 各平台/框架中的 Skills 概念对比

| 平台/框架 | Skills 的叫法 | 核心思想 |
|-----------|--------------|---------|
| **Claude Code** | Skills | 自动发现的能力包，LLM 推理触发 |
| **OpenAI GPTs** | Actions / Custom Instructions | 预定义的能力和行为模式 |
| **LangChain** | Tools / Toolkits | 可调用的功能模块 |
| **AutoGPT** | Skills / Abilities | Agent 可执行的原子操作 |
| **Microsoft Copilot** | Skills / Plugins | 扩展 Copilot 能力的模块 |
| **Semantic Kernel** | Skills / Plugins | 可组合的 AI 能力单元 |
| **CrewAI** | Tools | Agent 可使用的工具集 |

### 为什么 "Skills" 成为热门词汇？

#### 1. AI Agent 范式转变

```
传统 LLM 使用方式：
  用户 → Prompt → LLM → 回答

Agent 范式：
  用户 → Agent → [选择 Skill] → [执行] → [反馈] → 结果
                     ↑
              这就是 Skills 的作用
```

Agent 需要**模块化的能力**来完成复杂任务，Skills 就是这些能力的封装。

#### 2. 能力组合的需求

```
复杂任务 = Skill A + Skill B + Skill C

例如："帮我分析这个 PR 并部署到测试环境"
     = Code Review Skill + Security Check Skill + Deploy Skill
```

#### 3. 可扩展性要求

- **核心 Agent** 保持轻量
- **Skills** 作为插件按需加载
- 社区可以贡献新 Skills

### Claude Code Skills 的独特之处

相比其他平台，Claude Code 的 Skills 有几个独特设计：

| 特性 | Claude Code | 其他平台（通常） |
|------|-------------|-----------------|
| **触发方式** | LLM 语义推理 | 显式调用或关键词匹配 |
| **加载策略** | 渐进式披露 | 一次性加载 |
| **定义格式** | Markdown + YAML frontmatter | JSON/YAML/Code |
| **Token 优化** | 按需加载，节省 98% | 通常全量加载 |

### 行业趋势：从 Tools 到 Skills

```
2022: Tools（工具）
      └─ 简单的函数调用

2023: Toolkits（工具包）
      └─ 相关工具的集合

2024-2025: Skills（技能）
      └─ 带有上下文、知识、策略的完整能力包
      └─ 强调"知道什么时候用"而不只是"能做什么"
```

**Skills 比 Tools 更高级的地方：**
- Tools：我能调用这个 API
- Skills：我知道什么时候该调用这个 API，怎么解读结果，失败了怎么处理

### 总结

| 问题 | 答案 |
|------|------|
| Skills 是 Claude Code 独有的吗？ | 不是，是 AI Agent 领域的通用概念 |
| 为什么都在谈 Skills？ | 因为 Agent 需要模块化、可组合的能力 |
| Claude Code 的 Skills 有什么特别？ | 渐进式披露、LLM 语义推理触发、Markdown 定义 |
| Skills 和 Tools 什么区别？ | Skills = Tools + 知识 + 策略 + 上下文 |

---

## Q3: SKILL.md 文件结构

### 最简结构

```markdown
---
name: code-reviewing
description: Review code for quality, security, and best practices. Use when the user asks for code review, wants feedback on their code, mentions reviewing changes, or asks about code quality.
allowed-tools:
  - Read
  - Grep
  - Glob
---

# Code Review Skill

[具体指令内容...]
```

### Frontmatter 字段

| 字段 | 必需 | 说明 |
|------|------|------|
| `name` | 是 | 唯一标识符（小写字母/数字/连字符） |
| `description` | 是 | **触发器**：决定何时激活（最重要！） |
| `allowed-tools` | 否 | 限制可用工具，增强安全性 |
| `user-invocable` | 否 | 是否显示在 /help 中 |

### description 的重要性

**description 是最重要的字段** —— 它决定 Skill 何时被 Claude 激活。

**不好的 description：**
```yaml
description: Handles PDFs
```

**好的 description：**
```yaml
description: Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction.
```

---

## Q4: Skill 目录结构

### 基础结构（最小化）

```
my-skill/
└── SKILL.md              # 必需：主指令文件
```

### 完整结构（带资源）

```
financial-analyzer/
├── SKILL.md              # 必需：主指令文件
├── REFERENCE.md          # 可选：API 参考文档
├── EXAMPLES.md           # 可选：使用示例
├── PATTERNS.md           # 可选：框架模式
├── STANDARDS.md          # 可选：规范标准
├── scripts/              # 可选：可执行脚本
├── templates/            # 可选：标准化模板
└── resources/            # 可选：资源文件
```

### 渐进式加载示例

| 场景 | 加载的文件 | Token 消耗 |
|------|-----------|-----------|
| 简单请求 | SKILL.md | ~800 |
| 框架特定 | SKILL.md + PATTERNS.md | ~1200 |
| 完整生成 | SKILL.md + 多个文件 | ~2000 |
| 传统方式 | 全部 | ~3000+ |

---

## 参考资源

- [tutorial.md](./tutorial.md) - 完整教程
- [01-basic-skill/](./projects/01-basic-skill/) - 基础 Skill 示例
- [02-progressive-skill/](./projects/02-progressive-skill/) - 渐进式 Skill 示例
- [Anthropic Skills 仓库](https://github.com/anthropics/skills) - 官方 Skills 集合
