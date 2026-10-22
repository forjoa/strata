# Security

## Per project

- Threat model: STRIDE in `docs/architecture/threats.md`, updated when boundaries or data change.
- Verification target: an OWASP ASVS level (L1 public app, L2 anything with personal or financial data, L3 critical), chosen in an ADR.
- Data classification: every table or field holding PII or secrets is marked in `docs/architecture/data.md`.

## Rules

**Access**
- Deny by default. Authorization is checked in the application layer and again in the database with RLS (or equivalent) as defense in depth.
- Every query is tenant-scoped wherever there is multi-tenancy.
- Service accounts, DB roles, and CI tokens get the least privilege they need. Never use a superuser at runtime.

**Input and output**
- Validate and parse at every trust boundary: HTTP, queues, files, env, third-party responses.
- Use parameterized queries only. Encode output for its context.
- Set size limits on payloads, uploads, and pagination.

**Secrets**
- Secrets come from the environment or a secrets manager. Never from the repo, logs, error messages, or test fixtures.
- Commit `.env.example`, never `.env`.

**Supply chain**
- Commit lockfiles and pin versions. Automate updates with Renovate or Dependabot.
- CI gates: dependency vulnerabilities (osv-scanner), secrets (gitleaks), static analysis (Semgrep or CodeQL), SBOM (syft, CycloneDX).

**Runtime**
- Use structured logs without PII or tokens. Log security events: auth failures, permission denials, admin actions.
- TLS in transit, encryption at rest for sensitive data.
- Rate-limit authentication and expensive endpoints.
