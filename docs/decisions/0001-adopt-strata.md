# 0001. Adopt Strata

Date: 2026-10-22 · Status: accepted

## Context

AI agents write code fast and forget engineering just as fast. Every project needs the same baseline: evidence-based technology choices, clear boundaries, tests that catch real bugs, and docs that match the code.

## Decision

We will build every project on Strata:

- Modular monolith with bounded-context modules, hexagonal layers, and an architecture test
- Every technology choice comes from a scored investigation and is recorded as an ADR
- All documentation in Markdown, all diagrams in Mermaid
- Realistic unit tests gated by mutation score
- `CLAUDE.md` holds the rules, `docs/engineering/` the rationale, `.claude/skills/` the procedures

## Alternatives

- **Microservices from day one**: we pay the cost of distribution before knowing where the boundaries really are.
- **Unstructured monolith**: boundaries erode and later extraction becomes a rewrite.
- **Rules-only CLAUDE.md**: no procedures and no enforcement, so rules decay.

## Consequences

The first days of every project go to research and design instead of code. Boundaries cost some upfront indirection. Docs must be updated with every change.
