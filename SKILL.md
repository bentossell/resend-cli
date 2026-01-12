# Resend CLI

CLI for Resend email API. Send emails, manage domains, API keys, audiences, contacts, and webhooks.

## Setup

```bash
export RESEND_API_KEY=re_xxxxxxxxx
```

## Commands

### Emails

```bash
# Send email
./scripts/resend.js send --from "you@domain.com" --to "them@email.com" --subject "Hello" --html "<p>Hi</p>"
./scripts/resend.js send --from "you@domain.com" --to "a@test.com,b@test.com" --subject "Hello" --text "Plain text"

# Send with cc/bcc/reply-to
./scripts/resend.js send --from "you@domain.com" --to "them@email.com" --cc "cc@test.com" --bcc "bcc@test.com" --reply-to "reply@test.com" --subject "Hello" --html "<p>Hi</p>"

# Schedule email (ISO 8601 format)
./scripts/resend.js send --from "you@domain.com" --to "them@email.com" --subject "Hello" --html "<p>Hi</p>" --scheduled-at "2025-01-15T10:00:00Z"

# List sent emails
./scripts/resend.js emails list
./scripts/resend.js emails list --limit 20

# Get email by ID
./scripts/resend.js emails get <id>

# Cancel scheduled email
./scripts/resend.js emails cancel <id>
```

### Domains

```bash
# List domains
./scripts/resend.js domains list

# Get domain
./scripts/resend.js domains get <id>

# Create domain
./scripts/resend.js domains create --name "example.com"

# Verify domain
./scripts/resend.js domains verify <id>

# Delete domain
./scripts/resend.js domains delete <id>
```

### API Keys

```bash
# List API keys
./scripts/resend.js api-keys list

# Create API key
./scripts/resend.js api-keys create --name "Production"

# Delete API key
./scripts/resend.js api-keys delete <id>
```

### Audiences

```bash
# List audiences
./scripts/resend.js audiences list

# Get audience
./scripts/resend.js audiences get <id>

# Create audience
./scripts/resend.js audiences create --name "Newsletter"

# Delete audience
./scripts/resend.js audiences delete <id>
```

### Contacts

```bash
# List contacts in audience
./scripts/resend.js contacts list <audience_id>

# Get contact
./scripts/resend.js contacts get <audience_id> <contact_id>

# Create contact
./scripts/resend.js contacts create <audience_id> --email "user@test.com" --first-name "John" --last-name "Doe"

# Update contact
./scripts/resend.js contacts update <audience_id> <contact_id> --unsubscribed true

# Delete contact
./scripts/resend.js contacts delete <audience_id> <contact_id>
```

### Webhooks

```bash
# List webhooks
./scripts/resend.js webhooks list

# Get webhook
./scripts/resend.js webhooks get <id>

# Create webhook
./scripts/resend.js webhooks create --endpoint "https://example.com/webhook" --events "email.sent,email.delivered"

# Delete webhook
./scripts/resend.js webhooks delete <id>
```

## Output

All commands output JSON for easy parsing:

```bash
./scripts/resend.js domains list | jq '.data[].name'
```
