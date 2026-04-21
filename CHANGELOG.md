# Changelog

## 0.3.0 - 2026-04-22

- Added optional local LanceDB memory backend with JSONL/hash-vector fallback.
- Added automatic memory index refresh requirements to feature, orchestration,
  bug-fix, memory-update, session-update, and init workflows.
- Added MCP tools:
  - `forgekit_compact_memory`
  - `forgekit_dashboard`
- Added `/team:dashboard` for memory, session, plan, report, and index status.
- Strengthened memory compaction guidance for completed sessions and oversized
  hot memory files.
- Added MCP setup documentation and backend mode configuration.
- Bumped extension and MCP server versions to `0.3.0`.

## 0.2.0 - 2026-04-22

- Added local memory index commands:
  - `/team:memory-index`
  - `/team:memory-search`
  - `/team:memory-audit`
  - `/team:memory-compact`
- Added MCP tools for local memory indexing, bounded memory search, and memory
  audit.
- Added local hash-vector recall cache under `.gemini/forgekit/memory/`.
- Kept Markdown memory files as the source of truth.
- Bumped extension and MCP server versions to `0.2.0`.

## 0.1.0 - 2026-04-21

- Added ForgeKit extension scaffold with agents, skills, commands, memory
  templates, and optional MCP server scaffold.
- Added `/team:session-update` for focused session-state maintenance.
- Tightened `/team:fix-issue` with bounded inspection and a memory/workflow
  fast path.
- Added project-memory session, plan, and report starter templates.
- Added contributor and architecture documentation.
