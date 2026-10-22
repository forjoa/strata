---
name: investigate
description: Evidence-based comparison of technologies (language, framework, database, service, library) before any choice. Use when starting a project or whenever a technology decision is needed.
---

Follow `docs/engineering/stack-selection.md` exactly.

1. Restate the decision in one sentence.
2. Gather constraints from `docs/product/vision.md` and the user. Ask for any that are missing and would change the outcome: budget, team skills, deadline, load, compliance, lifetime.
3. List at least three candidates, including the boring baseline.
4. Research every candidate with web search and official sources: CVE history (OSV.dev, NVD, GitHub Advisories), OpenSSF Scorecard, endoflife.date, release history, licence, pricing. Record the URL and access date for every claim. Never fill gaps from memory: write "unverified".
5. Apply the hard gates, then score the survivors with the weighted table.
6. Write `docs/research/YYYY-MM-DD-<topic>.md` from `docs/templates/research.md`.
7. Present the recommendation, the runner-up, and the key risks. Offer `/decide`.
