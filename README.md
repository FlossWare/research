# research

**Cross-project engineering research for FlossWare.**

This repository holds investigations and experiments **before** they become standards, architecture decisions, or implementation requirements. Research may be incomplete, contradictory, or wrong. That is intentional.

## Lifecycle

```text
Question
  |
  v
research
  |
  v
Investigation / experiment
  |
  v
Conclusion
  +--> knowledge          reusable knowledge capability
  +--> standards          normative engineering practice
  +--> ADR                architectural decision
  +--> project repository implementation
```

## What belongs here

- Cross-project architectural research
- Evaluation of competing technologies or approaches
- Historical architecture archaeology
- Prototypes used to answer architectural questions
- Research into workflow, dataflow, object models, orchestration, DSLs, and similar foundations
- Questions that should not yet become standards or ADRs

## What does not belong here

- Normative engineering rules: use `standards`.
- Stable, reusable knowledge software: use `knowledge`; keep private authoring material in `kbase`.
- Project implementation: use the relevant project repository.
- Final architectural decisions: record an ADR in the relevant project or `standards` repository.

## Status vocabulary

- `PARKED`: worth revisiting, but not currently active
- `ACTIVE`: currently being investigated
- `CONCLUDED`: investigation complete; outcome documented
- `PROMOTED`: conclusion moved into standards, an ADR, knowledge, or implementation

## Principle

> Research is allowed to be wrong. Standards and ADRs are not.
