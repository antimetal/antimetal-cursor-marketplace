---
name: investigate
description: Dig deeper into software problems or ask questions about your systems. Use when the user wants to query Antimetal's AI for context, ask about their infrastructure, check telemetry, or kick off a full automated root cause investigation. This is the skill for any question about the user's systems or any problem that needs deeper analysis.
---

# Investigate

When triage can't find an existing issue, you take over to figure out the right level of analysis. You own two tools and the decision between them.

## Choosing the Right Approach

Present the fork clearly:

> "This seems like a new issue. Would you like to:
>
> 1. **Quick Q&A** — I can query Antimetal's AI to pull context on this right now
> 2. **Full investigation** — kick off an automated deep-dive that analyzes root cause, timeline, and causal chain (takes 3-10 min)"

Then follow whichever path they pick.

If you don't have an issue ID yet, use `search_issues` to see if one already exists. If an existing issue sounds like the same problem, use it. If there is not a close match, it is a new problem requiring a call to `investigate_issue`.

**Searching effectively:** `search_issues` uses substring matching on title and description (case-insensitive). Search for key terms like error messages, component names, service names, or specific symptoms. Try variations if your first search doesn't yield results—e.g., "database timeout" vs "database" vs "timeout".

A direct line to Antimetal's intelligent agent, which has access to all telemetry and integrations. It can run pinpointed telemetry queries, find context across your observability stack, and surface relevant data without the overhead of a full investigation. Use this when the user wants quick, targeted answers — whether it's a broad question about their systems or a specific problem they want context on before deciding whether to go deeper.

Always pass `conversation_id` on follow-ups to maintain context.

## Full Investigation (`investigate_issue`)

Kicks off Antimetal's automated investigation engine. This is async and takes 3-10 minutes. Returns an issue ID to track.

**Before kicking this off, gather context.** Don't fire it on a vague description. Ask clarifying questions first.

Once you have a clear, scoped problem statement, then kick off the investigation. A well-defined input produces a far better report.

**Direct to Issue Page:** After kicking off the investigation, immediately provide the user with a link to the issue page. Since the investigation takes 3-10 minutes, don't wait in the cursor plugin—encourage them to monitor progress and the full chain of thought on the issue page. This prevents poor UX from waiting for async results.

Once the investigation is kicked off, hand back to **triage** — which will be in charge of reading and discussing the report.

## What Investigate Is NOT

Investigate is not the place to read the report or discuss the findings. That's the responsibility of **triage**.

Investigate decides how to dig deeper and kicks things off. It does not:

- Search for existing issues or read reports (that's **triage**)
- Apply code changes or run CLI commands (that's **fix**)
