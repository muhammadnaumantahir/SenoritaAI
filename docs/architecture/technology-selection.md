# Technology Selection and Implementation Baseline

**Status:** Proposed baseline — approved for initial implementation planning  
**Version:** 0.1  
**Scope:** Senorita SPS runtime, AI inference, developer workspace and deployment foundation

## 1. Executive decision

Senorita will use an **online-first, provider-independent AI architecture with optional local-model support**.

The application, trusted supervisor, agent runtime, memory, capability registry, evolution planner, research and coding orchestration, verification pipeline, audit trail and user workspace run on the user's machine or trusted deployment host. Model inference is accessed through configurable online providers by default. Local inference is an optional provider, not a prerequisite.

This separates Senorita's software capabilities from the hardware required to run large language models. A modest Windows PC can host the orchestration and control plane while configured remote providers perform inference. Actual provider availability, latency, pricing, quotas, terms and data handling remain external dependencies and must be visible to the user.

Senorita must not depend on any single model, vendor, gateway, API format or inference runtime.

## 2. Target principles

1. **Provider independence:** agents call Senorita's internal model interface, never vendor SDKs directly.
2. **Online-first, local-optional:** remote inference is the default deployment mode; local inference can be enabled per task or policy.
3. **Capability-aware routing:** select a model based on task requirements, not only a preferred-model name.
4. **Cost and quota control:** every call has a budget, timeout, token limit and usage record.
5. **Privacy-aware routing:** classify data before sending it to an external provider; block or redact restricted data.
6. **Graceful degradation:** provider failures must not corrupt durable jobs; retry or route to an eligible alternative.
7. **Auditable decisions:** record provider, model, routing reason, usage, latency, outcome and policy decision without logging secrets.
8. **Replaceable components:** keep adapters and infrastructure behind stable contracts.
9. **Security before autonomy:** model output is untrusted input; tool execution and code changes require policy enforcement and independent verification.
10. **Resource-aware operation:** orchestration should remain lightweight; workers and model inference must have separate resource budgets.

## 3. Recommended stack

| Concern | Initial choice | Decision notes |
|---|---|---|
| Primary language | Python 3.13 | Use the installed Python baseline only after environment verification; pin a supported version for reproducible builds. |
| Backend/API | FastAPI + Pydantic | Typed request/response contracts, validation and API documentation. |
| Frontend | React + TypeScript + Vite | One unified workspace; keep UI independent of orchestration internals. |
| Initial database | SQLite | Suitable for single-machine bootstrap and durable local state. Define repository interfaces so PostgreSQL can be added for multi-worker/shared deployments. |
| Future shared database | PostgreSQL | Adopt when concurrent workers, remote deployment or operational requirements justify it. |
| AI abstraction | Senorita Model Gateway interface | Internal provider-neutral contract; do not couple domain logic to LiteLLM or another framework. |
| Initial provider integrations | FreeLLMAPI and OmniRoute adapters, subject to endpoint/auth/compatibility audit | Reuse existing user-installed gateways if they meet the contract. Do not assume they are interchangeable or route through each other without testing. |
| Direct online providers | Optional provider adapters | Add only providers whose API, terms, security, pricing and data policies have been reviewed. |
| Local inference | Optional Ollama adapter | Keep it as an opt-in provider for privacy, offline use, experimentation or cost control. Not required for baseline operation. |
| Agent orchestration | Senorita-owned Python runtime | Explicit task states, contracts, permissions, budgets, checkpoints and durable execution. External frameworks may be evaluated as absorbable components. |
| Background work | Persistent job records + lightweight worker processes | Begin without Kafka or a complex distributed queue. Add a broker only when measured scale requires it. |
| Code isolation | Docker/WSL2 sandbox where available + Git worktrees | Never execute untrusted repository code inside the trusted supervisor. Provide a restricted fallback or disable execution if isolation is unavailable. |
| Testing | pytest, Ruff, mypy, Playwright | Unit, integration, static, API and browser-level checks. |
| Observability | Structured logs, metrics and correlation IDs; OpenTelemetry-compatible instrumentation | Keep local diagnostics useful without requiring a hosted telemetry service. |
| Source control | Git + GitHub | Branch/worktree per candidate, traceable commits, release tags and rollback points. |
| Packaging/launch | Windows-first launcher; Docker Compose only for services that benefit from isolation | Avoid requiring Kubernetes or a large always-on container stack. |

Versions are not frozen by this document. Pin exact versions only after Phase 0 compatibility checks and record them in dependency manifests and the environment baseline.

## 4. Logical architecture

### 4.1 Local control plane

The following capabilities belong to Senorita and must not be outsourced to an AI provider:

- Trusted bootstrap and supervisor.
- Identity, policy, permissions and secret access.
- Durable task state, event history and audit records.
- Capability registry and architecture knowledge.
- Agent lifecycle and orchestration.
- Evolution planning and scheduling.
- Research and repository analysis workflow.
- Coding workspace management and patch application.
- Test orchestration, verification and release decisions.
- Backup, recovery and rollback.
- Unified user workspace and administration API.

### 4.2 Model inference plane

The Model Gateway is an internal Senorita subsystem with a stable contract. It resolves a task to an eligible provider/model and invokes a provider adapter.

Expected flow:

1. Agent submits a structured inference request to the internal gateway.
2. Policy classifies data sensitivity and permitted destinations.
3. Task requirements declare capabilities such as coding, reasoning, context size, tool calling, structured output or vision.
4. Router filters eligible models by policy, availability, configured budget and required capabilities.
5. Router selects a provider/model using configured preferences and observed performance.
6. Adapter normalises provider-specific request and response formats.
7. Usage, latency, routing reason and outcome are recorded.
8. On eligible transient failure, retry or fail over within the task's budget; otherwise pause safely and report the reason.

The model gateway must support explicit model pinning for reproducibility, as well as policy-driven automatic selection.

### 4.3 Provider adapter contract

Each adapter should implement a common interface for:

- Provider identity and configuration validation.
- Model/capability discovery or a maintained capability manifest.
- Text/chat completion.
- Streaming where supported.
- Tool/function calling where supported.
- Structured output where supported.
- Token/usage reporting when supplied.
- Timeouts, cancellation and bounded retries.
- Normalised errors and health checks.
- Provider-specific limitations and feature flags.

Do not pretend every provider supports every feature. The router must know which capabilities are genuinely supported.

## 5. Provider strategy

### 5.1 Initial gateway candidates

**FreeLLMAPI** and **OmniRoute** are candidates because they already exist in the user's environment. Before integrating, inspect their actual source/configuration and verify:

- Base URL and authentication method.
- OpenAI-compatible or other API surface.
- Model listing and model identifiers.
- Streaming and tool-call behaviour.
- Structured-output support.
- Rate limits, quotas, concurrency and timeout behaviour.
- Provider fallback semantics.
- Logging and secret handling.
- Licence, maintenance and security posture.

Build independent adapters if their APIs differ. Avoid a gateway chain such as Senorita → FreeLLMAPI → OmniRoute → provider unless there is a deliberate, tested reason; nested routing can create loops, opaque billing, duplicated retries and confusing failures.

Senorita should also be able to connect directly to a reviewed provider adapter when useful. No provider is mandatory.

### 5.2 Model selection and routing

Maintain a model catalogue with fields such as:

- Provider and model identifier.
- Supported capabilities and modalities.
- Context and output limits, when known.
- Tool calling and structured-output support.
- Streaming support.
- Data retention/training policy metadata, where verified.
- Pricing or quota metadata, with source and last-checked timestamp.
- Observed latency, error rate and task-specific quality.
- Availability and user configuration state.

Routing inputs include task type, required capabilities, sensitivity class, quality threshold, latency target, token budget, monetary budget and provider availability.

Use a configurable strategy:
- **Pinned:** exact provider/model for reproducibility.
- **Preferred:** try the user's preferred eligible model, then approved fallbacks.
- **Capability-based:** choose among models meeting the task contract.
- **Local-only:** use a local provider or fail safely; never silently send the task online.
- **Online-only:** exclude local inference.
- **Manual:** ask for a selection when policy or configuration requires it.

Do not route solely by benchmark scores or provider marketing claims. Collect Senorita's own task-specific evaluation data.

### 5.3 Optional local models

Ollama is an optional local adapter. Local models may be useful for private tasks, offline operation, low-cost routine work or development. The system must check available RAM/VRAM, model size, context settings and concurrent load before enabling a model.

Local inference must be switchable without changing agent or business logic. Senorita should continue to operate in online mode if Ollama is not installed or no local model is configured.

## 6. Security, privacy and spending controls

- Store provider credentials in an OS-protected secret store where feasible; never commit credentials or write them to ordinary logs.
- Define data classes (public, internal, confidential, restricted) and provider eligibility for each.
- Default to blocking restricted data from external inference unless a specifically approved policy permits it.
- Provide redaction and minimise prompt context.
- Make provider data retention/training terms visible and record review dates; do not infer privacy guarantees from API compatibility.
- Enforce per-task, per-agent, per-day and global token/spend limits.
- Require explicit configuration before paid providers are enabled.
- Set bounded timeouts, retries and concurrency.
- Treat all model responses, repository files and tool outputs as untrusted.
- Require human approval for provider credential changes, budget increases and policy exceptions.
- Keep audit and recovery controls outside the authority of evolutionary agents.

## 7. Windows-first deployment profile

Initial target is a single Windows workstation with modest memory and no discrete GPU requirement for the control plane.

- Run the FastAPI service, database, scheduler and UI locally.
- Run isolated coding/research workers with resource limits.
- Use Docker Desktop/WSL2 only for sandboxed execution or services that require it.
- Keep inference remote by default; local Ollama is optional.
- Provide a simple launcher and health/status page.
- Avoid Kubernetes, Kafka and a multi-database setup in the initial phase.
- Design interfaces so workers can later move to another machine without redesigning the system.

The system cannot promise uninterrupted autonomy: power, Windows updates, network access, provider outages, account quotas and hardware availability remain external dependencies. Durable jobs and restart recovery should resume eligible work after interruption.

## 8. Implementation sequence

1. **Phase 0 — Verify environment:** inspect Python/Node/Git/Docker/WSL, existing FreeLLMAPI and OmniRoute APIs, network exposure, secrets and hardware/resource limits.
2. **Trusted kernel:** bootstrap, supervisor, policy, durable state, event log, secrets boundary, health checks and safe mode.
3. **Model Gateway:** internal contracts, provider registry, model catalogue, routing policy, budgets and usage audit.
4. **First adapters:** integrate the best verified existing gateway(s); add a direct provider adapter only when justified. Add Ollama as optional.
5. **Agent runtime:** task contracts, tool permissions, durable checkpoints, retries and worker lifecycle.
6. **Sandbox and verification:** isolated worktrees, code execution restrictions, tests, patch review and rollback.
7. **Evolution capabilities:** observation, research, planning, absorption, coding and controlled release.
8. **Workspace:** provider/model configuration, budgets, task queue, health, audit and evolution history.

Do not begin autonomous self-modification before the trusted kernel, policy enforcement, sandboxing, audit, backup and rollback have passed acceptance tests.

## 9. Acceptance criteria for the technology foundation

- Agent code depends only on Senorita's internal model interface.
- At least two independently configured inference routes can be selected without changing agent code, once two usable routes are verified.
- A provider can be disabled or replaced through configuration.
- Local inference can be absent without preventing online-mode startup.
- Local-only policy never falls back to an online provider.
- Online-only policy never selects a local model.
- Per-task and global budgets are enforced and audited.
- Provider errors are normalised; retries are bounded and do not duplicate unsafe tool actions.
- Secrets are excluded from logs and repository history.
- Data classification is enforced before external inference.
- A model/provider outage does not lose durable task state.
- Routing decisions and usage can be inspected in the workspace.
- The trusted supervisor and recovery controls cannot be modified by ordinary evolutionary agents.

## 10. Open decisions

These remain evidence-based Phase 0 decisions, not assumptions:

- Which of FreeLLMAPI and OmniRoute should be the first adapter, or whether both are useful.
- Which online providers and plans are affordable and available to the user.
- Whether a provider exposes reliable model metadata and tool calling.
- Whether PostgreSQL is needed before multi-machine workers exist.
- Which Windows sandbox configuration provides acceptable isolation on this machine.
- Exact dependency versions and supported Python/Node versions.
- Which task classes may run unattended and their budgets.

## 11. Related documents

- [System Architecture](system-architecture.md)
- [Architecture Decisions](decisions.md)
- [Autonomy Policy](../governance/autonomy-policy.md)
- [Security and Provenance](../governance/security-and-provenance.md)
- [Verification Strategy](../quality/verification-strategy.md)
- [Roadmap](../planning/roadmap.md)
- [Initial Backlog](../planning/initial-backlog.md)
