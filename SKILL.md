---
name: using-zendesk-mcp
description: Manages Zendesk tickets via MCP tools for searching, viewing, creating, updating tickets and comments. Use when working with Zendesk, support tickets, customer issues, or transfer lookups.
---

# Using Zendesk MCP

## Tools

### Search & Retrieve

**`Zendesk:search_tickets`** - Find tickets by criteria (text, status, priority, tags, custom fields, dates)
```
Zendesk:search_tickets(query="wire transfer", status="open", limit=10)
Zendesk:search_tickets(custom_field_id=23301179390491, custom_field_value="txn_abc123")
Zendesk:search_tickets(requester="customer@example.com", status="pending")
```

**`Zendesk:get_ticket`** - Fetch a single ticket by ID
```
Zendesk:get_ticket(ticket_id=12345)
```

**`Zendesk:get_tickets`** - List recent tickets with pagination
```
Zendesk:get_tickets(page=1, per_page=25, sort_by="updated_at", sort_order="desc")
```

**`Zendesk:get_ticket_comments`** - Get conversation history for a ticket
```
Zendesk:get_ticket_comments(ticket_id=12345)
```

### Create & Modify

**`Zendesk:create_ticket`** - Create a new ticket
```
Zendesk:create_ticket(subject="Issue title", description="Details", priority="high")
```

**`Zendesk:create_ticket_comment`** - Add a comment to a ticket
```
Zendesk:create_ticket_comment(ticket_id=12345, comment="Response text", public=true)
```

**`Zendesk:update_ticket`** - Update ticket fields (status, priority, assignee, etc.)
```
Zendesk:update_ticket(ticket_id=12345, status="pending", priority="high")
```

## Prompts

**`analyze-ticket`** - Analyzes a ticket and provides summary, status, timeline, and key interaction points.

**`draft-ticket-response`** - Drafts a professional response using ticket context and knowledge base.

## Resources

**`zendesk://knowledge-base`** - Help Center articles organized by section. Useful for drafting informed responses.

## Workflows

### Investigate a customer issue
1. `Zendesk:search_tickets` with requester email or transfer ID
2. `Zendesk:get_ticket` for full details
3. `Zendesk:get_ticket_comments` to see conversation history

### Respond to a ticket
1. `Zendesk:get_ticket` and `Zendesk:get_ticket_comments`
2. Read `zendesk://knowledge-base` if needed
3. Use `draft-ticket-response` prompt or draft manually
4. `Zendesk:create_ticket_comment` to post response

### Triage unassigned tickets
1. `Zendesk:search_tickets(status="new")` or `Zendesk:get_tickets`
2. `Zendesk:update_ticket` to set assignee, priority, or status

## Reference

### Custom Fields
- Transfer ID: `custom_field_id=23301179390491`

### Status Values
`new` | `open` | `pending` | `hold` | `solved` | `closed`

### Priority Values
`low` | `normal` | `high` | `urgent`
