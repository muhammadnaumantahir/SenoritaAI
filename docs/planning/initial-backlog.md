# Initial Backlog

| ID | Priority | Work item | Acceptance evidence |
|---|---|---|---|
| SPS-001 | P0 | Audit target environment and repository | Baseline report |
| SPS-002 | P0 | Define architecture/module inventory | Versioned inventory |
| SPS-003 | P0 | Define permissions and data classification | Policy matrix |
| SPS-004 | P0 | Implement supervisor skeleton | Startup, health and stop tests |
| SPS-005 | P0 | Implement durable state and event log | Restart/replay tests |
| SPS-006 | P0 | Implement isolated worker execution | Sandbox boundary tests |
| SPS-007 | P0 | Implement snapshots and rollback | Successful rollback drill |
| SPS-008 | P0 | Audit FreeLLMAPI and OmniRoute | Endpoint, auth, capabilities, limits, security and licence report |
| SPS-009 | P0 | Define internal Model Gateway contract | Contract tests independent of provider |
| SPS-010 | P0 | Implement provider registry and model catalogue | Provider configuration and capability tests |
| SPS-011 | P0 | Implement routing policy, budgets and usage audit | Routing, privacy, quota and budget tests |
| SPS-012 | P1 | Implement verified online provider adapters | At least two independent routes tested, if available |
| SPS-013 | P2 | Implement optional Ollama adapter | Local provider can be enabled/disabled without agent changes |
| SPS-014 | P1 | Implement capability registry | Registry/API tests |
| SPS-015 | P1 | Implement observation engine | Telemetry/fault-injection tests |
| SPS-016 | P1 | Implement evolution planner | Scoring and deduplication tests |
| SPS-017 | P1 | Implement coding worker | Isolated patch-generation test |
| SPS-018 | P1 | Implement verification pipeline | Reproducible build/test evidence |
| SPS-019 | P1 | Implement controlled release manager | Canary/rollback demonstration |
| SPS-020 | P1 | Implement repository research | Evidence-based candidate report |
| SPS-021 | P1 | Implement licence/provenance pipeline | SBOM and provenance output |
| SPS-022 | P1 | Implement absorption workflow | Verified component adoption |
| SPS-023 | P2 | Implement agent factory | Agent contract/permission tests |
| SPS-024 | P2 | Implement unified workspace | Health, queue, audit, provider usage and release views |
| SPS-025 | P2 | Run long-duration autonomy test | Soak and recovery report |

Update this backlog, architecture, tests and changelog with every implementation change. Never mark work complete without acceptance evidence.
