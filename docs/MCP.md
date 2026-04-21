# MCP Setup

ForgeKit works without MCP, but MCP gives the team stronger workflow tools:

- create and inspect sessions
- build and search the local memory index
- audit missing or stale memory
- compact completed sessions and oversized hot memory
- show a project dashboard
- use optional local LanceDB vector search

## Install

From the extension root:

```bash
cd mcp-server
npm install
npm run check
```

LanceDB is optional. If the native package does not install on a machine,
ForgeKit still works with the JSONL/hash-vector backend.

## Enable

Add this block to `gemini-extension.json` after the MCP dependencies are
installed:

```json
{
  "mcpServers": {
    "forgekit": {
      "command": "node",
      "args": ["${extensionPath}${/}mcp-server${/}index.js"],
      "cwd": "${extensionPath}${/}mcp-server",
      "env": {
        "FORGEKIT_WORKSPACE_PATH": "${workspacePath}",
        "FORGEKIT_VECTOR_BACKEND": "auto"
      }
    }
  }
}
```

Restart Gemini CLI after changing extension-level config.

## Backend Modes

Use `FORGEKIT_VECTOR_BACKEND` to control local recall:

- `auto`: use LanceDB when installed, otherwise JSONL/hash-vector fallback
- `lancedb`: prefer local LanceDB
- `jsonl`: force the dependency-light local backend

The memory source of truth remains markdown under `.gemini/`. The index under
`.gemini/forgekit/memory/` is a rebuildable cache.

## Tools

- `forgekit_initialize_workspace`
- `forgekit_create_session`
- `forgekit_get_status`
- `forgekit_archive_session`
- `forgekit_index_memory`
- `forgekit_search_memory`
- `forgekit_audit_memory`
- `forgekit_compact_memory`
- `forgekit_dashboard`

## Recommended Test

Inside a sample project, run:

```text
/team:init-project
/team:feature "Build a small endpoint and tests"
/team:dashboard
/team:memory-search "current task"
```

The final response for non-trivial work should include memory files changed and
memory index refresh status.
