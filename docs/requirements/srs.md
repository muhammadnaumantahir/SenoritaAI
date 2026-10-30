# Software Requirements Specification

These are target requirements, not claims that features are already implemented.

## Functional requirements

| ID | Priority | Requirement |
|---|---|---|
| SPS-F-001 | P0 | Maintain versioned module, dependency and capability inventories. |
| SPS-F-002 | P0 | Persist evolution tasks, decisions, evidence and execution state. |
| SPS-F-003 | P0 | Run a trusted supervisor independently of evolutionary modules. |
| SPS-F-004 | P0 | Execute development in isolated workspaces with bounded permissions. |
| SPS-F-005 | P0 | Enforce policy for filesystem, network, secrets, data and deployment access. |
| SPS-F-006 | P0 | Record auditable autonomous actions and releases. |
| SPS-F-007 | P0 | Support snapshots, known-good releases and tested rollback. |
| SPS-F-008 | P1 | Observe health, errors, resources and capability gaps. |
| SPS-F-009 | P1 | Generate and prioritise improvements without prompts. |
| SPS-F-010 | P1 | Discover and evaluate repositories and packages. |
| SPS-F-011 | P1 | Support source, component and knowledge absorption. |
| SPS-F-012 | P1 | Generate or modify code, tests, agents and documentation. |
| SPS-F-013 | P1 | Run reproducible build, test, security, licence and performance gates. |
| SPS-F-014 | P1 | Release eligible changes and monitor health. |
| SPS-F-015 | P1 | Quarantine or roll back unhealthy releases. |
| SPS-F-016 | P1 | Resume interrupted jobs safely after restart. |

## Non-functional requirements
Reliability, least-privilege security, recoverability, reproducible builds, observability, resource efficiency, provider neutrality, maintainability, privacy and compatibility.

## Verification status
Use planned, in_progress, implemented, tested, verified, operational, deferred and blocked. Code existing is not sufficient evidence for verified or operational. Every requirement must map to implementation, automated tests and runtime evidence.
