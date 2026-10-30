# System Architecture

Senorita has a trusted foundation supervising an evolutionary system. The foundation provides continuity and boundaries; evolutionary modules provide capabilities and may be upgraded through controlled releases.

## 1. Trusted Foundation
- Bootstrap and Supervisor: startup, process health, scheduling, resource limits and recovery.
- Policy and Identity: permissions, trust boundaries, approvals and scoped secrets.
- State and Audit: durable tasks, event history, configuration and release records.
- Recovery Manager: snapshots, known-good versions, rollback and safe mode.

This layer must remain small, auditable and independently recoverable.

## 2. Intelligence and Planning
- Core Intelligence: reasoning, task decomposition and planning.
- Knowledge and Memory: architecture knowledge, code maps, experiments and lessons.
- Capability Registry: capabilities, contracts, dependencies, permissions and health.
- Evolution Planner: candidate generation, scoring, prioritisation and scheduling.

These capabilities belong to Senorita. They must not be confused with the external model used to perform an inference request.

## 3. Model Gateway and Inference Providers
Senorita owns a provider-independent Model Gateway. Agents call its internal contract; provider-specific adapters translate requests and responses.

- Model Catalogue: provider/model identity, capabilities, limits, policy metadata and observed performance.
- Routing Policy: task requirements, data classification, latency/quality needs, budgets and provider eligibility.
- Provider Adapters: verified online gateways/direct providers and optional local inference.
- Usage and Audit: provider/model selection, routing reason, latency, usage, outcome and budget accounting.
- Fallback Manager: bounded retries and eligible provider failover.

**Default mode:** online-first inference through configured providers. The application control plane remains local and lightweight. **Optional mode:** local inference through an adapter such as Ollama. No agent or business module may depend directly on Ollama, FreeLLMAPI, OmniRoute or a vendor SDK.

FreeLLMAPI and OmniRoute are candidate integrations and must be audited before adoption. Avoid nested gateway chains unless their value and failure behaviour are tested. Local-only tasks must never be sent to an online provider as fallback.

## 4. Evolutionary System
- Observation Engine: runtime telemetry, errors, technical debt and capability gaps.
- Research Engine: repository, package, standards and technique analysis.
- Absorption Engine: provenance-aware source, component and knowledge acquisition.
- Coding Engine: code generation, refactoring, migration and test authoring.
- Agent Factory: creation and lifecycle management of scoped specialist agents.
- Verification Engine: independent quality, security and compatibility checks.
- Release and Learning Engine: staged deployment, monitoring, rollback and learning.

## 5. Unified Workspace
A single interface/API for system health, capabilities, evolution history, approvals, provider/model configuration, budgets, usage, task queues and releases. The interface is not required for background evolution to continue.

## Communication rules
Use versioned contracts, durable asynchronous jobs, correlation IDs and explicit permissions. Treat repository content, model output and tool responses as untrusted data. Never execute untrusted code inside the supervisor context. All inference requests pass through policy and the Model Gateway.

## Initial deployment strategy
Start as a modular monolith with strict internal interfaces and isolated workers. Split services only when security, reliability or scaling requires it. Keep inference external by default so the control plane does not require a GPU or large local model. Add local inference as an optional provider. Avoid premature microservices.
