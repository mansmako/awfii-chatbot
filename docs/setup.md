# Setup Guide

## Prerequisites
- n8n Cloud account (or self-hosted >= 2.20)
- Twilio account with WhatsApp Sandbox enabled
- Airtable account + Personal Access Token
- Groq API key (free tier)

## 1. Credentials in n8n

Create the following credentials (Settings → Credentials):

| Credential | Type | Notes |
|---|---|---|
| Twilio | Twilio API | Account SID + Auth Token |
| Airtable | Airtable Personal Access Token | Scope: `data.records:read`, `data.records:write` |
| Groq | Groq API | Generate at console.groq.com |

Replace placeholders only — never commit real keys.

## 2. Airtable

Create base with tables per [airtable-schema.md](airtable-schema.md). Note the base ID and table IDs from the API docs panel — they're referenced in the workflow JSON and must match.

## 3. Twilio Webhook

In Twilio Console → WhatsApp Sandbox Settings:
- **When a message comes in:** paste the Twilio Trigger node webhook URL from n8n
- **Method:** POST

## 4. Import Workflow

- Workflows → Import from File → select `workflow/awfii-echo-loop.json`
- Re-bind each credential reference (n8n flags missing creds)
- Update base/table IDs in all Airtable nodes if your IDs differ
- Save → Activate

## 5. Test

Send `hello` from your WhatsApp test number → expect `Hi there! Welcome to AWFII 👋`.

Send `what is a TFSA?` → expect AI-generated response + new row in `Conversation_History`.

