# Quickstart

## 1. Link the extension

From the `forgekit/` directory:

```bash
gemini extensions link .
```

Restart Gemini CLI if it is already open.

## 2. Check that it loaded

Inside Gemini CLI:

```text
/extensions list
```

## 3. Initialize project memory

In a target project:

```text
/team:init-project
```

This creates the expected `.gemini/` memory and session folders.

For stronger memory automation, enable the optional MCP server:

```bash
cd mcp-server
npm install
npm run check
```

Then follow [MCP setup](MCP.md).

## 4. Run basic commands

```text
/team:orchestrate "Summarize this repository"
/team:quality-gate
/team:session-update
/team:dashboard
/team:checkpoint
```

## 5. Validate local changes

From `forgekit/`:

```bash
gemini extensions validate .
python3 -c "import tomllib; tomllib.load(open('commands/team/fix-issue.toml','rb'))"
node --check mcp-server/index.js
```

## Current Caveat

ForgeKit can require memory and index updates, and the dashboard can report
missing work. Gemini CLI still owns final instruction-following behavior.
Use `/team:checkpoint` or `/team:release-readiness` when you need a strict
answer about whether work is truly ready.
