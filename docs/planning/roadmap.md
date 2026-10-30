# Roadmap

## Phase 0 — Repository, environment and technology foundation
Inspect the target environment, define standards, threat model, data classification, autonomy policy, bootstrap and backups. Audit existing FreeLLMAPI and OmniRoute installations and verify provider API compatibility, limits, security and licensing. Confirm Python/Node/Windows/WSL/Docker versions and pin a reproducible baseline.

## Phase 1 — Trusted SPS kernel
Build supervisor, policy engine, durable state, event log, capability registry, isolated workers, safe mode and rollback.

## Phase 2 — Provider-independent Model Gateway
Define internal inference contracts, provider registry, model catalogue, capability-aware routing, provider adapters, budgets, privacy rules, usage audit and bounded fallback. Integrate verified online gateway/provider routes first; add Ollama as an optional local adapter. The application must not depend on a local model.

## Phase 3 — Self-understanding and planning
Build code/dependency maps, telemetry, candidate generation, scoring and autonomous backlog management.

## Phase 4 — Coding and verification loop
Add isolated coding, automated verification, controlled release and automatic rollback.

## Phase 5 — Absorption Engine
Add repository discovery, licence/security/provenance evaluation and source/component/knowledge absorption.

## Phase 6 — Agent Factory
Create specialist agents with explicit contracts, scoped permissions, lifecycle and compatibility tests.

## Phase 7 — Long-running autonomy
Add event-driven scheduling, resource-aware execution, fallback strategies, soak tests and restore drills.

## Phase 8 — Advanced evolution
Improve architecture, collaboration, controlled core upgrades and optional distributed workers.

A phase is complete only with acceptance evidence, not a demo alone. Autonomous self-modification must not begin until the trusted kernel, isolation, audit, backup and rollback are verified.
