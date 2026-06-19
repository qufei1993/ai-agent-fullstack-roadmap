# AI Agent Full-Stack Development Roadmap

> A capability map for developers with Node.js / frontend backgrounds building expertise in AI Agent full-stack development. **TypeScript is the mainline, but not exclusive** — Python's ecosystem has deeper maturity in Agent engineering (e.g., LangGraph, CrewAI). Use the right tool for the job; don't sacrifice solution quality for language preference. This roadmap focuses on learning order, core concepts, engineering boundaries, and technology selection — it does not expand into hands-on project tutorials.

---

## How to Read This Roadmap

The 7 stages are designed to be followed **in order**, but you don't need to dive deep into everything. Use these three tags to prioritize:

- 🟢 **Core Path** — AI-assisted development, LLM API, structured output, RAG, Agent Loop, full-stack deployment
- 🔵 **Engineering Throughline** — Security · Evaluation · Observability · Cost — runs through every stage, not something you bolt on before launch
- 🟡 **Advanced Elective** — MCP development, Skills, sub-agents, multi-agent systems, local inference, minimal agent runtimes like Pi

---

## Stage 1: AI-Assisted Development Workflow

### AI Coding Tools

- Cursor — AI-native editor
- Claude Code — terminal AI coding assistant
- Codex — OpenAI terminal AI coding assistant
- GitHub Copilot — code completion
- Windsurf / Trae

> The core of AI-assisted development isn't switching editors — it's building a collaborative workflow of Spec → Context → Execution → Review → Testing → Iteration.

### AI Programming Methodologies

- Spec-Driven Development — write the spec first, then let AI implement
- Context Engineering — design the context to precisely guide AI
- Vibe Coding — AI writes code, humans do review & decision-making (requires disciplined code review & verification, not reckless generation)
- Harness Engineering — build repeatable, evaluable execution frameworks for AI tasks
- Loop Engineering — evolve from manual prompting to designing autonomous loops: let AI continuously iterate through "execute → observe → correct", driven by feedback signals like tests and builds, while humans set verifiable goals, termination conditions, and guardrails (e.g., the Ralph technique)
- Human-AI collaboration principles & division of labor

### Project Rules & Memory Configuration

- **AGENTS.md** — open format for sharing project instructions across multiple Agent coding tools (maintained by Agentic AI Foundation / Linux Foundation), supported by Codex and other tools, with more tools adopting or compatible
- **CLAUDE.md** — Claude Code specific, supports directory-level overrides
- **.cursor/rules/\*.mdc** — Cursor multi-file rules with file-type scoping
- **.github/copilot-instructions.md** — GitHub Copilot project instructions
- **.windsurfrules** — Windsurf configuration
- Rule contents: code standards / tech stack conventions / commit conventions / security boundaries / deployment steps

### MCP & Skills Usage (within AI Coding Tools)

- Configure MCP Servers in Cursor / Claude Code / Windsurf
- Common community MCP Servers (file system / database / search / SaaS tools)
- Load and use Skills within AI coding tools
- MCP Server selection & security assessment

### AI-Assisted Debugging

- Have AI interpret error messages & stack traces
- Root Cause Analysis & localization
- Context-aware questioning with execution logs
- AI-assisted performance & memory issue diagnosis

### AI-Assisted Test Generation

- TDD with AI: write specs, let AI generate tests, then drive implementation
- Generate test cases from requirements documents
- AI fills test coverage blind spots
- Test results as AI iteration feedback

### Engineering Design Thinking

- Requirements analysis & use case decomposition
- Technology selection
- System architecture design
- API interface design

---

## Stage 2: LLM API & Structured Interaction

### LLM Fundamentals

- Token / Context Window mechanics
- Temperature / Top-p / Top-k
- Model family selection: Anthropic Claude series / OpenAI GPT series / Google Gemini series
- Model selection dimensions: reasoning capability, latency, cost, context length, multimodality, tool-calling support
- Multimodal (text / image / audio)
- Cost & rate-limit management

### API Integration

- OpenAI API / Anthropic API
- Unified interfaces (OpenRouter / LiteLLM)
- Streaming responses

### Prompt Engineering

- System Prompt vs User Prompt
- Few-shot Learning
- Task decomposition & reasoning guidance (reasoning models typically handle this internally; non-reasoning models rely more on explicit guidance)
- Prompt safety & untrusted input handling (mitigate Prompt Injection / Jailbreak risks)

### Structured Output & Tool Calling

- Structured Output — constrain model output format to JSON Schema
- Tool Calling — let models request external actions
- JSON Mode — guarantees valid JSON, not business-correct semantics; still requires application-level validation
- JSON Schema definition / Zod validation / invalid output repair & retry

### Core SDKs

- Vercel AI SDK
- LangChain.js / LangChain (Python)
- OpenAI SDK / Anthropic SDK

---

> **Engineering Throughline Principle:** Security, evaluation, observability, and cost control are not capabilities you bolt on before launch. From your very first LLM API call, log inputs/outputs, traces, errors, latency, token usage, cost, and failure cases.

---

## Stage 3: RAG Knowledge Base Applications

### Embeddings & Vector Retrieval

- Embedding fundamentals & model selection
- Text chunking strategies — chunks too large cause context redundancy, too small lose semantics
- Similarity computation (cosine similarity / dot product)
- Hybrid Search (vector + full-text)

### Vector Databases

- PostgreSQL + pgvector (default recommendation, supports full-text search alongside vectors)
- Chroma (local development)
- Pinecone / Weaviate / Qdrant (scale-oriented scenarios)

### RAG Pipeline

- Data ingestion (PDF / web / database / API)
- Document cleaning & preprocessing / index building & incremental updates
- Query Rewrite / query decomposition
- Retrieval & Reranking
- Context assembly & citation tracing
- Permission filtering (Metadata Filter / tenant isolation) — must be enforced at the retrieval layer, not via Prompt alone
- Document versioning & freshness management

### RAG Failure Mode Handling

- How to refuse answering when nothing relevant is retrieved
- How to detect when retrieved documents produce unfaithful answers
- Recall quality degradation detection & alerting

### RAG Frameworks & Evaluation

- LlamaIndex.TS / LlamaIndex (Python) / LangChain RAG
- Evaluation metrics: Recall@K / Precision@K / MRR / NDCG / citation accuracy / answer faithfulness
- RAG data poisoning prevention / cross-tenant information leakage prevention

---

## Stage 4: Tool Calling & Mini Agent Loop

> At its core, an agent is a while loop + Function Calling. The real complexity lies in context management, tool execution, error handling, and permission control. Build one from scratch without frameworks to understand the underlying mechanisms.

**The Mini Coding Agent has three learning tiers:**

### Foundational Understanding (Must Know)

- Agent's three elements: Brain (LLM) + Tools + Agent Loop
- Tool Use / Function Calling
- ReAct loop: Reason → Act → Observe → Loop
- Message history as conversation context (simplified starting point for Mini Agents; production agents need additional execution state, checkpoints & idempotency keys)
- Loop termination condition: agent stops when LLM ceases tool calls

### Core Implementation (Should Be Able to Build)

- Three-layer tool architecture: Registry → Dispatcher → Implementation
- JSON Schema for tool interface definitions (language-agnostic)
- Core toolset: Read / Write / Edit / Bash / Glob / Grep
- Streaming response handling: detect tool calls mid-stream, **accumulate complete parameters** before execution
- Tool output truncation strategies / errors returned as feedback
- Permission tiers: Read-only → Workspace write → Dangerous full access
- High-risk operation human confirmation / Middleware Hooks
- Step limits & Token budget guardians
- System Prompt engineering (behavioral norms / tool usage principles / read-before-write)

### Advanced Extensions (Elective)

- Context Compaction: HeadTail pruning / LLM summarization replacement (must preserve complete tool-call/result pairs; production systems should compact by semantic turns)
- Sub-agent context isolation
- MCP Client integration (connect to and invoke existing MCP Servers)
- Skills loading & on-demand execution

### Comparative Study with Production Coding Agents

- Claude Code full architecture analysis (Agent Loop / tool system / permission model / MCP / Skills)
- Codex CLI design comparison
- Pi (earendil-works/pi) — minimal implementation: only 4 core tools, system prompt <1000 tokens
- What frameworks (LangGraph / Vercel AI SDK) abstract away

---

## Stage 5: Agent Application Engineering

> **Workflow vs Agent boundary:** If a problem can be solved with a deterministic Workflow, don't design it as an Agent. Agents are better suited for open-ended goals, uncertain paths, and tasks requiring dynamic tool selection with environment feedback. Workflows are predefined paths; Agents let the model dynamically decide process and tool choices.

### Memory Management

- Session state (message history, tool calls, execution results)
- Workflow state (task steps, checkpoints, approval status)
- User memory (preferences, long-term profile)
- Semantic memory (retrievable knowledge, not limited to vector stores)
- Artifact memory (files, reports, code, execution records)
- Memory governance (expiry, deletion, privacy isolation)

### Agent Security & Reliability

- Termination conditions & step limits
- Token / time / cost budget controls
- Human-in-the-Loop — beyond safety approval: also includes supplementary information, correction, recovery, and branch decisions
- Least privilege & tool allowlists
- Error handling & failure recovery

### MCP (Model Context Protocol) — Building Custom MCP Servers

- Host / Client / Server responsibility boundaries
- Tools / Resources / Prompts distinction
- STDIO & Streamable HTTP transport layers
- Lifecycle & capability negotiation
- OAuth 2.1 authorization / Scope minimization / Token audience validation
- Tool input validation & call auditing
- Malicious Shadow MCP Server risks

### Agent Skills — Advanced Capability

- Skills principles & specification (agentskills.io)
- Custom Skill development
- Cross-platform Skill reuse (Claude Code / other Agent platforms)
- Skills & MCP collaboration patterns

### Agent Frameworks

> **Principle: TypeScript mainline, Python without prejudice.** This roadmap defaults to Node.js/TS, but the Python ecosystem has deeper maturity in Agent engineering — for complex workflows and long-running task orchestration, LangGraph (Python) is more production-hardened than LangGraph.js. Don't sacrifice solution quality for language preference.

| Tier | Recommendation | Notes |
|------|---------------|-------|
| TypeScript Mainline | Vercel AI SDK ToolLoopAgent | Top pick for full-stack frontend, seamless with Next.js / Streaming UI |
| Minimal Composable Base | Pi (pi-agent-core, same engine as OpenClaw, pure TS) | Minimal source code, ideal for understanding Agent internals before customizing |
| Vendor SDKs | OpenAI Agents SDK / Claude Agent SDK | Native integration, fast start |
| Complex Stateful Workflows | **LangGraph (Python)** ⭐ | Stateful DAG + checkpoints + Human-in-the-Loop, most battle-tested; LangGraph.js catching up, usable for simple scenarios |
| Multi-Agent Orchestration | CrewAI / AutoGen AG2 (Python) | Role-based division + workflow orchestration, best for rapid prototyping |

### Multi-Agent Systems

- Role & task distribution
- Workflow orchestration
- Sub-agents (Subagent)
- Applicability boundaries of multi-agent systems

---

## Stage 6: AI Full-Stack Productionization

### Frontend AI

- Vercel AI SDK (Chat / Generative UI / Object Generation / Tool Calling)
- Streaming UI / tool call status display / citation & source display
- User confirmation & approval UI / connection recovery & cancellation
- File & multimodal input
- Local inference (WebGPU / Transformers.js)

### Full-Stack Framework & Data Layer

- Reuse existing capabilities: Next.js / Nest / Hono, Route Handlers (BFF), PostgreSQL, Redis, containerization (already in place, not expanded)
- Real-time communication: WebSocket / SSE (carrying streaming responses)
- AI-specific data requirements: vector databases (semantic search), session & memory persistence, long-task / checkpoint state, multimodal files → object storage

### AI Security (Incremental, on Top of Existing Web Security)

- Treat LLM output & external content as untrusted data — full-stack Prompt Injection defense
- Multi-tenant RAG data isolation — enforced at the retrieval layer, not via Prompt alone
- LLM log & trace sanitization (PII / secrets must not enter logs)
- LLM API Key & secret management
- Traditional authN/authZ (OAuth/OIDC, RBAC/ABAC) reused — not expanded here

### Deployment & Runtime (AI-Specific Challenges)

- Long-running agent tasks ↔ Serverless timeouts → Durable Workflow / background task queues
- Streaming response infrastructure — SSE long connections, connection recovery, request cancellation
- Edge AI (Cloudflare Workers) / local inference deployment
- Platform selection: Vercel / Cloudflare / Railway / Render / Docker (reuse what you know; choose as needed)
- Object storage / Webhooks

---

## Stage 7: Production Operations

### Observability

**Establish General Concepts First**

- Trace / Span model
- Model call / Agent execution / tool call / retrieval process tracing
- Token usage / latency / error rate / per-task cost
- User feedback collection

**Then Choose Tooling Platforms**

- LangSmith (LangChain ecosystem)
- Langfuse (open-source, framework-agnostic)
- Helicone (lightweight proxy layer)
- OpenTelemetry GenAI semantic conventions (still in Development status)

### Evaluation & Testing

- Retrieval quality: Recall@K / Precision@K / MRR / NDCG
- Answer quality: semantic similarity / citation & factual accuracy / answer faithfulness
- Agent quality: task success rate / tool call accuracy / execution trajectory analysis
- Schema compliance rate / security violation rate
- A/B testing
- CI Eval (evaluation suites integrated into continuous integration)

### Cost Optimization

- Prompt Caching
- Token compression (context pruning)
- Model routing (tiered small/large model dispatch)
- Batch inference
- Cost monitoring & budget alerts

### Reliability

- Rate limiting & retry strategies
- Graceful degradation (Fallback) & multi-model backups
- Traffic control & circuit breaking
- Idempotency design
- Concurrency control
- Canary releases
