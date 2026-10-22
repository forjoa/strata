---
name: decide
description: Record an architecture or technology decision as an ADR. Use after /investigate, or for any decision that is costly to reverse.
---

1. Find the next number in `docs/decisions/`.
2. Write `docs/decisions/NNNN-<kebab-title>.md` from `docs/templates/adr.md`. Link the research doc if one exists.
3. If it replaces an earlier ADR, set the old one's status to `superseded by NNNN`. Never delete ADRs.
4. For a stack ADR, also fix: formatter, linter, test runner, mutation tool, architecture-test tool, test placement, CI platform, and the tool for each CI stage listed in `CLAUDE.md`.
5. Show the ADR to the user. Status stays `proposed` until they accept it.
