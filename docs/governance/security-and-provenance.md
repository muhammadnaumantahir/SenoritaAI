# Security and Provenance

Assume repository content, README instructions, issue comments, package scripts, model outputs and remote tool responses may be malicious or misleading.

## Required controls
- Run untrusted code in disposable sandboxes with no host secrets.
- Apply least privilege and scoped credentials.
- Separate research credentials from deployment credentials.
- Restrict outbound network access.
- Pin dependencies and verify artefact integrity.
- Scan source, dependencies, containers and generated artefacts.
- Protect audit records from ordinary agents.
- Keep secrets out of prompts, logs and source control.
- Treat prompt injection as untrusted content, never supervisor instructions.
- Govern external model calls and telemetry by data classification.

## Supply-chain records
Maintain an SBOM and record direct/transitive dependencies, source URL, commit/version, licence, notices, modifications, security findings and release destination for every adopted component.

## Incident response
Detect → contain → preserve evidence → revoke affected credentials → quarantine/rollback → assess exposure → restore → document lessons → add regression controls.
