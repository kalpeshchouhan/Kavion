# ForgeKit MCP Server

This is an optional MCP workflow server for ForgeKit.

It is not enabled in `gemini-extension.json` yet, so ForgeKit can load without
Node dependencies. Enable it after installing dependencies.

## Install

```bash
cd mcp-server
npm install
npm run check
```

`npm install` also installs optional LanceDB support when the platform supports
the native package. ForgeKit falls back to JSONL/hash-vector recall if LanceDB
is not installed.

## Enable

Add this to `gemini-extension.json`:

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

Restart Gemini CLI after enabling.

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
- `forgekit_check_workflow`
- `forgekit_record_checkpoint`
- `forgekit_handoff_report`
- `forgekit_release_readiness`

## Local Memory Index

The memory tools build and search a local cache under:

```text
.gemini/forgekit/memory/
  manifest.json
  memory.jsonl
  vectors.jsonl
  lancedb/
```

Markdown files remain the source of truth. The index is used only for bounded
recall and search.

The backend mode defaults to `auto`:

- use local LanceDB when `@lancedb/lancedb` is installed
- otherwise use JSONL chunk metadata, exact token matching, and local hash-vector similarity

Set `FORGEKIT_VECTOR_BACKEND=jsonl` to force the dependency-light backend.
Set `FORGEKIT_VECTOR_BACKEND=lancedb` to require LanceDB when installed.
