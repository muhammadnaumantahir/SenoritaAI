# Runtime and Reliability

## Operating model
Senorita is intended to run as a long-lived background system with a unified local/web workspace. Closing the workspace should not stop authorised background evolution.

## Runtime responsibilities
- Supervisor: lifecycle, scheduling, health, policy and recovery.
- API/UI: visibility and user controls.
- Durable store: tasks, events, decisions, memory and release metadata.
- Worker pool: isolated research, coding, build and test jobs.
- Model gateway: local/external model routing under data and cost policies.
- Artifact store: source snapshots, builds, test evidence and backups.

## Reliability practices
Durable queues, checkpoints, idempotent jobs, health checks, bounded retries, circuit breakers, disk monitoring, resource budgets, graceful restart, verified backups and provider timeouts.

## Dependency reality
Continuous autonomy still depends on power, hardware, storage, operating-system health, network where required, model availability and external services. Local fallback paths can reduce but not eliminate these dependencies.

## Known target hardware
The currently known PC has 16 GB RAM, a 7th-generation i7 and Intel HD 620 graphics. It can support a lightweight control plane, but should not be assumed to run large coding models or many concurrent agents. Benchmark before selecting inference architecture.

## Metrics
Track uptime, crash loops, queue age, task success, verification failures, rollback rate, resource consumption, model latency, security findings and recovery time.
