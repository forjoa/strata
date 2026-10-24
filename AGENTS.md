# Strata

Engineering first, AI second. These rules are non-negotiable. Rationale and detail live in `docs/engineering/`.

## Order of work

No code exists before its reason does. Drive these steps yourself by invoking the matching skill; the user never has to type the commands. Skills live in `.claude/skills/` (Codex reads them through the `.agents/skills` symlink): `/investigate` in Claude Code is `$investigate` in Codex.

1. **Investigate** `/investigate` → evidence-based comparison in `docs/research/`
2. **Decide** `/decide` → ADR in `docs/decisions/`
3. **Design** `/design` → diagrams and module contracts in `docs/architecture/`
4. **Specify** `/feature` → use case, sequence, test list in `docs/features/`
5. **Test** → failing tests written from the spec
6. **Implement** → the least code that makes them pass
7. **Reconcile** → docs and diagrams match the code, in the same change

Trivial changes (typo, rename, patch bump) may skip to step 5.

## Investigation

- Never choose a technology because it is new, viral, or familiar to you. Choose it because the evidence wins.
- Score every option on security, budget, delivery time, maturity, and fit: `docs/engineering/stack-selection.md`.
- Cite sources with dates (OSV.dev, NVD, GitHub Advisories, OpenSSF Scorecard, endoflife.date, official docs).
- Never invent versions, CVE counts, benchmarks, or prices. Unverified means labelled unverified.

## Architecture

Modular monolith, ready to split: `docs/engineering/architecture.md`.

- One module = one bounded context. It owns its data; no other module touches its tables.
- Modules talk only through their `contract/` or domain events. Never import another module's internals.
- Stateless: nothing survives a request in memory. State lives in stores.
- Dependencies point inward: `adapters → application → domain`. Domain has no framework and no I/O.
- An architecture test enforces boundaries. Convention alone is not enforcement.

## Code

- The least code that fully solves the problem. Delete before adding. No speculative abstraction, options, or "for later".
- Names say what. Comments only say a non-obvious why. No commented-out code. No TODO without an issue link.
- Validate at trust boundaries, parse into types, then trust the types.
- Errors are handled or propagated explicitly. Never swallowed.
- Idiomatic style for the language, enforced by the formatter and linter named in the stack ADR.
- New dependency only after checking maintenance, licence, vulnerabilities, and transitive size. A few lines beat a package.

## Tests

`docs/engineering/testing.md`

- Every behaviour change ships with unit tests built from realistic domain data, edge cases, and failure paths. No trivial tests.
- Test behaviour through public APIs. Fake at ports; never mock what you own.
- Deterministic: injected clock, seeded randomness, no network in unit tests. A flaky test is a bug.
- The quality bar is mutation score, not line coverage.
- Every bug fix starts with a test that reproduces it.

## Documentation

- Everything lives in Markdown under `docs/`. Every diagram is Mermaid: `docs/engineering/diagrams.md`.
- Every module has a `README.md` built from `docs/templates/module.md`.
- Doc drift is a bug: any change to behaviour, data, or boundaries updates its docs in the same change.

## Security

`docs/engineering/security.md`

- No secrets in code, logs, docs, or tests. Config comes from the environment.
- Deny by default. Least privilege for users, DB roles (RLS), tokens, and CI.
- Dependency, secret, and static scans run in CI and must pass.

## CI

Every project MUST get a CI pipeline once the stack ADR is accepted. Until then, run the same stages locally before finishing.

Stages, in order, all blocking: format check → lint → build → unit tests → architecture test → integration tests → mutation score → dependency scan (osv-scanner) → secret scan (gitleaks) → static analysis (Semgrep/CodeQL) → SBOM. The tools come from the stack ADR.

## Commits

- Format, one line, nothing else: `type(scope): message`
- Types: `feat` `fix` `refactor` `perf` `test` `docs` `build` `ci` `chore` `style` `revert`
- Scope is the module or area. Message is imperative, lowercase, no trailing period.
- No body, no trailers, no `Co-Authored-By`, no AI attribution of any kind, in commits or PRs.

## GitHub

- The `gh` CLI is authenticated. Use it freely for repos, issues, PRs, releases, Actions runs, and API calls.

## Working here

- If an ambiguity changes the design, ask. Otherwise decide and state the assumption.
- Before finishing: run tests, linters, and the architecture test, then launch the `reviewer` agent yourself on any non-trivial change (`.claude/agents/reviewer.md`; Codex uses the generated `.codex/agents/reviewer.toml`).
- Say what you did not verify.
