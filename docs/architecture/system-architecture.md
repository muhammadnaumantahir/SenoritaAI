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

## 3. Evolutionary System
- Observation Engine: runtime telemetry, errors, technical debt and capability gaps.
- Research Engine: repository, package, standards and technique analysis.
- Absorption Engine: provenance-aware source, component and knowledge acquisition.
- Coding Engine: code generation, refactoring, migration and test authoring.
- Agent Factory: creation and lifecycle management of scoped specialist agents.
- Verification Engine: independent quality, security and compatibility checks.
- Release and Learning Engine: staged deployment, monitoring, rollback and learning.

## 4. Unified Workspace
A single interface/API for system health, capabilities, evolution history, approvals, resource use and releases. The interface is not required for background evolution to continue.

## Communication rules
Use versioned contracts, durable asynchronous jobs, correlation IDs and explicit permissions. Treat repository content, model output and tool responses as untrusted data. Never execute untrusted code inside the supervisor context.

## Initial deployment strategy
Start as a modular monolith with strict internal interfaces and isolated workers. Split services only when security, reliability or scaling requires it. Avoid premature microservices.
