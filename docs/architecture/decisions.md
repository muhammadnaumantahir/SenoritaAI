# Architecture Decisions

## ADR-001 — SPS, not an integration dashboard
Senorita's primary identity is a self-programming software ecosystem. Integrations are optional bridges, not the architectural centre.

## ADR-002 — Absorption and evolution are first-class
Absorption and Evolution are core subsystems because Senorita must discover, understand, adapt, build, verify and maintain capabilities.

## ADR-003 — Stable supervisor plus evolutionary modules
Keep a small trusted recovery/policy foundation separate from modules that can evolve.

## ADR-004 — Modular monolith first
Begin with clear module boundaries and isolated workers. Avoid premature microservices.

## ADR-005 — Local-first, provider-neutral intelligence
Design model interfaces so local and external models can be switched under policy and budget controls.

## ADR-006 — Evidence-based release
No generated or absorbed code reaches production without verification and rollback evidence.

## ADR-007 — Provenance is mandatory
Track origin, version, licence, notices and modifications for every absorbed component.

## Open decisions
- Runtime/language and repository implementation layout.
- Initial local model and minimum inference hardware.
- Worker isolation technology on Windows.
- Persistent database and event-log design.
- UI framework and local network exposure.
- Backup destination, retention and encryption.
- Which release classes may be fully automatic initially.
