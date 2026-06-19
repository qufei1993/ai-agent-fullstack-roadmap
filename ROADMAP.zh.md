# AI Agent 全栈开发 Roadmap

> 面向具备 Node.js / 前端基础的开发者，建立 AI Agent 全栈开发的能力地图。TypeScript 为主线，但不拘泥——Python 生态在 Agent 工程上积累更深（如 LangGraph、CrewAI 等），成熟处直接取用，不因语言偏好牺牲方案质量。重点说明学习顺序、核心概念、工程边界和技术选型，不展开具体项目实战。

---

## 如何阅读这份 Roadmap

7 个阶段建议按顺序学，但不必全部深挖。用下面三类标签做取舍：

- 🟢 **必学主线**：AI 辅助开发、LLM API、结构化输出、RAG、Agent Loop、全栈部署
- 🔵 **工程贯穿线**：安全 · 评测 · 可观测性 · 成本 —— 贯穿每个阶段，不是上线前才补
- 🟡 **进阶选修**：MCP 开发、Skills、Sub-agent、多 Agent、本地推理、Pi 等极简底座

---

## 阶段一：AI 辅助开发工作流

### AI 编程工具

- Cursor — AI 原生编辑器
- Claude Code — 终端 AI 编程助手
- Codex — OpenAI 终端 AI 编程助手
- GitHub Copilot — 代码补全
- Windsurf / Trae

> AI 辅助开发的核心不是换编辑器，而是建立 Spec、上下文、执行、Review、测试和迭代的协作流程。

### AI 编程方法论

- 规格驱动开发（Spec-Driven Development）— 先写规格再让 AI 实现
- 上下文工程（Context Engineering）— 设计上下文，精准指导 AI
- Vibe Coding — AI 写代码，人做 Review 与决策（需保持代码 Review 与验证，不是随意开发）
- Harness 工程 — 为 AI 任务构建可重复执行、可评估的执行框架
- Loop 工程（Loop Engineering）— 从手动 prompt 转向设计自主循环：让 AI 在"执行→观察→修正"中持续迭代，靠测试/构建等反馈信号驱动，人负责设定可验证目标、终止条件与护栏（如 Ralph 技术）
- 人机协作分工原则

### 项目规则与记忆配置

- **AGENTS.md** — 多 Agent 编程工具共享项目指令的开放格式（Agentic AI Foundation / Linux Foundation 维护），Codex 等工具已支持，更多 Agent 编程工具正在采用或兼容
- **CLAUDE.md** — Claude Code 专属，支持目录层级覆盖
- **.cursor/rules/\*.mdc** — Cursor 多文件规则，支持按文件类型作用域
- **.github/copilot-instructions.md** — GitHub Copilot 项目指令
- **.windsurfrules** — Windsurf 配置
- 规则内容：代码规范 / 技术栈约定 / 提交规范 / 安全禁区 / 部署步骤

### MCP & Skills 使用（在 AI 编程工具中）

- 在 Cursor / Claude Code / Windsurf 中配置 MCP Server
- 常用社区 MCP Server（文件系统 / 数据库 / 搜索 / SaaS 工具）
- 在 AI 编程工具中加载和使用 Skills
- MCP Server 选型与安全评估

### AI 辅助调试

- 让 AI 解读报错信息与堆栈追踪
- 根因分析与定位（Root Cause Analysis）
- 结合执行日志做上下文提问
- AI 辅助排查性能与内存问题

### AI 辅助测试生成

- TDD with AI：先写规格让 AI 生成测试，再驱动实现
- 根据需求文档生成测试用例
- AI 补全测试覆盖率盲区
- 测试结果作为 AI 迭代反馈

### 工程设计思维

- 需求分析与用例拆解
- 技术选型
- 系统架构设计
- API 接口设计

---

## 阶段二：LLM API 与结构化交互

### 大模型基础概念

- Token / Context Window 机制
- Temperature / Top-p / Top-k
- 模型系列选型：Anthropic Claude 系列 / OpenAI GPT 系列 / Google Gemini 系列
- 模型选型维度：推理能力、延迟、成本、上下文长度、多模态、工具调用支持
- 多模态（文本 / 图像 / 音频）
- 成本与限速管理

### API 集成

- OpenAI API / Anthropic API
- 统一接口（OpenRouter / LiteLLM）
- Streaming 流式响应

### Prompt Engineering

- System Prompt vs User Prompt
- Few-shot Learning
- 任务分解与推理引导（推理模型通常内部处理，非推理模型更依赖显式引导）
- 提示安全与不可信输入处理（降低 Prompt Injection / Jailbreak 风险）

### 结构化输出与工具调用

- Structured Output — 约束模型输出格式，遵守 JSON Schema
- Tool Calling — 让模型请求执行外部操作
- JSON Mode — 保证合法 JSON，不代表业务语义正确，仍需应用层验证
- JSON Schema 定义 / Zod 验证 / 无效输出修复与重试

### 基础 SDK

- Vercel AI SDK
- LangChain.js / LangChain（Python）
- OpenAI SDK / Anthropic SDK

---

> **工程贯穿原则：** 安全、评测、可观测性和成本控制不是上线前才补的能力。从第一个 LLM API 调用开始，就应记录输入输出、Trace、错误、延迟、Token 使用量、成本和失败案例。

---

## 阶段三：RAG 知识库应用

### Embedding 与向量检索

- Embedding 原理与模型选型
- 文本分块策略（Chunking）— 块太大上下文冗余，块太小丢失语义
- 相似度计算（余弦相似度 / 点积）
- Hybrid Search（向量 + 全文）

### 向量数据库

- PostgreSQL + pgvector（默认推荐，兼顾全文检索）
- Chroma（本地开发）
- Pinecone / Weaviate / Qdrant（规模化场景）

### RAG 管道

- 数据摄入（PDF / 网页 / 数据库 / API）
- 文档清洗与预处理 / 索引构建与增量更新
- Query Rewrite / 查询分解
- 检索与重排（Reranking）
- 上下文拼装与引用追溯
- 权限过滤（Metadata Filter / 租户隔离）— 必须在检索层完成，不能只靠 Prompt
- 文档版本与时效管理

### RAG 失败模式处理

- 检索不到答案时如何拒答
- 检索到文档但答案不忠实时如何识别
- 召回质量下降的检测与告警

### RAG 框架 & 评测

- LlamaIndex.TS / LlamaIndex（Python）/ LangChain RAG
- 评测指标：Recall@K / Precision@K / MRR / NDCG / 引用正确率 / 答案忠实度
- RAG 数据投毒防护 / 跨租户信息泄漏防护

---

## 阶段四：Tool Calling 与 Mini Agent Loop

> 核心是一个 while 循环 + Function Calling，真正复杂的部分在上下文管理、工具执行、错误处理和权限控制。不依赖框架手写，理解 Agent 底层机制。

**Mini Coding Agent 分三个学习层级：**

### 基础理解（必懂）

- Agent 三要素：大脑（LLM）+ 工具（Tools）+ 循环（Agent Loop）
- Tool Use / Function Calling
- ReAct 循环：推理（Reason）→ 行动（Act）→ 观察（Observe）→ 循环
- 消息历史作为对话上下文（Mini Agent 的简化起点；生产级 Agent 需额外的执行状态、检查点与幂等键）
- 循环终止条件：LLM 停止调用工具即退出

### 核心实现（应会）

- 工具三层架构：注册表（Registry）→ 分发器（Dispatcher）→ 实现（Implementation）
- JSON Schema 定义工具接口（与语言无关）
- 核心工具集：Read / Write / Edit / Bash / Glob / Grep
- 流式响应处理：中途检测工具调用，**累积完整参数后**再执行
- 工具输出截断策略 / 错误作为反馈返回
- 权限分级：只读 → 工作区写入 → 危险完全访问
- 高风险操作人工确认 / Middleware Hooks
- 步骤上限与 Token 预算守护
- System Prompt 工程（行为规范 / 工具使用原则 / 先读后写）

### 进阶扩展（选修）

- 上下文压缩（Context Compaction）：HeadTail 裁剪 / LLM 摘要替换（需保护完整 tool-call/result 配对，生产系统应按语义回合压缩）
- Sub-agent 上下文隔离
- MCP Client 接入（连接并调用已有 MCP Server）
- Skills 加载与按需执行

### 与成熟 Coding Agent 对比学习

- Claude Code 完整架构解析（Agent Loop / 工具系统 / 权限模型 / MCP / Skills）
- Codex CLI 设计对比
- Pi（earendil-works/pi）— 极简实现对比：仅 4 个核心工具、系统提示 <1000 token
- 框架（LangGraph / Vercel AI SDK）做了哪些抽象

---

## 阶段五：Agent 应用工程

> **Workflow 与 Agent 的边界：** 能用确定性 Workflow 解决的问题，不要优先设计成 Agent。Agent 更适合目标开放、路径不确定、需要动态选择工具并根据环境反馈调整的任务。Workflow 是预定义路径，Agent 是模型动态决定过程和工具选择。

### 记忆管理

- 会话状态（消息历史、工具调用、执行结果）
- 工作流状态（任务步骤、检查点、审批状态）
- 用户记忆（偏好、长期档案）
- 语义记忆（可检索知识，不局限于向量存储）
- 产物记忆（文件、报告、代码、执行记录）
- 记忆治理（过期、删除、隐私隔离）

### Agent 安全与可靠性

- 停止条件与步骤上限
- Token / 时间 / 费用预算控制
- Human-in-the-Loop — 不只是安全审批，还包括补充信息、纠错、恢复和分支决策
- 最小权限与工具白名单
- 错误处理与失败恢复

### MCP（Model Context Protocol）— 开发自定义 MCP Server

- Host / Client / Server 职责划分
- Tools / Resources / Prompts 边界
- STDIO 与 Streamable HTTP 传输层
- 生命周期与能力协商
- OAuth 2.1 授权 / Scope 最小化 / Token audience 校验
- 工具输入验证与调用审计
- 恶意 Shadow MCP Server 风险

### Agent Skills（技能封装）— 进阶能力

- Skills 原理与规范（agentskills.io）
- 自定义 Skill 开发
- Skill 跨平台复用（Claude Code / 其他 Agent 平台）
- Skills 与 MCP 协作模式

### Agent 框架

> **原则：TypeScript 主线，Python 不避。** 本路线图以 Node.js/TS 为默认，但 Python 生态在 Agent 工程上积累更深——复杂工作流和长任务编排等场景，LangGraph（Python）比 LangGraph.js 更成熟稳定，选型时不因语言偏好牺牲方案质量。

| 层级 | 推荐 | 说明 |
|------|------|------|
| TypeScript 主线 | Vercel AI SDK ToolLoopAgent | 前端全栈首选，与 Next.js/Streaming UI 无缝衔接 |
| 极简可组合底座 | Pi（pi-agent-core，OpenClaw 同款，纯 TS） | 源码极简，适合学习 Agent 底层机制后做可组合定制 |
| 厂商 SDK | OpenAI Agents SDK / Claude Agent SDK | 原生集成，快速启动 |
| 复杂状态工作流 | **LangGraph（Python）** ⭐ | 有状态 DAG + 检查点 + Human-in-the-Loop，生产验证最充分；LangGraph.js 功能追赶中，简单场景可用 |
| 多 Agent 编排 | CrewAI / AutoGen AG2（Python） | 角色分工 + 工作流编排，快速原型首选 |

### 多 Agent 系统

- 角色与任务分工
- 工作流编排
- 子 Agent（Subagent）
- 多 Agent 适用边界

---

## 阶段六：AI 全栈产品化

### 前端 AI 化

- Vercel AI SDK（Chat / Generative UI / Object Generation / Tool Calling）
- Streaming UI / 工具调用状态展示 / 引用来源展示
- 用户确认与审批 UI / 断线恢复与取消
- 文件与多模态输入
- 本地推理（WebGPU / Transformers.js）

### 全栈框架与数据层

- 复用已有能力：Next.js / Nest / Hono、Route Handlers（BFF）、PostgreSQL、Redis、容器化（已具备，不展开）
- 实时通信：WebSocket / SSE（承载流式响应）
- AI 应用新增的数据需求：向量库（语义检索）、会话与记忆持久化、长任务/检查点状态、多模态文件 → 对象存储

### AI 安全（在已有 Web 安全之上的增量）

- 把 LLM 输出与外部内容当不可信数据 —— 全栈层防 Prompt Injection
- 多租户 RAG 数据隔离 —— 检索层强制过滤，不只靠 Prompt
- LLM 日志与 Trace 脱敏（PII / 密钥不入日志）
- LLM API Key 与 Secret 管理
- 传统 authN/authZ（OAuth/OIDC、RBAC/ABAC）复用已有，不展开

### 部署与运行时（AI 特有挑战）

- 长耗时 agent 任务 ↔ Serverless 超时 → Durable Workflow / 后台任务队列
- 流式响应基础设施 —— SSE 长连接、断线恢复、请求取消
- Edge AI（Cloudflare Workers）/ 本地推理部署
- 平台选型：Vercel / Cloudflare / Railway / Render / Docker（复用已有，按需选）
- 对象存储 / Webhook

---

## 阶段七：生产级运营

### 可观测性

**先建立通用概念**

- Trace / Span 模型
- 模型调用 / Agent 执行 / 工具调用 / 检索过程追踪
- Token 使用量 / 延迟 / 错误率 / 单次任务成本
- 用户反馈收集

**再选型工具平台**

- LangSmith（LangChain 生态）
- Langfuse（开源，全框架支持）
- Helicone（轻量代理层）
- OpenTelemetry GenAI 语义约定（仍处于 Development 状态）

### 评估与测试

- 检索质量：Recall@K / Precision@K / MRR / NDCG
- 回答质量：语义相似度 / 引用与事实正确率 / 答案忠实度
- Agent 质量：任务成功率 / Tool Call 正确率 / 执行轨迹分析
- Schema 合规率 / 安全违规率
- A/B 测试
- CI Eval（评测集纳入持续集成）

### 成本优化

- Prompt Caching（提示缓存）
- Token 压缩（上下文裁剪）
- 模型路由（大小模型分级调用）
- 批量推理
- 成本监控与预算告警

### 可靠性

- 限速与重试策略
- 故障降级（Fallback）与多模型备份
- 流量控制与熔断
- 幂等性设计
- 并发控制
- 灰度发布
