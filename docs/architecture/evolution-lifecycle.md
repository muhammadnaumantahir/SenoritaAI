# Continuous Evolution Lifecycle

Senorita should run this lifecycle on schedules and events without waiting for a user prompt.

1. Observe: health, errors, resource use, test failures, advisories and capability gaps.
2. Diagnose: identify likely causes and separate evidence from hypotheses.
3. Propose: create candidates with value, confidence, risk, cost and reversibility.
4. Prioritise: rank work while protecting security and reliability tasks from starvation.
5. Research: inspect internal code and trustworthy external sources.
6. Design: define contracts, acceptance criteria, migration and rollback plans.
7. Acquire or build: absorb permitted source/components, learn techniques, or implement original code.
8. Experiment: work in isolated, resource-bounded environments.
9. Verify: run builds, tests, security/licence checks and benchmarks.
10. Decide: policy permits, rejects or holds the change.
11. Release: deploy through a reversible strategy.
12. Monitor: compare production health with baseline.
13. Learn: record outcomes and update knowledge and future priorities.

## Triggers
- Event-driven: crashes, failing tests, advisories, dependency events and resource thresholds.
- Periodic: health reviews, dependency reviews, architecture drift and repository discovery.

## Loop protection
Use task deduplication, cooldowns, retry ceilings, budgets and circuit breakers. Repeated failure must quarantine a candidate rather than create an endless retry loop.

## Completion
A task is complete only when acceptance criteria pass, evidence is stored, documentation is updated, the release is healthy and rollback remains available. A generated patch alone is not completion.
