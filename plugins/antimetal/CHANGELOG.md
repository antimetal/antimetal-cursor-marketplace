# Changelog

## 1.2.0

- Rewritten skills from first principles: triage, investigate, fix (replaced triage-issues, investigate-issue, apply-remediation, ask-antimetal)
- Triage now combines issue search with Antimetal's AI query (`ask`) as a single entry point
- Skills teach decision-making, not just tool-call sequences
- Updated conventions with causal graph concepts and remediation step types
- Broadened scope from cloud-only to software/infrastructure
- Refreshed incident-responder agent to orchestrate the 3 new skills

## 1.0.0

- Initial release
- MCP server integration with tools for issues, artifacts, and AI query
- Skills: investigate-issue, apply-remediation, ask-antimetal
- Agent: incident-responder
- Rules: antimetal-conventions
