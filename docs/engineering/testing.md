# Testing

A test is valuable only if it would catch a real bug. If no realistic code change could make it fail, it is noise.

## Shape

| Level | Scope | Share | Notes |
|---|---|---|---|
| Unit | domain + application, ports faked | Most | Milliseconds each, no I/O |
| Integration | one adapter against the real dependency | Some | Real DB/broker in containers (e.g. Testcontainers) |
| Architecture | module boundaries, layer direction | One suite | Fails the build |
| End-to-end | critical user journeys only | Few | Smoke-level |

## Unit test rules

- Test behaviour through the public API of a use case or aggregate, not private functions.
- Fake ports (repositories, clocks, gateways) with in-memory implementations. Never mock types you own.
- Use realistic data: real-shaped names, amounts, dates, locales. Build it with test data builders, not copy-pasted literals.
- Structure each test as Arrange, Act, Assert. One behaviour per test. The name states the scenario and the outcome.
- Keep tests deterministic: inject the clock, seed randomness, never touch the network.

## What to cover

Use this as a checklist when writing the test list in a feature spec:

- Boundaries: zero, one, max, max+1, empty, null/absent, very large
- Text: unicode, emoji, RTL, whitespace, injection payloads
- Time: time zones, DST transitions, leap days, month ends, clock skew
- Money: rounding mode, currency mismatch, negative amounts, minor units
- Concurrency: double submit, lost update, ordering of events
- Idempotency: the same command or event delivered twice
- Authorization: wrong tenant, wrong role, missing permission
- Failure: dependency down, timeout, partial write, retry

## Example

Not this:

```
add(1, 1) == 2
```

This:

```
Feature: apply loyalty discount to invoice
- gold customer, 3 lines with mixed tax rates, net 1,249.99 EUR → 10% discount applied to net before tax, each line rounded half-even, net 1,124.99
- discount pushes a line below zero due to a prior credit → line clamped at 0, DiscountCapped event emitted
- invoice issued at local 2026-03-29T02:30 Europe/Madrid (nonexistent, DST gap) → rejected or shifted per documented rule, never silently stored
- same ApplyDiscount command delivered twice → applied once, second call returns the original result
- customer from another tenant → AccessDenied, invoice unchanged
```

## Quality bar

- Mutation testing on `domain` and `application`, with a minimum score of 80%. Tools: Stryker (JS/TS, C#, Scala), PIT (JVM), mutmut (Python), cargo-mutants (Rust), gremlins (Go).
- Use property-based tests for invariants (parsers, money, state machines): Hypothesis, fast-check, jqwik, proptest, rapid.
- Coverage is reported but never the goal.
