# Historical Command Architecture Research

**Status:** ACTIVE  
**Source projects:** `redhataccess/command`, `redhataccess/command-lang`, `redhataccess/pipeline`

## Purpose

Recover architectural ideas from the historical command-family projects created by Scot Floess and evaluate which ideas should influence modern FlossWare architecture, especially Loom.

This is research, not a port. We will preserve useful semantics while rejecting historical constraints that no longer make sense.

## Architectural lineage

```text
redhataccess/command
        │
        ▼
  command model
        │
        ▼
redhataccess/command-lang
        │
        ▼
 language representation
        │
        ▼
redhataccess/pipeline
        │
        ├── definitions
        ├── contexts
        ├── pipelines
        ├── steps
        ├── executors
        └── intermediate representation
```

## Research questions

1. What is the minimal command abstraction?
2. How are commands composed?
3. What is the relationship between a command and its input/output objects?
4. How does `command-lang` represent or translate commands?
5. How do definitions separate representation from instantiation?
6. How are global, pipeline, and step contexts scoped and propagated?
7. How are pipelines and steps represented and executed?
8. What responsibilities belong to executors?
9. What does the intermediate representation buy us?
10. How are filtering, selection, transformation, and validation represented?
11. Which concepts are deterministic data operations versus execution/reasoning operations?
12. Which ideas map cleanly to a Loom intermediate representation?
13. Which historical choices should explicitly not be carried forward?

## Loom comparison hypothesis

The historical architecture may suggest a separation such as:

```text
operation model → representation/language → execution
```

Loom may eventually need a related separation:

```text
goals / data / operations → Loom IR → planner/executor
                                      │
                                      ├── deterministic operations
                                      └── reasoning operations
```

This is a hypothesis, not a decision.

## Investigation plan

- [ ] Inventory the public API and type hierarchy in `command`.
- [ ] Inventory language/front-end abstractions in `command-lang`.
- [ ] Trace definitions from source representation to instantiated objects in `pipeline`.
- [ ] Trace context creation, scope, mutation, and propagation.
- [ ] Trace pipeline and step execution through executors.
- [ ] Identify object/data transformations and any filtering primitives.
- [ ] Identify composition and chaining semantics.
- [ ] Identify extension points and plugin patterns.
- [ ] Evaluate concurrency, error, and lifecycle semantics.
- [ ] Compare the historical IR with candidate Loom IRs.
- [ ] Record reusable patterns and anti-patterns.
- [ ] Produce a Loom implications document.

## Deliverables

- `command-model.md`
- `language-and-representation.md`
- `context-and-dataflow.md`
- `pipeline-execution.md`
- `loom-implications.md`

## Guardrail

Do not finalize the Loom DSL, object/data semantics, or backtracking model based on this research until the three source projects have been reviewed as a coherent system.
