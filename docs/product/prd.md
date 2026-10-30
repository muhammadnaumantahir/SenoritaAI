# Product Requirements Document

## Outcome
A unified, continuously operating SPS platform that autonomously improves its capabilities under bounded governance.

## Operating modes
- Bootstrap: install, configure policies and establish trusted foundation.
- Autonomous operation: observe, plan, research, develop, test, release and learn.
- Supervised operation: continue safe work while holding high-impact changes.
- Safe mode: stop evolution while preserving diagnostics and recovery.
- Recovery: restore a known-good release and resume durable work.
- Inference-degraded mode: continue local control-plane functions while pausing, queuing or rerouting tasks affected by unavailable inference providers.

## Required capabilities
- Self-understanding: map modules, APIs, dependencies, tests, data flows and permissions.
- Autonomous planning: create and prioritise improvements from telemetry, failures, debt and capability gaps.
- Research and absorption: evaluate repositories, licences, security and compatibility.
- Self-programming: create and modify code, tests, agents and documentation in isolated workspaces.
- Verification and release: run deterministic gates, stage deployments and roll back failures.
- Unified workspace: expose health, capabilities, evolution history, approvals and resource usage.
- Provider-independent inference: use a Senorita-owned Model Gateway with configurable online providers and optional local inference.
- Capability-aware model selection: route by task requirements, data policy, configured budget, latency and provider health.
- Privacy and cost controls: enforce data classification, provider eligibility, token/spend budgets and usage audit.
- Durable operation: retain tasks and checkpoints across provider outages and application restarts.

## Initial exclusions
No unrestricted host administrator access, unbounded cloud spending, automatic changes to legal/privacy commitments, blind copying of unlicensed code, or self-removal of the trusted recovery supervisor. No mandatory GPU or mandatory local LLM. No assumption that a free online model/provider will remain available or offer unlimited quotas.

## Acceptance outcomes
A safe improvement can complete without a prompt; failed candidates cannot corrupt the running release; adopted components have provenance; unhealthy releases roll back; interrupted jobs resume after restart; agents can switch eligible inference providers without code changes; local inference can be absent in online mode; and local-only tasks never leak to online providers.
