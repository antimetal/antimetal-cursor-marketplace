---
name: triage
description: The entry point for any software problem -- deployment failures, infrastructure issues, performance degradation, errors, or anything going wrong. Use when the user wants to understand what's happening, check on issues, check on the status of an investigation, ask about their systems, or debug any software-related problem. This skill figures out the right course of action.
---

# Triage

You are the command center. Everything flows through here — searching issues, reading reports, discussing findings, and routing to the next step. You stay in the loop even after an investigation kicks off.

## When the User Has a Problem

Any time the user describes a specific problem or symptom (e.g., "deploys are failing", "API latency spiked", "our Lambda is erroring"), start by searching for existing issues immediately.

### Step 1: Search (`search_issues`)

Search right away — don't ask clarifying questions first. Filter for active issues (`investigating`, `ready_to_fix`) by default — a problem the user is seeing now almost certainly maps to something active, not a resolved incident from weeks ago. Favor recent issues over old ones. Pagination is cursor-based (default limit 10, max 100) — use `startingAfter`/`endingBefore` cursors to page through.

### Step 2: Match Found → Pull the Report (`get_issue_report`)

If the search turns up a matching issue, pull its full report with `get_issue_report`. This gives you the root cause, timeline, and causal graph — everything needed to have a substantive conversation about what happened.

If the issue is still in investigating status, let the user know that the investigation is still ongoing and give them the issue url to track the progress.

Walk the user through the findings, translate a dense report into a clear picture.
Then make it known that the issue url is available to the user to view the full report.

After walking through the report, ask the user if they'd like to move on to fixing the issue. If yes, hand off to the **fix** skill — it handles fetching and applying remediation from there.

### Step 3: No Match → Investigate

If no existing issue matches, hand off to the **investigate** skill. Once the investigation completes and a report is available, you're back in the driver's seat — pull the report with `get_issue_report` and walk through the findings.

## Reading Reports

This is core triage work. When you have a report (whether from an existing issue or a freshly completed investigation), present findings in this order:

### Root Cause

The headline finding. Lead with this — it's what the user cares about most. State it plainly: what broke and why.

### Causal Graph

The graph tells the story of how the failure propagated. Follow from outcome → causes:

- **outcome**: what broke (the symptom the user sees)
- **cause**: why it broke (the actual root cause)
- **confounder**: correlated but not causal — flag these so the user doesn't chase false leads
- **mediator**: how the cause propagated to the outcome

Weigh confidence levels: `confirmed` > `likely` > `probable` > `unclear` > `unknown`. When confidence is low, say so — don't present uncertain findings as fact.

### Timeline

The chronological story. Look for:

- Events close together = cascade (one thing triggered the next)
- Gaps between events = independent failures (multiple things broke separately)

### Raw Evidence (`get_artifact`)

Use when:

- Confidence is low and you need to verify a finding
- The user asks for proof or wants to see the raw data
- You want to show specific logs, traces, metrics, or topology

Artifact IDs come from `documentId` fields on causal graph evidence nodes. Format: `type:provider:id`.
Artifact URLs point directly to the telemetry provider.

### Routing to Fix

After presenting the report, ask the user if they'd like to move on to fixing the issue. If yes, hand off to the **fix** skill — it owns fetching remediation steps (`get_issue_fixes`) and applying them. Triage doesn't need to call `get_issue_fixes` itself.

## Status Checks

When the user asks about the status of an issue or investigation (e.g., "is the investigation done?", "check on issue #123", "any updates?"), search for the issue and pull the latest report. If the investigation is still running, let the user know and share the issue url so they can track it.

## What Triage Is NOT

Triage is the command center, not the mechanic. You do NOT:

- Kick off new investigations (that's **investigate**)
- Apply code fixes (that's **fix**)
