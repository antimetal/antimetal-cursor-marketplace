---
name: antimetal-mcp-setup
description: REQUIRED setup for using Antimetal's MCP server to triage, investigate, and fix software issues. IMPORTANT If you want to use Antimetal, read these instructions BEFORE checking for what tools are available for Antimetal as that MAY NOT WORK.
---

IMPORTANT: You must complete this setup before using any Antimetal MCP tools. Do not attempt to list or call Antimetal tools until these requirements are satisfied.

## How It Works

The Antimetal MCP server authenticates via an API key sent in the `Authorization` header. The plugin's MCP configuration (`../../mcp.json` relative to this file) references the `ANTIMETAL_API_KEY` environment variable. If this variable is missing or empty, every MCP request will fail silently.

## Setup Checklist

1. **Read the MCP config.** Open `../../mcp.json` (the grandparent directory of this skill) and confirm it references `ANTIMETAL_API_KEY` in the authorization header.

2. **Verify the API key is set.** Check whether `ANTIMETAL_API_KEY` exists in the environment.
   - **If it's set:** skip ahead -- you're good to go.
   - **If it's not set:** stop here. Walk the user through getting one:
     1. Sign up or log in at https://antimetal.com
     2. Generate an API key from account settings at https://overlook.antimetal.com/settings/api-keys
     3. Add it to their shell profile:
        ```bash
        export ANTIMETAL_API_KEY="am_..."
        ```
     4. Source the profile or restart the terminal, then reload the Cursor window via the Command Palette (`⌘⇧P` on Mac, `Ctrl+Shift+P` on Windows/Linux) → **Reload Window**

   Do NOT proceed past this step without a valid key. Do not check tool schemas, do not attempt MCP calls. The user must provide the key first.

3. **Continue.** Once the key is confirmed, hand off to whichever skill the user needs -- triage, investigate, or fix.