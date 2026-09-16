
---

## 2. `AGENTS.md` (Project Root)

For other AI tools (and Qwen reads this too).

```markdown
# rEos — Agent Instructions

See [QWEN.md](./QWEN.md) for full project memory. This file mirrors the essentials for tool-agnostic AI agents.

## Project

rEos is a Rust-based Enterprise OS with a small stable kernel and API-only plugin extensions.

## Non-Negotiable Rules

1. Kernel stays small and stable.
2. Plugins never modify core tables or Kernel source.
3. All plugin interaction is via API, commands, queries, metadata, events.
4. Tenant isolation, authorization, accounting integrity, auditability, atomicity, event reliability, upgrade safety are invariants.
5. AI proposes; Kernel validates and guarantees.

## Commands

```bash
cargo build && cargo test && cargo clippy -- -D warnings
cd ui && npm install && npm run dev
docker compose up -d
docker compose exec api reos migrate
