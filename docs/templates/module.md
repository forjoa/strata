# Module: <context>

One sentence: the business capability this module owns.

## Ubiquitous language

| Term | Meaning |
|---|---|

## Contract

What other modules may call (`contract/`). Inputs, outputs, errors.

## Events

| Event | Version | Published when | Payload |
|---|---|---|---|

| Consumed event | From | Reaction |
|---|---|---|

## Data

Schema `<context>`. ER diagram + RLS table, following `docs/engineering/diagrams.md`.

## Lifecycle

`stateDiagram-v2` for each aggregate that has states.

## Invariants

Rules the domain must never break. Each one has a test.
