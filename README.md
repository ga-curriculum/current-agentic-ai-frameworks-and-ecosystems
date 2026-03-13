# Current Agentic AI Frameworks and Ecosystems
**Session Time:** 120 minutes  
**Format:** Instructor-Led  

---

## Prerequisites

- Completion of Sessions 1–3  
- Understanding of the core agent components: reasoning engine, memory, tools, and feedback loops  
- Familiarity with the perceive–act loop and the LLM's roles as reasoner, planner, and orchestrator  

---

## Learning Objectives

By the end of this session, students will be able to:

1. **Compare** the features and capabilities of major no-code and low-code platforms for building AI agents.
2. **Identify** the strengths and limitations of different frameworks based on project needs and team context.
3. **Select** the most suitable framework for specific project requirements, considering extensibility, ecosystem maturity, operational complexity, and risk of vendor lock-in.

> The goal of this session is not to master any single platform — it is to develop a decision-making framework that applies to any tool you will encounter, including ones that don't exist yet.

---

## Session Breakdown

| # | Segment | Duration |
|---|---------|----------|
| 1 | Mapping the Ecosystem | 20 min |
| 2 | Strengths, Limitations, and What They Don't Tell You | 10 min |
| 3 | A Framework for Selecting the Right Tool | 15 min |
| 4 | Break | 10 min |
| 5 | Lab | 60 min |
| 6 | Wrap-Up & Reflection | 5 min |
|   | **Total** | **120 min** |

---

## 1. Mapping the Ecosystem (20 min)

### The Landscape Problem

The agentic AI tooling ecosystem is large, fast-moving, and poorly categorized. New platforms launch frequently, existing ones pivot their positioning, and marketing language ("autonomous," "intelligent," "orchestrated") is applied inconsistently. Before comparing specific tools, we need a stable taxonomy.

### A Taxonomy for Agent Platforms

Every agent-building platform sits somewhere on two axes:

**Axis 1: Abstraction level**
- **No-code:** Visual builders, drag-and-drop flows, minimal or no programming required
- **Low-code:** Configuration-heavy, some scripting, mostly pre-built components
- **Code-first:** Full programmatic control, framework libraries, requires engineering

**Axis 2: Scope of control**
- **Opinionated:** The platform makes architectural decisions for you (memory model, orchestration pattern, deployment target)
- **Flexible:** The platform provides primitives and lets you compose them freely

Neither axis is better or worse in isolation — the right position depends on your project, your team, and your constraints. The mistake most teams make is selecting a tool based on familiarity or hype rather than fit.

### Visual Map of the Ecosystem

<img width="592" height="451" alt="image" src="https://git.generalassemb.ly/user-attachments/assets/c124539f-881f-4192-be4e-1cdd645cbaf9" />


This map positions the major platforms across the two axes:
- Vertical: Opinionated → Flexible
- Horizontal: No-code → Code-first

Notice how platforms cluster based on trade-offs between control and accessibility.

### Platform-by-Platform Overview

The following platforms represent the major categories of the current ecosystem. Each overview covers: what it is, who it is designed for, its core philosophy, and how it implements the agent components covered in Session 2.

---

#### GPT Builder (OpenAI)

**Category:** No-code  
**Target user:** Non-technical professionals, product teams, rapid prototypers  
**Core philosophy:** The fastest path from idea to deployed agent, within the OpenAI ecosystem

GPT Builder is OpenAI's interface for creating custom GPTs — agents with a defined persona, knowledge base, and a limited set of tool integrations. Configuration happens entirely through a conversational setup interface and a structured form.

| Component | Implementation |
|---|---|
| Reasoning Engine | GPT-4o (fixed, not swappable) |
| Memory | Uploaded files as knowledge base; no persistent cross-session memory by default |
| Tools | Web search, DALL·E, code interpreter, custom Actions (OpenAPI schema) |
| Orchestration | Single-agent only; no multi-agent coordination |
| Deployment | Hosted on ChatGPT; shareable via link |

**What it does well:** Immediate deployment, zero infrastructure, accessible to non-engineers, good for internal knowledge assistants and simple workflows.

**What it does not do:** Complex multi-step reasoning, persistent user memory, multi-agent coordination, custom memory backends, or deployment outside the ChatGPT ecosystem.

---

#### Relevance AI

**Category:** No-code / Low-code  
**Target user:** Business teams, operations professionals, non-technical builders who need more power than GPT Builder  
**Core philosophy:** Enterprise-grade agent workflows without requiring engineering resources

Relevance AI provides a visual workflow builder where each agent step is a configurable node — LLM calls, tool integrations, conditional logic, and data transformations can all be composed visually. It also supports Python code blocks for custom logic when needed.

| Component | Implementation |
|---|---|
| Reasoning Engine | Configurable (GPT-4, Claude, Gemini, and others) |
| Memory | Built-in knowledge tables (vector storage); integration with external databases |
| Tools | Pre-built integrations (Google Sheets, Slack, Salesforce, etc.) + custom API connections |
| Orchestration | Sequential and parallel workflows; basic multi-agent handoffs |
| Deployment | Cloud-hosted; embeddable via widget or API |

**What it does well:** Rapid deployment of business workflows, strong integration library, accessible to operations teams, good observability dashboard.

**What it does not do:** Deep customization of the orchestration layer, complex conditional reasoning chains, or fine-grained control over memory retrieval strategies.

---

#### Flowise

**Category:** Low-code (self-hostable)  
**Target user:** Technical teams who want visual composition with full infrastructure control  
**Core philosophy:** The power of LangChain, accessible through a visual interface, on your own infrastructure

Flowise is an open-source, self-hostable platform that exposes LangChain and LlamaIndex components as drag-and-drop nodes in a visual canvas. It gives builders access to the full LangChain ecosystem — chains, agents, memory types, vector stores, and tool integrations — without requiring direct Python development.

| Component | Implementation |
|---|---|
| Reasoning Engine | Any LangChain-supported model (OpenAI, Anthropic, HuggingFace, Ollama, etc.) |
| Memory | Buffer memory, summary memory, vector store memory, entity memory — all configurable |
| Tools | Full LangChain tool library + custom tool definitions |
| Orchestration | Single-agent and multi-agent flows; supports ReAct, OpenAI Functions, and custom chains |
| Deployment | Self-hosted (Docker); API endpoint exposed for integration |

**What it does well:** Full LangChain access without writing Python, self-hosting for data privacy, flexible memory configuration, strong community and documentation.

**What it does not do:** Managed infrastructure, enterprise SLA, or visual deployment pipelines — operations overhead is higher than hosted platforms.

---

#### n8n

**Category:** Low-code  
**Target user:** Technical teams building automated workflows with AI embedded as a step  
**Core philosophy:** Workflow automation first, AI as a powerful node in a broader process

n8n is a workflow automation platform — similar to Zapier or Make — but with native support for LLM nodes, AI agents, and vector store integrations. Unlike agent-first platforms, n8n treats the AI agent as one component in a larger automation workflow, which makes it particularly strong for integrating agents into existing business processes.

| Component | Implementation |
|---|---|
| Reasoning Engine | OpenAI, Anthropic, and others via configurable nodes |
| Memory | In-memory buffer; Postgres or Pinecone for persistent memory |
| Tools | 400+ pre-built integrations; custom HTTP request nodes |
| Orchestration | Sequential and conditional workflow logic; AI Agent node with tool use |
| Deployment | Cloud or self-hosted; webhook and scheduler triggers |

**What it does well:** Deep integration with existing business systems, trigger-based automation, strong conditional logic, excellent for hybrid human+agent workflows.

**What it does not do:** Complex multi-agent coordination, autonomous goal-directed behavior, or long-horizon planning — the workflow structure is defined by the builder, not the agent.

---

#### CrewAI

**Category:** Code-first (Python framework)  
**Target user:** Developers and ML engineers building multi-agent systems  
**Core philosophy:** Teams of specialized agents, coordinated by roles, goals, and structured delegation

CrewAI is a Python framework designed specifically for **multi-agent orchestration**. Instead of building a single agent that does everything, CrewAI encourages the creation of a "crew" — a team of agents with defined roles, each responsible for a specific part of a complex task, coordinated by a structured delegation system.

| Component | Implementation |
|---|---|
| Reasoning Engine | OpenAI, Anthropic, and others via LangChain integration |
| Memory | Short-term (in-context), long-term (SQLite by default), entity memory, shared crew memory |
| Tools | LangChain tools + custom Python functions |
| Orchestration | Sequential, hierarchical, and consensus-based crew coordination |
| Deployment | Python package; integrates with FastAPI, Docker, and cloud runners |

**What it does well:** Multi-agent coordination patterns, role-based task delegation, shared memory between agents, structured output enforcement.

**What it does not do:** Visual configuration, rapid non-technical prototyping, or managed cloud deployment — requires Python development and DevOps capability.

---

#### LangGraph

**Category:** Code-first (Python framework)  
**Target user:** Engineers building production agents that require precise control over reasoning flows  
**Core philosophy:** Agents as stateful graphs — explicit control over every node, edge, and state transition

LangGraph is LangChain's framework for building agents as **directed graphs**, where each node is a processing step (LLM call, tool call, conditional branch) and each edge is a transition between steps. This graph-based model gives engineers complete control over the agent's execution flow — including cycles, branching, human-in-the-loop interrupts, and state checkpointing.

| Component | Implementation |
|---|---|
| Reasoning Engine | Any LangChain-supported model |
| Memory | State object passed through the graph; persistent checkpointing via LangGraph Cloud |
| Tools | Full LangChain tool library + custom nodes |
| Orchestration | Graph-based; supports cycles, parallel branches, conditional edges, and interrupt nodes |
| Deployment | LangGraph Cloud (managed) or self-hosted; native LangSmith observability |

**What it does well:** Precise control over execution flow, production-grade state management, native observability, support for complex conditional and cyclic agent behaviors, human-in-the-loop patterns.

**What it does not do:** Rapid prototyping, visual configuration, or accessibility for non-engineers — the learning curve is steeper than any other platform covered here.

---

#### Dust

**Category:** Low-code  
**Target user:** Enterprise teams building internal AI assistants and knowledge agents  
**Core philosophy:** Connecting agents to company knowledge and workflows, with enterprise governance built in

Dust is an enterprise-focused platform for deploying AI assistants ("agents") connected to a company's internal data sources — Notion, Slack, Google Drive, GitHub, Salesforce, and more. Its primary strength is structured data access and team-level governance: permissions, access controls, and audit logs are first-class features.

| Component | Implementation |
|---|---|
| Reasoning Engine | GPT-4, Claude, Gemini — configurable per agent |
| Memory | Connected data sources as retrieval context; conversation history |
| Tools | Native connectors to 20+ enterprise data sources |
| Orchestration | Single-agent and multi-agent with defined handoffs |
| Deployment | Cloud-hosted; Slack and web interface |

**What it does well:** Enterprise data connectivity, team permissions and governance, compliance-friendly deployment, fast time-to-value for knowledge agents.

**What it does not do:** Custom tool development, complex workflow automation, or fine-grained orchestration control — it is optimized for knowledge retrieval and assistants, not process automation.

---

### Ecosystem Summary

<img width="637" height="466" alt="image" src="https://git.generalassemb.ly/user-attachments/assets/9eb01621-622f-4cea-b424-356b77061848" />

---

## 2. Strengths, Limitations, and What They Don't Tell You (10 min)

### What Platform Documentation Won't Say

Every platform's documentation emphasizes its strengths and buries its limitations. Before selecting a tool for a real project, there are four categories of honest questions to ask:

#### 1. Vendor Lock-In Risk

How much of your agent's behavior is tied to this specific platform?

- **High lock-in:** GPT Builder (OpenAI ecosystem only), Dust (proprietary connectors)
- **Medium lock-in:** Relevance AI (proprietary workflows, but exportable logic)
- **Low lock-in:** Flowise, n8n (open-source, self-hostable), CrewAI, LangGraph (pure Python)

Lock-in is not inherently bad — sometimes the tradeoff of speed and simplicity is worth it. But it should be a conscious decision, not an oversight.

#### 2. Observability and Debuggability

When your agent fails in production, how easily can you find out why?

- Platforms with strong native observability: LangGraph (LangSmith), n8n (execution logs), Relevance AI (run history)
- Platforms where you need to add your own: GPT Builder (minimal logs), CrewAI (requires external tooling)

An agent you cannot observe is an agent you cannot improve.

#### 3. Scalability Ceiling

What happens when the number of users, requests, or data sources grows by 10x?

- Managed platforms (GPT Builder, Relevance AI, Dust) handle scaling automatically — but at a cost, and within their infrastructure limits
- Self-hosted platforms (Flowise, n8n) give you control but require operational investment
- Code-first frameworks (CrewAI, LangGraph) scale as well as your infrastructure allows

#### 4. Community and Ecosystem Maturity

How much help exists when you get stuck?

<img width="716" height="421" alt="image" src="https://git.generalassemb.ly/user-attachments/assets/ee7929e0-b3dd-4873-a9c6-fddfdb951e76" />

---

## 3. A Framework for Selecting the Right Tool (15 min)

### The Selection Decision Is Not About Features — It's About Fit

A common mistake is building a feature comparison matrix and selecting the platform with the most checkmarks. This approach fails because it ignores the constraints that actually determine success: team capability, timeline, data sensitivity, and long-term maintenance.

### The Five-Dimension Selection Framework

Use the following five dimensions to evaluate any agent-building platform against a specific project:

#### Dimension 1: Team Capability

What is the technical baseline of the people who will build and maintain this agent?

<img width="698" height="384" alt="image" src="https://git.generalassemb.ly/user-attachments/assets/20788951-053b-4947-bb23-cd4cb38cf13c" />

Choosing a code-first framework for a non-engineering team does not produce a more capable agent — it produces an abandoned project.

#### Dimension 2: Task Complexity

How many steps, tools, and decision branches does the agent require?

| Task Profile | Recommended Approach |
|---|---|
| Single-turn Q&A or summarization | GPT Builder, Dust |
| Multi-step workflow with defined steps | n8n, Relevance AI |
| Adaptive reasoning, dynamic tool selection | Flowise, CrewAI |
| Complex conditional flows, cyclic reasoning | LangGraph |
| Multiple specialized agents collaborating | CrewAI, LangGraph |

#### Dimension 3: Data Sensitivity

Where does the data live, and who is allowed to see it?

| Data Context | Recommended Approach |
|---|---|
| Public or low-sensitivity data | Any hosted platform |
| Internal business data, standard compliance | Relevance AI, Dust (with enterprise controls) |
| Regulated industries (healthcare, finance) | Self-hosted (Flowise, n8n) or LangGraph with private deployment |
| Maximum data control required | Code-first frameworks on private infrastructure |

#### Dimension 4: Time-to-Value

How quickly does a working prototype need to exist?

| Timeline | Recommended Approach |
|---|---|
| Hours to days | GPT Builder, Relevance AI |
| Days to weeks | Flowise, n8n, Dust |
| Weeks to months | CrewAI, LangGraph |

Code-first frameworks deliver more control, but they require significantly more upfront engineering investment.

#### Dimension 5: Long-Term Extensibility

How likely is this agent to grow in complexity, integrate new tools, or be maintained by a larger team over time?

| Extensibility Need | Recommended Approach |
|---|---|
| Low (static use case, limited scope) | Any no-code platform |
| Medium (new integrations over time) | n8n, Flowise, Relevance AI |
| High (evolving architecture, team ownership) | CrewAI, LangGraph |

### Applying the Framework: Two Scenarios

**Scenario A: A marketing operations team at a mid-size company wants to automate lead qualification from inbound emails.**

- Team capability: Non-technical operations team
- Task complexity: Multi-step but well-defined (read email → check CRM → score lead → route)
- Data sensitivity: Internal CRM data, standard privacy requirements
- Time-to-value: 2 weeks
- Extensibility: Medium (may add channels later)

**Recommended:** n8n or Relevance AI. The workflow is structured enough for a visual builder, the integrations (email + CRM) are pre-built, and the timeline rules out code-first frameworks.

---

**Scenario B: A fintech startup wants to build an autonomous research agent that monitors regulatory filings, cross-references internal risk models, and generates compliance briefs.**

- Team capability: Engineering team with Python experience
- Task complexity: High — adaptive reasoning, dynamic tool use, multi-source data
- Data sensitivity: High — regulated financial data, must be self-hosted
- Time-to-value: 6–8 weeks acceptable
- Extensibility: High — will grow in scope and integrate with more data sources

**Recommended:** LangGraph with self-hosted infrastructure. The complexity and data requirements rule out hosted no-code platforms; the need for precise execution control and auditability makes LangGraph the strongest fit.

---

## 4. Break (10 min)

---

## 5. Lab (60 min)

- https://pages.git.generalassemb.ly/Build-AI-Agents/Use-Cases-Across-Industries/

---

## 6. Wrap-Up & Reflection (5 min)

### Key Takeaways
- There Is No “Best” Framework — Only Best Fit
- Control, Speed, and Risk Are Trade-Offs
- Framework Choice Determines Production Outcomes



> Next session: **Use Cases Across Industries** 
---

## Resources

- [CrewAI Documentation](https://docs.crewai.com/)
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [Flowise Documentation](https://docs.flowiseai.com/)
- [n8n Documentation](https://docs.n8n.io/)
- [Relevance AI Documentation](https://relevanceai.com/docs)
- [Dust Documentation](https://docs.dust.tt/)
- [OpenAI GPT Builder Guide](https://platform.openai.com/docs/assistants/overview)
- Lilian Weng — *LLM-powered Autonomous Agents* (2023) — [lilianweng.github.io](https://lilianweng.github.io/posts/2023-06-23-agent/)
