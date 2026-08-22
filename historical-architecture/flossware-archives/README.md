# FlossWare Archives: Engineering History and Research Corpus

**Status:** ACTIVE

The `FlossWare-Archives` organization contains historical FlossWare projects. This document establishes the archive as a source for autonomous engineering understanding and research.

## Purpose

The goal is not to retrofit historical projects into current systems. The goal is to understand the engineering ideas, experiments, architectures, algorithms, languages, systems work, and design instincts represented by the archive.

The archive has **56 repositories**, including projects that are purely historical and projects that may be candidates for future resurrection, such as `tftp-os`.

## Research approach

Review the archive as a corpus rather than as 56 isolated repositories.

For each project, investigate as appropriate:

- Original purpose and engineering intent
- Architectural structure and important abstractions
- Algorithms and data structures
- Language, DSL, parser, and compiler work
- Object and data models
- Command, pipeline, and execution models
- Systems, OS, boot, filesystem, and networking work
- Automation and build/deployment approaches
- Particularly elegant or technically ambitious work
- Ideas that were ahead of their time
- Approaches that should remain historical
- Relationships and dependencies between projects
- Potential resurrection candidates
- Concepts that are useful independent research material

## Classification

Historical understanding and future intent must remain separate.

- **HISTORICAL**: primarily valuable for understanding prior engineering work
- **RESEARCH**: contains an idea worth investigating independently
- **RESURRECT**: a dormant project that may be intentionally revisited
- **ACTIVE**: currently being pursued

A repository can have more than one research finding without changing its historical status.

## Research principles

1. Do not judge a project solely by its age or current technology.
2. Recover the engineering intent before evaluating implementation details.
3. Preserve useful ideas even when the original implementation should not be reused.
4. Do not assume historical designs should influence Loom or any other current project.
5. Promote findings only when evidence supports them.
6. Record uncertainty rather than filling gaps with guesses.

## Relationship to other repositories

- `FlossWare-Archives`: source material
- `FlossWare/engineering-research`: analysis, research findings, and cross-project synthesis
- `FlossWare/knowledge`: stable technical knowledge after research has settled
- `FlossWare/engineering-standards`: normative engineering practices
- Current project repositories: implementation

## Current known resurrection candidate

### `tftp-os`

` tftp-os` has been explicitly identified as a project of interest for potential future pursuit. It should receive deeper investigation than a purely historical archive entry once its repository contents are accessible.

## Command/language/pipeline lineage

The historical `redhataccess/command`, `redhataccess/command-lang`, and `redhataccess/pipeline` repositories are related research material and should be studied alongside relevant FlossWare archive projects, particularly for command composition, language representation, contexts, pipelines, execution, and intermediate representations.

## jplate

`jplate` is the user's first open-source project and contains notable JavaCC work. The JavaCC implementation is preserved as historical evidence of language/grammar engineering and should be understood on its own terms rather than treated as a prescription for current projects.

## Autonomous research policy

As the archive is investigated, genuinely useful findings may be added to this research repository without requiring a separate approval step for each individual note. Changes to the historical repositories themselves require explicit authorization.

Research notes should favor architectural understanding over superficial summaries.
