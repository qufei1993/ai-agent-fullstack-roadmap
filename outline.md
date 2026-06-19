# AI Agent Full-Stack Development Roadmap

## Stage 1: AI-Assisted Development Workflow

### AI Coding Tools
- Cursor
- Claude Code
- Codex
- GitHub Copilot
- Windsurf / Trae

### AI Programming Methodologies
- Spec-Driven Development
- Context Engineering
- Vibe Coding
- Harness Engineering
- Loop Engineering
- Human-AI Collaboration Principles

### Project Rules Configuration
- AGENTS.md (cross-tool standard)
- CLAUDE.md
- .cursor/rules
- copilot-instructions.md
- .windsurfrules

### MCP & Skills Usage
- Configure MCP Servers
- Community MCP Servers
- Load & use Skills
- Selection & security assessment

### AI-Assisted Debugging
- Error & stack trace interpretation
- Root cause analysis
- Log context questioning
- Performance & memory diagnosis

### AI-Assisted Test Generation
- TDD with AI
- Requirements → test cases
- Coverage gap filling
- Test feedback iteration

### Engineering Design Thinking
- Requirements analysis & decomposition
- Technology selection
- System architecture design
- API interface design

## Stage 2: LLM API & Structured Interaction

### LLM Fundamentals
- Token / Context Window
- Temperature / Top-p / Top-k
- Model selection (Claude / GPT / Gemini)
- Selection dimensions
- Multimodal
- Cost & rate limits

### API Integration
- OpenAI / Anthropic API
- OpenRouter / LiteLLM
- Streaming responses

### Prompt Engineering
- System / User Prompt
- Few-shot
- Task decomposition & reasoning guidance
- Prompt safety (injection mitigation)

### Structured Output & Tool Calling
- Structured Output
- Tool Calling
- JSON Mode
- Zod validation / retry

### Core SDKs
- Vercel AI SDK
- LangChain.js
- OpenAI / Anthropic SDK

## Stage 3: RAG Knowledge Base Applications

### Embeddings & Vector Retrieval
- Embedding principles & selection
- Chunking strategies
- Similarity computation
- Hybrid Search

### Vector Databases
- pgvector (default recommendation)
- Chroma (local)
- Pinecone / Weaviate / Qdrant

### RAG Pipeline
- Data ingestion
- Cleaning & index updates
- Query Rewrite
- Retrieval & Reranking
- Citation tracing
- Permission filtering (retrieval layer)
- Versioning & freshness

### RAG Failure Modes
- Refusal strategies
- Faithfulness detection
- Recall quality alerting

### Frameworks & Evaluation
- LlamaIndex.TS / LangChain RAG
- Recall@K / MRR / NDCG
- Faithfulness / citation accuracy
- Poisoning / cross-tenant leakage prevention

## Stage 4: Tool Calling & Mini Agent Loop

### Foundational (Must Know)
- Agent three elements
- Tool Use / Function Calling
- ReAct loop
- Message history as context
- Loop termination conditions

### Core Implementation (Should Build)
- Three-layer tool architecture
- JSON Schema tool interfaces
- Core tools: Read/Write/Edit/Bash
- Streaming parameter accumulation before execution
- Permission tiers
- Human confirmation / Hooks
- Step & Token guardians
- System Prompt engineering

### Advanced (Elective)
- Context compaction
- Sub-agent isolation
- MCP Client integration
- Skills loading

### Comparative Study
- Claude Code architecture
- Codex CLI comparison
- Pi (4 tools / minimal prompt)
- What frameworks abstract

## Stage 5: Agent Application Engineering

### Workflow vs Agent Boundary

### Memory Management
- Session state
- Workflow state
- User memory
- Semantic memory
- Artifact memory
- Memory governance

### Security & Reliability
- Stop conditions / step limits
- Budget controls
- Human-in-the-Loop
- Least privilege
- Failure recovery

### MCP Server Development
- Host / Client / Server
- Tools / Resources / Prompts
- STDIO / HTTP transport
- OAuth 2.1 authorization
- Input validation & audit
- Shadow MCP risks

### Agent Skills (Advanced)
- agentskills.io spec
- Custom Skill development
- Cross-platform reuse
- MCP collaboration

### Agent Frameworks
> TypeScript mainline, Python without prejudice — use mature Python solutions like LangGraph directly

- Vercel AI SDK (TS mainline, frontend full-stack first choice)
- Pi (minimal base / OpenClaw engine, pure TS)
- OpenAI / Claude Agent SDK
- LangGraph (Python, ⭐ production-grade complex workflows; LangGraph.js for simple scenarios)
- CrewAI / AutoGen (Python, multi-agent orchestration)

### Multi-Agent Systems
- Role & task distribution
- Workflow orchestration
- Subagent
- Applicability boundaries

## Stage 6: AI Full-Stack Productionization

### Frontend AI
- Vercel AI SDK (Chat / Generative UI)
- Streaming UI
- Tool call status display
- Citation & source display
- Approval UI
- Connection recovery / cancel
- Multimodal input
- Local inference (WebGPU)

### Full-Stack Framework & Data Layer
- Reuse existing (Next / Nest / PG / Redis)
- Real-time: WS / SSE
- Vector databases
- Session & memory persistence
- Long task / checkpoint state
- Multimodal files → object storage

### AI Security (Incremental)
- LLM output / external content as untrusted
- Multi-tenant RAG isolation
- Log / Trace sanitization
- API Key management
- Traditional authN/authZ reused

### Deployment & Runtime
- Long tasks ↔ Serverless timeouts
- Durable Workflow / queues
- Streaming infrastructure
- Edge AI / local inference
- Platform selection (Vercel / CF / Docker)
- Object storage / Webhooks

## Stage 7: Production Operations

### Observability
- Trace / Span model
- Call / execution / tool / retrieval tracing
- Token / latency / error / cost
- User feedback
- LangSmith / Langfuse / Helicone
- OpenTelemetry GenAI

### Evaluation & Testing
- Retrieval quality: Recall / MRR / NDCG
- Answer quality: faithfulness
- Agent quality: success rate / trajectory
- Schema / security violation rate
- A/B testing
- CI Eval

### Cost Optimization
- Prompt Caching
- Context pruning
- Model routing
- Batch inference
- Budget alerts

### Reliability
- Retry strategies
- Fallback / multi-model
- Circuit breaking / rate limiting
- Idempotency
- Concurrency control
- Canary releases

## Engineering Throughline (Across All Stages)

### Security
- Untrusted input handling
- Data / tenant isolation
- Secret & log sanitization

### Evaluation
- Offline eval suites
- CI Eval

### Observability
- Trace / Span
- Token / cost

### Cost Control
- Prompt Caching
- Model routing
