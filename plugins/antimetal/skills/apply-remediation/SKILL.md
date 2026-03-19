---
name: apply-remediation
description: Apply an Antimetal remediation to the current codebase. Use when the user wants to fix an issue that Antimetal has investigated and has remediation steps available.
---

# Apply Antimetal Remediation

## Workflow

1. Use `get_issue_remediation` with the issue ID to get remediation steps
2. Remediation steps come in three types:
   - **info**: Context and explanation -- read and present to the user
   - **code**: File changes as an array of `{ filename, language?, content }` -- apply these to the codebase
   - **cli**: Shell commands to execute
3. For code changes: identify the target files in the user's project, read them, and apply the suggested changes with appropriate context
4. For CLI commands: present them to the user for approval before running
5. After applying changes successfully, update the issue status using `update_issue_status` with status `resolved`

## Guardrails

- Always show the user what changes will be made before applying code modifications
- Don't blindly apply code changes -- verify they make sense in the current codebase context
- If a remediation step references files that don't exist locally, flag this to the user
- CLI commands may need adaptation for the user's local environment
- Let the user decide whether to mark the issue as resolved after applying
