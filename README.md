# FlossWare Engineering Research

Cross-project engineering investigations, experiments, and architectural research for FlossWare.

## Purpose

This repository is where ideas are investigated **before** they become standards, architecture decisions, or implementation requirements.

Research may be incomplete, contradictory, or wrong. That is intentional.

## Lifecycle

```text
Question
  ↓
engineering-research
  ↓
Investigation / experiment
  ↓
Conclusion
  ├──→ axium           durable knowledge, research outcomes, and provenance
  ├──→ standards       normative FlossWare-wide rules
  ├──→ ADR             architectural decision
  └──→ project repo    implementation
```

## What belongs here

- Cross-project architectural research
- Evaluation of competing technologies or approaches
- Historical architecture archaeology
- Prototypes used to answer architectural questions
- Research into workflow, dataflow, object models, orchestration, DSLs, and similar foundations
- Questions that should **not yet** become standards or ADRs

## What does not belong here

- Normative FlossWare-wide rules: use `standards`
- Durable knowledge, research outcomes, and provenance: use `axium`
- Project implementation: use the relevant project repository
- Final architectural decisions: use an ADR in the relevant project/standards repository

## Status vocabulary

Use explicit status markers such as:

- `PARKED` - interesting and worth revisiting, but not currently active
- `ACTIVE` - currently being investigated
- `CONCLUDED` - investigation complete; outcome documented
- `PROMOTED` - conclusion has moved into Axium, Standards, an ADR, or implementation

## Principle

> Research is allowed to be wrong. Standards and accepted ADRs are normative.
