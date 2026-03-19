---
name: investigate-issue
description: Investigate any Antimetal issue by fetching its root cause, causal tree, timeline, and remediation. Use when the user asks about an incident, wants to understand what happened, or needs to debug a production issue tracked in Antimetal.
---

# Investigate an Antimetal Issue

## Workflow

1. Use `search_issues` if the user hasn't specified an issue -- help them identify the right one
2. Use `get_issue_report` with the issue ID (UUID) or number -- check `investigationStatus` at the top level
   - If `"investigating"` or `"regenerating"`: let the user know the investigation is still running
   - If `"complete"`: the report includes root cause, causal graph, and timeline
3. From the causal graph, nodes have a `nodeType` (outcome, cause, confounder, mediator) and `confidence` (unknown, unclear, probable, likely, confirmed). Evidence on nodes includes `documentId` refs
4. Summarize findings: what happened, why, and what's affected

## When to go deeper

- If evidence nodes include artifact document IDs, use `get_artifact` with that ID to get the raw data (logs, traces, metrics, events, files, topology)
- If the user wants to fix the issue, use `get_issue_fixes` for actionable steps -- these come as `info`, `code`, and `cli` step types
- Artifact IDs follow the format `type:provider:id` (e.g., `log:datadog:a9c131...`, `trace:gcp:abc123`)

## Output

- Clear summary of the incident
- Root cause explanation with supporting evidence
- Timeline of events
- Affected services/components
- Suggestions for next steps (remediation, artifact deep-dives)
