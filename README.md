# AWFII WhatsApp Financial Literacy Chatbot

n8n workflow for a WhatsApp chatbot delivering financial literacy guidance to South African users via Twilio, Airtable, and Groq AI.

## Stack
- **n8n Cloud** v2.20.7
- **Twilio WhatsApp Sandbox** — messaging layer
- **Airtable** — user state, conversation history, FAQs
- **Groq** (`llama-3.3-70b-versatile`) — LLM responses
- **LangChain AI Agent** (n8n native) — orchestration + memory

## Architecture

```
Twilio Trigger → Edit Fields → Search User_States → Switch (keyword)
                                                    ├─ HELLO → Twilio Send
                                                    ├─ HELP  → Twilio Send
                                                    ├─ BYE   → Twilio Send
                                                    └─ Fallback → AI Agent → Log to Airtable → Twilio Send
                                                                  │
                                                                  ├─ Groq Chat Model
                                                                  └─ Simple Memory (keyed by phone)
```

## Status: Working

| Component | Status |
|---|---|
| Inbound WhatsApp via Twilio | ✅ |
| Keyword routing | ✅ |
| AI fallback with per-user memory | ✅ |
| Conversation logging (assistant role) | ✅ |
| Outbound replies | ✅ |

## Gaps (Help Wanted)

- New-user detection + `User_States` record creation
- Onboarding flow: START → CONSENT_PENDING → NAME_PENDING → REGISTERED
- User-role message logging (currently only assistant role)
- `Last_Interaction` updates
- FAQ retrieval as AI tool
- Migration from Twilio Sandbox to Meta WhatsApp Cloud API

## Quickstart

1. Fork the n8n workflow JSON in `/workflow`
2. Set up credentials per `/docs/credentials.md`
3. Provision Airtable base per `/docs/airtable-schema.md`
4. Import workflow → activate
5. Send WhatsApp message to your Twilio sandbox number

## Docs

- [Setup Guide](docs/setup.md)
- [Airtable Schema](docs/airtable-schema.md)
- [Architecture Decisions](docs/architecture.md)
- [Known Issues](docs/known-issues.md)
- [Contributing](CONTRIBUTING.md)

## License
MIT
