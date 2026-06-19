# AI Agent 全栈开发 Roadmap

## 阶段一：AI 辅助开发工作流

### AI 编程工具
- Cursor
- Claude Code
- Codex
- GitHub Copilot
- Windsurf / Trae

### AI 编程方法论
- 规格驱动开发
- 上下文工程
- Vibe Coding
- Harness 工程
- Loop 工程
- 人机协作分工

### 项目规则配置
- AGENTS.md（多工具通用）
- CLAUDE.md
- .cursor/rules
- copilot-instructions.md
- .windsurfrules

### MCP & Skills 使用
- 配置 MCP Server
- 社区 MCP Server
- 加载使用 Skills
- 选型与安全评估

### AI 辅助调试
- 报错与堆栈解读
- 根因分析定位
- 日志上下文提问
- 性能与内存排查

### AI 辅助测试生成
- TDD with AI
- 需求生成用例
- 覆盖率盲区补全
- 测试反馈迭代

### 工程设计思维
- 需求分析与拆解
- 技术选型
- 系统架构设计
- API 接口设计

## 阶段二：LLM API 与结构化交互

### 大模型基础
- Token / Context Window
- Temperature / Top-p / Top-k
- 模型系列选型（Claude / GPT / Gemini）
- 选型维度
- 多模态
- 成本与限速

### API 集成
- OpenAI / Anthropic API
- OpenRouter / LiteLLM
- Streaming 流式响应

### Prompt Engineering
- System / User Prompt
- Few-shot
- 任务分解与推理引导
- 提示安全（降低注入风险）

### 结构化输出与工具调用
- Structured Output
- Tool Calling
- JSON Mode
- Zod 验证 / 重试

### 基础 SDK
- Vercel AI SDK
- LangChain.js
- OpenAI / Anthropic SDK

## 阶段三：RAG 知识库应用

### Embedding 与向量检索
- Embedding 原理与选型
- 分块策略 Chunking
- 相似度计算
- Hybrid Search

### 向量数据库
- pgvector（默认推荐）
- Chroma（本地）
- Pinecone / Weaviate / Qdrant

### RAG 管道
- 数据摄入
- 清洗与索引更新
- Query Rewrite
- 检索与 Reranking
- 引用追溯
- 权限过滤（检索层）
- 版本与时效

### RAG 失败模式
- 拒答策略
- 答案忠实度识别
- 召回质量告警

### 框架 & 评测
- LlamaIndex.TS / LangChain RAG
- Recall@K / MRR / NDCG
- 忠实度 / 引用正确率
- 投毒 / 越权防护

## 阶段四：Tool Calling 与 Mini Agent Loop

### 基础理解（必懂）
- Agent 三要素
- Tool Use / Function Calling
- ReAct 循环
- 消息历史即上下文
- 循环终止条件

### 核心实现（应会）
- 工具三层架构
- JSON Schema 工具接口
- 核心工具 Read/Write/Edit/Bash
- 流式参数累积后执行
- 权限分级
- 人工确认 / Hooks
- 步骤与 Token 守护
- System Prompt 工程

### 进阶扩展（选修）
- 上下文压缩
- Sub-agent 隔离
- MCP Client 接入
- Skills 加载

### 对比成熟 Coding Agent
- Claude Code 架构解析
- Codex CLI 对比
- Pi（4 工具 / 提示极简）
- 框架做了哪些抽象

## 阶段五：Agent 应用工程

### Workflow vs Agent 边界

### 记忆管理
- 会话状态
- 工作流状态
- 用户记忆
- 语义记忆
- 产物记忆
- 记忆治理

### 安全与可靠性
- 停止条件 / 步骤上限
- 预算控制
- Human-in-the-Loop
- 最小权限
- 失败恢复

### MCP Server 开发
- Host / Client / Server
- Tools / Resources / Prompts
- STDIO / HTTP 传输
- OAuth 2.1 授权
- 输入验证与审计
- Shadow MCP 风险

### Agent Skills（进阶）
- 规范 agentskills.io
- 自定义 Skill
- 跨平台复用
- 与 MCP 协作

### Agent 框架
> TypeScript 主线，Python 不避 —— LangGraph（Python）等成熟方案直接取用

- Vercel AI SDK（TS 主线，前端全栈首选）
- Pi（极简底座 / OpenClaw 同款，纯 TS）
- OpenAI / Claude Agent SDK
- LangGraph（Python，⭐ 生产级复杂工作流首选；LangGraph.js 简单场景可用）
- CrewAI / AutoGen（Python，多 Agent 编排）

### 多 Agent 系统
- 角色与分工
- 工作流编排
- Subagent
- 适用边界

## 阶段六：AI 全栈产品化

### 前端 AI 化
- Vercel AI SDK（Chat / Generative UI）
- Streaming UI
- 工具调用状态展示
- 引用来源展示
- 审批 UI
- 断线恢复 / 取消
- 多模态输入
- 本地推理（WebGPU）

### 全栈框架与数据层
- 复用已有（Next / Nest / PG / Redis）
- 实时通信 WS / SSE
- 向量库
- 会话与记忆持久化
- 长任务 / 检查点状态
- 多模态文件 → 对象存储

### AI 安全（增量）
- LLM 输出 / 外部内容不可信
- 多租户 RAG 隔离
- 日志 / Trace 脱敏
- API Key 管理
- 传统 authN/authZ 复用

### 部署与运行时
- 长任务 ↔ Serverless 超时
- Durable Workflow / 队列
- 流式基础设施
- Edge AI / 本地推理
- 平台选型（Vercel / CF / Docker）
- 对象存储 / Webhook

## 阶段七：生产级运营

### 可观测性
- Trace / Span 模型
- 调用 / 执行 / 工具 / 检索追踪
- Token / 延迟 / 错误 / 成本
- 用户反馈
- LangSmith / Langfuse / Helicone
- OpenTelemetry GenAI

### 评估与测试
- 检索质量 Recall / MRR / NDCG
- 回答质量 忠实度
- Agent 质量 成功率 / 轨迹
- Schema / 安全违规率
- A/B 测试
- CI Eval

### 成本优化
- Prompt Caching
- 上下文裁剪
- 模型路由
- 批量推理
- 预算告警

### 可靠性
- 重试策略
- Fallback / 多模型
- 熔断 / 限流
- 幂等性
- 并发控制
- 灰度发布

## 工程贯穿线（贯穿全部阶段）

### 安全
- 不可信输入处理
- 数据 / 租户隔离
- 密钥与日志脱敏

### 评测
- 离线评测集
- CI Eval

### 可观测性
- Trace / Span
- Token / 成本

### 成本控制
- Prompt Caching
- 模型路由
