# Contributing to rEos

Thanks for contributing. rEos is designed to stay stable for decades — please respect the architecture.

## Before You Start

1. Read [`QWEN.md`](./QWEN.md) — it contains the architecture invariants.
2. Open an issue describing the change.
3. For large changes, wait for maintainer approval before coding.

## Ground Rules

- **Never break an invariant** (tenant isolation, authorization, accounting integrity, auditability, atomicity, event reliability, upgrade safety).
- **Kernel stays small.** New features go into Core, extensions, or plugins — not the Kernel.
- **Plugins use API only.** No direct DB writes. No modifying core tables.
- **All commands and queries go through the Kernel.** No raw SQL against core.
- **AI proposes; Kernel validates.** Never let AI write directly to protected tables.

## Development Setup

```bash
git clone https://github.com/your-org/reos.git
cd reos
cp .env.example .env
# Fill in secrets
docker compose up -d
docker compose exec api reos migrate
