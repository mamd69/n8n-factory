# Workflow — Telegram RAG Knowledge Chatbot

> Saved from a build session. Step 4 of the Factory assembly line.
> Brainstorm: [`2-brainstorm/ai-agent-chatbot-ideas.md`](../2-brainstorm/ai-agent-chatbot-ideas.md)

## Session prompt

Built from the brainstorm decision: a **RAG Knowledge Chatbot** on **Telegram**,
powered by **Google Gemini**, using a **Simple / In-Memory vector store**, with
documents ingested from a **Google Drive folder**.

> Design and build the RAG Knowledge Chatbot — Telegram channel, Google Gemini
> LLM, in-memory vector store, Google Drive as the document source.

## Claude's output

Two workflows were built, validated (0 errors), and deployed to the n8n instance
(`heroforge.app.n8n.cloud`) in an **inactive** state, awaiting credentials.

### 🤖 Telegram RAG Knowledge Chatbot — `bq40kFzrpQIzhkA0`

[Open in n8n](https://heroforge.app.n8n.cloud/workflow/bq40kFzrpQIzhkA0)

```
Telegram Trigger → AI Agent → Send Reply
                      ├── Google Gemini Chat Model (gemini-2.5-flash, temp 0.3)
                      ├── Simple Memory (per-chat history, 10 messages)
                      └── Knowledge Base Tool → Simple Vector Store → Gemini Embeddings
```

- The agent has a strict system message: **always search the knowledge base,
  never invent answers**, and cite the source document.
- Memory is keyed per Telegram chat ID — each user gets their own thread.

### 📥 Knowledge Ingestion (Google Drive → Vector Store) — `uJATaIuQqXEnO8OG`

[Open in n8n](https://heroforge.app.n8n.cloud/workflow/uJATaIuQqXEnO8OG)

```
Google Drive Trigger → Download File → Insert into Knowledge Base
                                          ├── Gemini Embeddings
                                          └── Default Data Loader → Recursive Text Splitter (1000/100)
```

- Watches a Drive folder; new files are auto-chunked, embedded, and indexed.

Both workflows share the in-memory vector store via memory key
**`company_knowledge`** — ingestion writes, the chatbot reads.

## How to use it — setup in the n8n UI

1. **Create 3 credentials:** Telegram API (bot token from @BotFather),
   Google Gemini (Google Gemini/PaLM API key), Google Drive OAuth2.
2. **Assign them** to the nodes — Telegram Trigger + Send Reply; both Gemini
   Chat/Embeddings nodes; Drive Trigger + Download File.
3. **Set the watched folder** in the Google Drive Trigger (`folderToWatch` is
   currently empty).
4. **Activate the ingestion workflow** and drop documents into the folder to
   seed the knowledge base.
5. **Activate the chatbot** and message your bot on Telegram.

## Caveats & next steps

- **In-memory store is volatile** — the knowledge base is wiped if the n8n
  instance restarts; re-run ingestion afterwards. For permanence, swap the two
  Simple Vector Store nodes for **Supabase pgvector** or **Pinecone**.
- The Drive Trigger fires on **new files only**. To also re-index edited files,
  add a second trigger with the `fileUpdated` event.
- Possible enhancements: persistent vector store, error handling on the Telegram
  nodes, and a "typing…" indicator while the agent thinks.
