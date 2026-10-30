# Autonomy Policy

## Principle
No per-task prompt is needed for actions explicitly pre-authorised, low-risk, reversible and within configured limits. Uncertainty or missing permission must reduce autonomy rather than invite guessing.

## Autonomy levels
| Level | Scope |
|---|---|
| A0 Observe | Read-only monitoring and analysis |
| A1 Prepare | Research, proposals and isolated patch drafts |
| A2 Verify | Builds, tests and sandbox experiments |
| A3 Bounded release | Low-risk changes after all gates pass |
| A4 Controlled release | Core modules, schema and authentication changes |
| A5 Protected | Supervisor, policy, secrets and permission-boundary changes |

Start conservatively. Increase autonomy only after reliability evidence.

## Configure before unattended operation
Permitted filesystem roots, network rules, secret scopes, CPU/RAM/disk budgets, inference budgets, parallel jobs, deployment targets, release classes, backup policy, data classification and telemetry rules.

## Always restricted
No unbounded spending, destructive user-data operations, publication of secrets/private data, external permission changes, disabling audit/security/rollback, privilege expansion, unresolved-licence adoption or irreversible production actions without a verified recovery plan.

A held task must record why it is held while unrelated safe work continues. Provide an emergency stop for evolution that leaves monitoring, audit and recovery active.
