# Known Issues / Help Wanted

## Open

### #1 Search records result is unused
The `Search records` node queries `User_States` but its output is not consumed by downstream nodes. Either remove it or wire it into an IF for new-user detection (preferred).

### #2 No new-user creation
First-time senders are not written to `User_States`. Onboarding cannot start.
**Fix:** Add IF after `Search records` → if `$json.id` empty → Airtable Create node (Phone_Number, Current_State: `START`).

### #3 Only assistant role is logged
`Conversation_History` only stores the AI reply. User messages are missing → no audit trail of inbound traffic.
**Fix:** Add second Airtable Create node before AI Agent logging the user message with Role: `user`.

### #4 No onboarding state machine
States exist in the Airtable schema (CONSENT_PENDING, NAME_PENDING, REGISTERED) but no workflow logic transitions between them.

### #5 `Last_Interaction` never updates
Schema has the field, no node writes to it.

### #6 Twilio Sandbox is not production-ready
Recipients must opt in via join code; sessions expire. Migration target: Meta WhatsApp Cloud API (built-in n8n node, free tier, business verification 1-5 days).

### #7 FAQs table unused
6 FAQ rows exist; AI Agent has no tool wired to retrieve them. Add an Airtable Tool to the agent node.

### #8 No rate-limit handling
Airtable free tier: 5 req/sec. Bursty conversations could hit limits with no retry.

## Closed

- ✅ Twilio credential mismatch causing 400 errors on outbound
- ✅ Empty message body errors from incorrect Twilio Trigger data path (`$json.data.body` vs `$json.Body`)
- ✅ Airtable Timestamp rejecting ISO string → resolved with `Typecast: ON` and `yyyy-MM-dd HH:mm:ss` format

