---
name: triage-issues
description: List and triage Antimetal issues by severity and status. Use when the user wants to see open incidents, prioritize work, or get an overview of current issues.
---

# Triage Antimetal Issues

## Workflow

1. Use `list_issues` to get the current issue list -- returns uuid, number, title, severity, status, environment, triggeredAt, and seedCount
2. Group and present issues by status: `investigating`, `ready_to_fix`, `resolved`, `muted`
3. Highlight high severity issues that need immediate attention
4. For any issue the user wants to dive into, use `get_issue` for full details

## Pagination

`list_issues` is cursor-based with a default limit of 10 (max 100). Use `startingAfter` and `endingBefore` cursors to page through results. The response includes an `after` cursor for the next page.

## Guardrails

- Summarize the list first -- don't fetch full details for every issue upfront
- Only drill into specific issues when the user asks
- When presenting issues, lead with severity and status to help the user prioritize
