---
name: zendesk-help
description: Guide for efficiently searching and managing Zendesk tickets
---

# Zendesk Help

Guide for efficiently searching and managing Zendesk tickets.

## Available Tools

### `search_tickets` - Find tickets by criteria
Use this when you need to find tickets matching specific criteria:
- Text search in subject/description
- Filter by status, priority, assignee, requester
- Search by custom fields (e.g., transfer ID)
- Date range filters

### `get_tickets` - List recent tickets
Use this to browse recent tickets with pagination. Good for:
- Seeing what's new
- Getting an overview of recent activity

### `get_ticket` - Fetch specific ticket
Use this when you have a ticket ID and need full details.

## Search Examples

### Find tickets by transfer ID
The transfer ID custom field is `23301179390491`:
```
search_tickets(custom_field_id=23301179390491, custom_field_value="txn_abc123")
```

### Find open tickets for a customer
```
search_tickets(requester="customer@example.com", status="open")
```

### Find unassigned urgent tickets
```
search_tickets(status="new", priority="urgent")
```

### Text search with filters
```
search_tickets(query="payment failed", status="open")
```

### Find tickets created in a date range
```
search_tickets(created_after="2024-01-01", created_before="2024-01-31")
```

### Combine multiple filters
```
search_tickets(
    query="wire transfer",
    status="pending",
    tags=["escalated"],
    sort_by="created_at",
    sort_order="desc"
)
```

## Common Workflows

### Finding tickets related to a transfer
1. Use `search_tickets` with the transfer ID custom field
2. If no results, try text search with the transfer ID as query
3. Use `get_ticket` to fetch full details of matching tickets

### Finding a customer's tickets
1. Use `search_tickets` with `requester` email
2. Optionally filter by `status` to see only active tickets

### Finding unassigned work
1. Search for tickets with no assignee: `search_tickets(status="new")`
2. Or filter by specific queue using tags

## Tips

- Use `limit` parameter to control result count (max 100)
- Results are sorted by `updated_at` descending by default
- Combine multiple filters to narrow results
- For exact phrase matching, the query text is automatically quoted
