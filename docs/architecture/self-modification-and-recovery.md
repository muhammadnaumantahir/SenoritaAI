# Self-Modification and Recovery

## Bootstrap problem
A self-programming system must not rely entirely on code it is actively modifying. If its updater, policy enforcement or startup path breaks, an independent mechanism must still restore it.

## Trusted supervisor
The supervisor owns startup, integrity checks, policy enforcement, resource limits, release activation, health checks, rollback and safe-mode startup. Evolutionary agents cannot silently remove or bypass these controls.

## Change zones
- Low risk: documentation and isolated additive modules; automatic release may be allowed after all gates pass.
- Controlled: core modules, schemas, authentication and dependency changes; require stronger tests and staged rollout.
- Protected: supervisor, policy, secrets, audit integrity, permissions and recovery; require independent review and explicit approval.
- Forbidden: disabling audit/security/rollback, silently expanding privileges or destructive actions without authorised recovery.

## Safe update transaction
Prepare candidate → build immutable artefact → verify → snapshot current state → activate in staging/canary → health check → promote or rollback.

Never overwrite the only known-good installation in place. Preserve audit history across rollback. Test restore procedures and handle database migrations separately.

Senorita may evolve most of its body. It must not have unrestricted unilateral power to rewrite the mechanism that constrains and recovers it.
