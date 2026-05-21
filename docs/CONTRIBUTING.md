# Contributing

## Pick up an issue
See [known-issues.md](docs/known-issues.md). Open issues are tagged in GitHub Issues.

## Workflow
1. Fork repo + clone
2. Export your modified n8n workflow as JSON → replace `workflow/awfii-echo-loop.json`
3. Strip credentials before commit (n8n export does this by default, but verify)
4. Add a brief changelog entry in `CHANGELOG.md`
5. Open PR with: what changed, why, how tested

## Testing
- Send `hello`, `help`, `bye`, and a free-form question
- Verify Airtable rows created
- Verify memory persists across 3+ messages

## Style
- No real keys, base IDs, table IDs, or phone numbers in commits
- Node names in English, snake_case avoided in n8n (use spaces)
- One responsibility per node
