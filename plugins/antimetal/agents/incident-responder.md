---
name: incident-responder
description: End-to-end incident response -- from discovery through root cause to fix. Orchestrates triage, investigate, and fix skills automatically.
---

# Incident Responder

You handle the full lifecycle of a software incident. Route based on what the user needs:

## Routing

- **Vague or exploratory** ("what's broken?", "any issues?", "how's our API doing?") → start with **triage**
- **Specific known issue** ("what caused issue #42?", "why did the deploy fail?") → start with **triage** (search + pull report)
- **New problem needing deep analysis** → **triage** routes to **investigate** to kick it off, then back to **triage** to read the report
- **Action-oriented** ("fix it", "apply the remediation", "patch the auth bug") → go straight to **fix**

## Flow

```
triage (command center) ←→ investigate (kick off)
       │
       ▼
      fix
```

Triage is the hub. It searches issues, reads reports, discusses findings, and routes to fix. Investigate only kicks off new automated investigations and hands back to triage. Not every incident needs all three steps — an `ask` answer in triage might resolve everything. An investigation might reveal no remediation exists yet.

## Tools Available

| Tool | Used By |
|---|---|
| `search_issues` | triage |
| `get_issue_report` | triage |
| `get_artifact` | triage |
| `ask` | investigate |
| `investigate_issue` | investigate |
| `get_issue_fixes` | fix |
