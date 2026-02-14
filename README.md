# Resend CLI

CLI for Resend email API. Send emails, manage domains, API keys, audiences, contacts, webhooks, templates, broadcasts, and segments.

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
./scripts/resend.js contacts <audience_id> list

# Get contact
./scripts/resend.js contacts <audience_id> get <contact_id>

# Create contact
./scripts/resend.js contacts <audience_id> create --email "user@test.com" --first-name "John" --last-name "Doe"

# Update contact
./scripts/resend.js contacts <audience_id> update <contact_id> --unsubscribed true

# Delete contact
./scripts/resend.js contacts <audience_id> delete <contact_id>
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

### Templates

```bash
# List templates
./scripts/resend.js templates list
./scripts/resend.js templates list --limit 10 --after <cursor>

# Get template
./scripts/resend.js templates get <id_or_alias>

# Create template with variables
./scripts/resend.js templates create --name "welcome" --html "<p>Hello {{{NAME}}}</p>" --subject "Welcome!" --from "you@domain.com"
./scripts/resend.js templates create --name "order" --html "<p>{{{PRODUCT}}} - ${{{PRICE}}}</p>" --variables '[{"key":"PRODUCT","type":"string","fallback_value":"item"},{"key":"PRICE","type":"number","fallback_value":0}]'

# Update template
./scripts/resend.js templates update <id> --html "<p>Updated content</p>" --subject "New Subject"

# Publish template (required before sending)
./scripts/resend.js templates publish <id>

# Duplicate template
./scripts/resend.js templates duplicate <id>

# Delete template
./scripts/resend.js templates delete <id>
```

**Template Variables:**
- Use `{{{VAR_NAME}}}` syntax in HTML
- Variables JSON: `[{"key":"NAME","type":"string|number","fallback_value":"default"}]`
- Must publish template before it can be used in emails

### Broadcasts

```bash
# List broadcasts
./scripts/resend.js broadcasts list

# Get broadcast
./scripts/resend.js broadcasts get <id>

# Create broadcast
./scripts/resend.js broadcasts create --segment-id <id> --from "you@domain.com" --subject "Newsletter" --html "<p>Hi {{{FIRST_NAME|there}}}</p>"

# Send broadcast (immediately or scheduled)
./scripts/resend.js broadcasts send <id>
./scripts/resend.js broadcasts send <id> --scheduled-at "2025-01-15T10:00:00Z"

# Delete broadcast (draft only)
./scripts/resend.js broadcasts delete <id>
```

### Segments (formerly Audiences)

```bash
# List segments
./scripts/resend.js segments list

# Get segment
./scripts/resend.js segments get <id>

# Create segment
./scripts/resend.js segments create --name "Newsletter Subscribers"

# Delete segment
./scripts/resend.js segments delete <id>
```

## Output

All commands output JSON for easy parsing:

```bash
./scripts/resend.js domains list | jq '.data[].name'
./scripts/resend.js templates list | jq '.data[] | {name, status}'
```
