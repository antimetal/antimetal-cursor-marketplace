# Antimetal Cursor Plugin

Bring [Antimetal's](https://antimetal.com) cloud investigation intelligence into Cursor. Investigate incidents, analyze root causes, fetch observability artifacts, and apply remediations -- all without leaving your editor.

## Setup

### 1. Get an API Key

Sign up at [antimetal.com](https://antimetal.com) and generate an API key from your account settings.

### 2. Set Your Environment Variable

```bash
export ANTIMETAL_API_KEY="your-api-key-here"
```

Add this to your shell profile (`~/.zshrc`, `~/.bashrc`, etc.) so it persists.

### 3. Install the Plugin

Install from the [Cursor Marketplace](https://cursor.com/marketplace) by searching for **Antimetal**, or use the command palette:

```
/add-plugin antimetal
```

## What's Included

### MCP Server

Connects to Antimetal's remote MCP server at `mcp.antimetal.com`, giving the Cursor agent access to these tools:

| Tool | Description |
|------|-------------|
| `list_issues` | Paginated list of issues with severity, status, and environment |
| `get_issue` | Full issue details including seeds and version history |
| `get_issue_root_cause` | Root cause analysis with evidence and artifact references |
| `get_issue_causal_tree` | Causal graph showing how events led to the incident |
| `get_issue_timeline` | Chronological sequence of investigation events |
| `get_issue_remediation` | Actionable fix steps (code changes, CLI commands, context) |
| `create_issue` | Create a new issue and trigger an investigation |
| `update_issue_status` | Update status: investigating, ready_to_fix, resolved, muted |
| `delete_issue` | Permanently delete an issue and all associated data |
| `fetch_artifact` | Fetch investigation artifacts: logs, traces, metrics, events, files, topology |
| `ask` | Ask Antimetal's AI about your infrastructure, costs, or issues |

### Skills

- **investigate-issue** -- Full investigation workflow: root cause, causal tree, timeline, and artifacts
- **apply-remediation** -- Apply Antimetal's suggested fixes to your codebase
- **ask-antimetal** -- Ask questions about your cloud infrastructure

### Agent

- **incident-responder** -- Dedicated agent for triaging and investigating production incidents

### Rules

- **antimetal-conventions** -- Conventions for working with Antimetal data (artifact ID formats, status values, etc.)

## Example Prompts

```
Investigate issue #42
What are the open high severity issues?
Apply the remediation for issue #15
What services had the most errors last week?
Triage my current incidents
```

## Links

- [Antimetal](https://antimetal.com)
- [Documentation](https://docs.antimetal.com)
- [MCP Server](https://mcp.antimetal.com)
