---
name: investigate-issue
description: Investigate any infrastru Antimetal issue by fetching its root cause, causal tree, timeline, and remediation. Use when the user asks about an incident, wants to understand what happened, or needs to debug a production issue tracked in Antimetal.
---

# Investigate an Antimetal Issue

## Workflow

1. Use `list_issues` if the user hasn't specified an issue -- help them identify the right one
2. Use `get_issue` with the issue ID (UUID) or number to get full details including seeds, version history, and current status
3. Use `get_issue_root_cause` to get the root cause analysis -- this returns an incident overview, analysis, and evidence with artifact document IDs
4. Use `get_issue_causal_tree` to see the causal graph. Nodes have a `nodeType` (outcome, cause, confounder, mediator) and `confidence` (unknown, unclear, probable, likely, confirmed). Evidence on nodes includes `documentId` refs you can use with `fetch_artifact`
5. Use `get_issue_timeline` to understand the chronological sequence of events
6. Summarize findings: what happened, why, and what's affected

## When to go deeper

- If the causal tree references artifact document IDs in evidence nodes, use `fetch_artifact` with that ID to get the raw data (logs, traces, metrics, events, files, topology)
- If the user wants to fix the issue, use `get_issue_remediation` for actionable steps -- these come as `info`, `code`, and `cli` step types
- Artifact IDs follow the format `type:provider:id` (e.g., `log:datadog:a9c131...`, `trace:gcp:abc123`)

## Output

- Clear summary of the incident
- Root cause explanation with supporting evidence
- Timeline of events
- Affected services/components
- Suggestions for next steps (remediation, artifact deep-dives)
