# Augmented Search

Local documentation RAG system for Claude Code. Answer questions using only local docs, no web search.

## Structure

- **`docs/`** - Library documentation (duckdb, polars, pytest, fumadocs)
- **`CLAUDE.md`** - Instructions for Claude Code

## Usage

Ask Claude questions about the libraries in `docs/`. Claude will search local files using ripgrep and answer from local docs only.

## Setup

`git clone` your favourite stack docs into `docs/`.
