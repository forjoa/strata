---
name: design
description: Produce or update the system design (context, bounded contexts, data model with RLS, threats, deployment) and scaffold module folders. Use after the stack ADR is accepted, or when boundaries or data change.
---

Follow `docs/engineering/architecture.md` and `docs/engineering/diagrams.md`.

1. Read `docs/product/` and the accepted ADRs.
2. Find bounded contexts: group use cases by ubiquitous language and by which data must change together. Prefer fewer, cohesive modules. Merge any module that has no data of its own.
3. Write or update `docs/architecture/context.md`, `modules.md`, `data.md` (ER + RLS + classification), `threats.md`, and `deployment.md`.
4. For each module, create `src/modules/<context>/` with the layer folders and a `README.md` from `docs/templates/module.md`.
5. Add or update the architecture test so it encodes the module boundaries.
6. Summarise the trade-offs for the user. Record significant ones with `/decide`.
