# Architecture Decisions

## ADR-001: n8n over custom backend
Rapid iteration, visual debugging, native LangChain nodes, no infra to manage. Trade-off: vendor lock-in.

## ADR-002: Twilio Sandbox for MVP
Lowest setup friction. **Known limitation:** recipients must join sandbox manually; not viable for production. Migration to Meta WhatsApp Cloud API planned (see [known-issues.md](known-issues.md)).

## ADR-003: Groq over OpenAI/Anthropic
Free tier. `llama-3.3-70b-versatile` is sufficient for FL guidance under 300 chars. Swap is one node change.

## ADR-004: Switch node for keyword routing, AI Agent for fallback
Deterministic keywords (HELLO, HELP, BYE) bypass the LLM — saves tokens, guarantees consistent responses. AI Agent handles open-ended queries only.

## ADR-005: Simple Memory keyed by phone
Per-user conversation context with no DB writes. Trade-off: memory is in-process; lost on n8n restart. Persistent memory via Airtable `Conversation_History` planned.

## ADR-006: Airtable over Postgres
Non-technical stakeholders need to inspect/edit data. Airtable's grid view is the cheapest CRM. Trade-off: 5 req/sec rate limit, no transactions.

## Data Flow

1. Twilio webhook → n8n Trigger
2. `Edit Fields` normalizes `phone` and `message`
3. `Search records` looks up User_States (currently unused — see Known Issues)
4. `Switch` routes by lowercased keyword
5. Fallback path: AI Agent with Groq + Simple Memory
6. Assistant reply logged to `Conversation_History`
7. Twilio sends reply

