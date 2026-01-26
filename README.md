# claude-rag

Local documentation RAG system for Claude Code. Answer questions using only local docs, no web search.

## Structure

- **`docs/`** - Library documentation (duckdb, polars, pytest, fumadocs)
- **`snippets/`** - Your code patterns (empty currently)
- **`projects/`** - Project-specific docs (empty currently)
- **`CLAUDE.md`** - Instructions for Claude Code

## Usage

Ask Claude questions about the libraries in `docs/`. Claude will search local files using ripgrep and answer from local docs only.

## Setup

Add your snippets to `snippets/`, project docs to `projects/` for Claude to reference them, and `git clone` your favourite stack docs into `docs/`.
