# rEos — Qwen Project Memory

> Rust-based Enterprise OS. One platform. Infinite business models. No code forks.

## What This Project Is

rEos is a modular, multi-tenant SaaS Enterprise Operating System.
- **Kernel**: small, secure, stable — written in Rust.
- **Universal Core**: Party, Contact, Item, Order, Invoice, Payment, Inventory, Accounting.
- **Extensions**: Country, Industry, Business Model — installed as signed plugins via API.
- **UI**: React + TypeScript.
- **Storage**: PostgreSQL (central), SQLite (edge), Redis (cache), NATS (events), S3 (objects).

## Architecture Invariants — Never Break These

- Tenant isolation
- Authorization
- Accounting integrity
- Auditability
- Transaction atomicity
- Event reliability
- Upgrade safety

**Lower layers may extend or configure upper layers but must NEVER modify protected invariants.**

## Golden Rule

> If a plugin needs to change the Kernel to work, the design is wrong.
> The Kernel must expose a contract instead.

Plugins talk to the Kernel **only** through:
- Stable APIs
- Metadata registration
- Commands and Queries
- Events

No direct DB writes. No core table changes. No importing internal Kernel crates.

## Tech Stack

| Area | Technology |
|---|---|
| Kernel / Engines | Rust |
| UI | React + TypeScript |
| Central DB | PostgreSQL |
| Edge DB | SQLite |
| Cache | Redis |
| Events | NATS / JetStream |
| Objects | S3-compatible |
| Search | PostgreSQL → OpenSearch / Meilisearch |
| Vector / RAG | PostgreSQL + pgvector |

## Rust Workspace Conventions

- One crate per stable responsibility.
- Each crate exposes a deliberate public contract — no leaking internals.
- No premature microservices. Start with a Cargo workspace.
- Recommended crates: `identity`, `tenant`, `organization`, `security`, `authorization`, `metadata`, `object`, `schema`, `transaction`, `command`, `query`, `workflow`, `event`, `policy`, `audit`, `storage`, `search`, `scheduler`, `notification`, `configuration`, `localization`, `integration`, `plugin`, `runtime`, `api`.

## Code Style

- **Rust**: `cargo fmt`, `cargo clippy -- -D warnings`. No `unwrap()` in library code. Use `thiserror` for error types.
- **TypeScript**: `prettier`, `eslint`. Strict mode. No `any`.
- **Commits**: Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`).
- **Naming**: `snake_case` for Rust, `camelCase` for TS, `PascalCase` for types/objects.

## Build & Test Commands

```bash
# Rust workspace
cargo build
cargo test
cargo clippy -- -D warnings
cargo fmt --check

# UI
cd ui
npm install
npm run dev
npm run test
npm run lint

# Full stack (Docker)
docker compose up -d
docker compose exec api reos migrate
docker compose exec api reos --help
