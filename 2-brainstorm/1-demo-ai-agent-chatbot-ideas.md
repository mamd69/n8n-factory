# Brainstorm — Advanced AI Agent Workflows with a Chatbot

> Saved from a brainstorm session. Step 2 of the Factory assembly line.

## Session prompt

> brainstorm to cool n8n workflows to build advanced ai agent with chatbot

## Claude's output

A tiered set of AI agent + chatbot workflow ideas, from starter builds to
advanced multi-agent systems.

### 🟢 Foundational (great first builds)

**1. RAG Knowledge-Base Chatbot**
- Telegram/Slack trigger → AI Agent → Vector Store (Pinecone/Qdrant/PGVector) as a tool
- Companion ingestion workflow: Google Drive/Notion → embeddings → vector store
- The agent answers only from *your* docs and cites sources.

**2. Customer Support Triage Bot**
- Webhook (web chat widget) → AI Agent with classification → routes to FAQ answer,
  ticket creation (Zendesk/Linear), or human handoff via Slack
- Sentiment detection escalates angry customers automatically.

**3. Personal Assistant Chatbot**
- Telegram → AI Agent with tools: Gmail, Google Calendar, Drive
- "Schedule a call with X next week" / "summarize unread emails" — all in chat.

### 🟡 Intermediate (multi-tool agents)

**4. Research Agent**
- Chat → Agent with web search (SerpAPI/Tavily), HTTP Request, scraping tools
- Returns synthesized briefs with citations; can drop results into Notion/Sheets.

**5. SQL / Analytics Chatbot**
- Natural language → Agent generates SQL → executes against Postgres → formats
  results as chat reply or chart.
- Add guardrails so it only runs read-only queries.

**6. Voice-Enabled Agent**
- WhatsApp/Telegram voice note → transcribe (Whisper) → AI Agent → text-to-speech reply
- Fully conversational, hands-free.

### 🔴 Advanced (multi-agent orchestration)

**7. Supervisor / Sub-Agent Architecture**
- A "router" agent delegates to specialist sub-workflows (each its own AI Agent):
  Sales agent, Tech-support agent, Billing agent — connected as tools via Execute Workflow.
- The most "advanced AI agent" pattern in n8n.

**8. Agent with Persistent Memory + Profile**
- Chatbot that remembers users across sessions: store conversation summaries in a
  database, load user profile on each message, inject as context.
- Add a nightly workflow that "consolidates" memory.

**9. Autonomous Task Agent (human-in-the-loop)**
- Agent plans multi-step tasks, pauses at a Slack approval gate before risky actions
  (sending emails, spending money), then resumes.

**10. Self-Improving Content Agent**
- Chat brief → research agent → writer agent → critic agent → revision loop →
  publish to CMS/social.

### Recommended path

Start with **#1 (RAG chatbot)** as the base, then layer toward **#7 (supervisor)** —
that progression teaches every core pattern.

## Decision — selected for build

| Choice | Selected |
|--------|----------|
| Workflow | RAG Knowledge Chatbot |
| Chat channel | Telegram |
| LLM provider | Google Gemini |
| Vector store | Simple / In-Memory Store |
| Document source | Google Drive folder |

➡️ Built in [`4-workflows/telegram-rag-chatbot.md`](../4-workflows/telegram-rag-chatbot.md)
