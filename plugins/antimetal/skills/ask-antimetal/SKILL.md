---
name: ask-antimetal
description: Ask Antimetal's AI agent a question about your cloud infrastructure, incidents, or observability data. Use when the user has a general question about their cloud environment that isn't about a specific issue.
---

# Ask Antimetal

## Workflow

1. Use `ask` with the user's question
2. The response includes an `answer` (natural language) and a `conversation_id`
3. For follow-up questions, pass the returned `conversation_id` to continue the conversation with context

## When to use

- General cloud infrastructure questions: "What services had the most errors last week?"
- Cost and usage queries: "How much are we spending on Lambda?"
- Anomaly detection: "Are there any anomalies in our CloudWatch metrics?"
- Trend analysis: "Show me the latency trends for the API gateway"
- Any question that doesn't map to a specific known issue

## Guardrails

- Present the answer clearly -- it's already in natural language
- Track the `conversation_id` across turns so follow-ups maintain context
- If the question is about a specific issue, prefer the investigate-issue skill instead
