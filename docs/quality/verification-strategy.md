# Verification Strategy

## Verification layers
1. Static checks: format, lint, type, secrets, licence and static security scans.
2. Unit and contract tests.
3. Integration tests for storage, queues, model gateway, filesystem and workers.
4. End-to-end evolution-cycle tests.
5. Security tests for sandbox boundaries, permissions and prompt injection.
6. Performance tests for latency, CPU, memory, disk and inference cost.
7. Reliability drills for crashes, restarts, outages, corrupted candidates and rollback.
8. Long-duration soak tests for leaks, repeated loops and queue growth.

## Independent verification
The agent creating a change must not be the sole authority deciding it is correct. Use deterministic tests and separate verification for high-risk changes.

## Release gates
Requirements and acceptance criteria must be explicit; builds reproducible; required tests passing; security and licence checks clean; no prohibited secrets; compatibility and migrations checked; resource budgets respected; provenance/audit complete; rollback prepared.

## Status definitions
- implemented: code exists.
- tested: specified tests ran.
- verified: required evidence and release gates passed.
- operational: healthy behaviour demonstrated in the target runtime.
