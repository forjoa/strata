---
name: feature
description: Deliver a feature end to end - spec, failing tests, minimal implementation, reconciled docs. Use for any non-trivial behaviour change.
---

1. **Spec**: write `docs/features/<name>.md` from `docs/templates/feature.md`: use case, sequence diagram, data changes, a realistic test list, and security notes. Get the user's agreement on the test list before writing code.
2. **Test**: turn the test list into failing tests (`docs/engineering/testing.md`). Run them and confirm they fail for the right reason.
3. **Implement**: write the least code that makes them pass, respecting the layers and boundaries.
4. **Harden**: run mutation testing on the touched domain and application code. Add tests for surviving mutants that matter.
5. **Reconcile**: update the module README, `data.md`, `use-cases.md`, and `threats.md` wherever they changed.
6. **Verify**: run tests, linters, and the architecture test, then the `reviewer` agent. Report the results and anything left unverified.
