# Stack selection

Every language, framework, database, and service is chosen through `/investigate` and recorded as an ADR. Choose the option that best fits this problem, not the one with the most buzz this month.

## 1. Constraints first

Write these down before naming any technology: budget (build and run), team skills, deadline, expected load, data sensitivity and compliance, hosting limits, project lifetime.

## 2. Hard gates

Any failure eliminates the option.

- Stable release (≥ 1.0 or the ecosystem's equivalent) and a release in the last 12 months
- A published security policy and advisory process
- A licence compatible with the project
- Not end-of-life within the project's lifetime (check endoflife.date)
- No unpatched critical CVE in the version you would use

## 3. Weighted score

The default weights are below. A project may change them only if the research doc says why.

| Criterion | Weight | Evidence |
|---|---|---|
| Security | 25 | CVE history and fix speed (OSV.dev, NVD, GitHub Advisories), memory safety, supply-chain hygiene (OpenSSF Scorecard, signed releases), size of the transitive dependency tree |
| Delivery time | 20 | Team familiarity, ecosystem fit for the problem, tooling, docs quality |
| Budget | 20 | Hosting and runtime cost at expected load, licences, cost of hiring for it |
| Maturity & longevity | 20 | Age in production, backing (foundation/company/individual), bus factor, release cadence, breaking-change history |
| Fit | 15 | Performance profile, concurrency model, operability, observability |

Score each criterion 1–5 and back each score with a cited, dated source.

## 4. Anti-hype rules

- Less than 3 years in production use: needs explicit justification in the ADR.
- Spend at most one innovation token per project (McKinley, *Choose Boring Technology*). Everything else is boring and proven.
- Always include the boring baseline as a candidate. If it loses, write down why.
- Benchmarks count only if they match the project's workload. Vendor benchmarks don't count.
- Ask: what did this replace, and why will it still be here in 5 years?

## 5. Output

`docs/research/YYYY-MM-DD-<topic>.md` from `docs/templates/research.md`, then an ADR from `docs/templates/adr.md`.
