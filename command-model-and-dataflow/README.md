# Command Model and Dataflow Research

**Status:** PARKED  
**Priority:** HIGH  
**Revisit:** Before finalizing the Loom workflow DSL and data/object semantics

## Context

Historical `redhat-access` command-family projects created by Scot Floess may contain architectural patterns relevant to the design of Loom's object, dataflow, filtering, transformation, and command-composition model.

This is architectural archaeology, not an attempt to revive the historical product. The goal is to recover useful concepts and determine which, if any, belong in modern FlossWare systems.

## Questions to investigate

- What constitutes a command?
- How are command inputs and outputs represented?
- How are objects passed between commands?
- How are filters and predicates expressed?
- How are objects transformed, selected, projected, or aggregated?
- Can commands compose or chain naturally?
- How does data flow between commands?
- What execution semantics exist?
- How are state and context propagated?
- Are results typed, structured, streamable, or lazy?
- How are failures and partial results represented?
- What concepts map naturally to a Loom intermediate representation?

## Loom relevance

Potential source of prior art for:

- Object model
- Dataflow
- Filters and predicates
- Transformations
- Command composition
- Execution graphs
- Workflow IR
- Deterministic data operations surrounding AI reasoning

## Current Loom hypothesis

Loom should distinguish deterministic data operations from reasoning operations.

```text
DATA → REASON → DATA → REASON → DATA
```

Potential deterministic primitives include:

```text
filter
map
select
project
join
group
sort
aggregate
validate
deduplicate
```

Potential reasoning primitives include:

```text
analyze
classify
infer
plan
decide
review
generate
```

The historical command-family architecture should be reviewed before these semantics are finalized.

## Related work

- `FlossWare/loom-ai` workflow model
- Loom object/data model research
- Future Loom DSL
- Future search/backtracking semantics
- `FlossWare/engineering-standards`
- `FlossWare/knowledge`

## Decision

Do **not** finalize the Loom DSL or its complete workflow/data semantics until this research has been revisited.

DSL design and backtracking remain intentionally parked until the underlying object/data model is better understood.

## Next investigation

When access to the historical `redhat-access` organization and command-family projects is available, review the family as a coherent architecture rather than performing isolated class-level code review.
