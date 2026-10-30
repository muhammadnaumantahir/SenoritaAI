# Senorita SPS

**Self-Programming Software — Foundation v0.3.0**

Senorita is envisioned as a continuously operating, self-programming software ecosystem. It should understand its own architecture, observe its health, discover capability gaps, research the software ecosystem, absorb legally reusable code and components, independently implement useful techniques, test improvements, and evolve without requiring a user prompt for every task.

It is not merely an integration dashboard or a collection of separately operated applications. Integrations may be temporary bridges; the long-term goal is a coherent system with native capabilities.

## Evolution loop
Observe → Diagnose → Discover → Plan → Absorb or Build → Test → Verify → Release → Monitor → Learn → Repeat.

## Architecture
- Trusted Foundation: bootstrap, supervisor, policy, durable state, audit and recovery.
- Core Intelligence: reasoning, planning, knowledge and capability registry.
- Model Gateway: provider-independent inference routing, capability-aware model selection, budgets, privacy controls and usage audit.
- Evolution System: observation, research, absorption, coding, agent factory and verification.
- Release and Learning: staged deployment, monitoring, rollback and learning.
- Unified Workspace: health, capabilities, provider/model configuration, evolution history, approvals and resource use.

## AI deployment strategy
**Online-first, provider-independent, local-model optional.** Senorita's control plane and agent orchestration are independent of model vendors. Agents use Senorita's internal Model Gateway rather than calling provider SDKs directly. Online gateways/providers can be configured; local inference (for example, Ollama) is an optional adapter and is not required to run the application.

FreeLLMAPI and OmniRoute are candidates for integration and must be audited before adoption. No gateway is assumed to be compatible or unlimited. Provider costs, quotas, data handling and availability remain explicit operational constraints.

## Safety principle
Senorita may autonomously release pre-authorised low-risk improvements. It must not silently disable its policy controls, audit trail or recovery mechanism. Generated and absorbed code is untrusted until independently verified.

## Documentation
- [Vision](docs/product/vision-and-charter.md)
- [Architecture](docs/architecture/system-architecture.md)
- [Technology selection](docs/architecture/technology-selection.md)
- [Architecture decisions](docs/architecture/decisions.md)
- [Evolution lifecycle](docs/architecture/evolution-lifecycle.md)
- [Absorption engine](docs/architecture/absorption-engine.md)
- [Self-modification and recovery](docs/architecture/self-modification-and-recovery.md)
- [Requirements](docs/requirements/srs.md)
- [Autonomy policy](docs/governance/autonomy-policy.md)
- [Security and provenance](docs/governance/security-and-provenance.md)
- [Verification](docs/quality/verification-strategy.md)
- [Roadmap](docs/planning/roadmap.md)
- [Initial backlog](docs/planning/initial-backlog.md)

## Status
This repository contains the product and architecture foundation only. It does not claim these autonomous capabilities are already implemented.

## Licence
No project licence has been granted yet. Unless a licence is added, all rights are reserved; public visibility does not grant permission to reuse this repository's code.
