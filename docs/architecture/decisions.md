# Architecture Decisions

## ADR-001 — SPS, not an integration dashboard
Senorita's primary identity is a self-programming software ecosystem. Integrations are optional bridges, not the architectural centre.

## ADR-002 — Absorption and evolution are first-class
Absorption and Evolution are core subsystems because Senorita must discover, understand, adapt, build, verify and maintain capabilities.

## ADR-003 — Stable supervisor plus evolutionary modules
Keep a small trusted recovery/policy foundation separate from modules that can evolve.

## ADR-004 — Modular monolith first
Begin with clear module boundaries and isolated workers. Avoid premature microservices.

## ADR-005 — Online-first, provider-independent intelligence
The application control plane and agent orchestration run independently of model vendors. Online inference is the default; local inference is optional. Agents use Senorita's internal Model Gateway contract rather than calling provider SDKs directly. Provider routing, data policy, budgets, fallback and audit are controlled by Senorita. Local-only tasks must never silently fall back online.

## ADR-006 — Evidence-based release
No generated or absorbed code reaches production without verification and rollback evidence.

## ADR-007 — Provenance is mandatory
Track origin, version, licence, notices and modifications for every absorbed component.

## ADR-008 — Separate orchestration from inference
Senorita's supervisor, memory, planning, agent runtime, research workflow, coding orchestration and verification pipeline are application capabilities, not model-provider services. They must remain operable when a provider is unavailable, with inference-dependent tasks paused or routed to an eligible alternative. This keeps hardware requirements modest and prevents model/vendor lock-in.

## ADR-009 — Existing gateways are candidates, not assumptions
Evaluate FreeLLMAPI and OmniRoute against the provider-adapter contract before adoption. Do not add overlapping gateways or nested routing chains without measured need and tests. Ollama remains an optional local adapter.

## Open decisions
- Exact runtime/dependency versions after environment verification.
- Which of FreeLLMAPI and OmniRoute should be integrated first, based on actual API and feature audits.
- Which online providers are affordable, available and policy-compatible.
- Windows worker isolation configuration.
- Persistent database and event-log design beyond initial SQLite.
- UI framework and local network exposure.
- Backup destination, retention and encryption.
- Which release classes may be fully automatic initially.
- Exact unattended task and provider spending budgets.

See [Technology Selection](technology-selection.md) for the implementation baseline and acceptance criteria.
