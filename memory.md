Store knowledge that AI agents should remember across sessions in `MEMORY.md` files:

* `MEMORY.md` => memory for the directory/project as a whole
* `some-dir/` => `some-dir/MEMORY.md`
* `some-file.ext` => `some-file.MEMORY.md`

# Goal

A `MEMORY.md` is the answer an AI agent gives itself when a future session asks: **"What do I need to remember about this?"**

It contains durable knowledge that is useful across agent sessions — things that would otherwise have to be rediscovered, re-learned, or repeatedly explained.

Litmus test: **if a fresh AI session would benefit from knowing this before working on the project, and the knowledge is not obvious from reading the code, it belongs in ****`MEMORY.md`****.**

* Memory is for **knowledge**, not a description of the codebase.
* Store things that are easy to forget but important to know.
* Prefer durable knowledge over temporary context.
* Do not document things the AI can trivially infer by reading the code.
* Do not turn memory into a diary or session log.
* Keep it concise: every sentence should earn its place.
* ELI5: simple terms, no jargon, assume the AI knows nothing about the project.

# Content

```md
One-sentence description of the knowledge this file contains.

## TLDR

- The most important things to remember
- ...

## Important

Knowledge that is particularly important when working on this area.

## Decisions

Important decisions that were made and their rationale.

## Gotchas

Things that are easy to get wrong or overlook.

## Before modifying this file

Read this file's format at https://raw.githubusercontent.com/brillout/sdd/refs/heads/main/memory.md
```

Notes:

* All `##` sections are optional.
* Keep memory **small and high-signal**.
* Prefer updating existing knowledge over accumulating new entries.
* Remove obsolete knowledge.
* Consider using graphics supported by GitHub (e.g. `mermaid` code blocks) whenever helpful.

# What gets a MEMORY.md

Store knowledge that is:

* Useful across multiple agent sessions
* Not obvious from the code
* Easy for an AI to forget or rediscover
* Important for making correct decisions
* Stable enough to remain useful
* Based on decisions, discoveries, conventions, constraints, or project-specific knowledge

Examples:

* Architectural decisions and their rationale
* Non-obvious project conventions
* Important constraints
* Domain-specific terminology
* Known pitfalls and their solutions
* Things that were tried and deliberately rejected
* Relationships between seemingly unrelated parts of the project
* User or project preferences that affect future work
* Important external knowledge that cannot be inferred from the repository

Skip:

* Information already obvious from the code
* Temporary task context
* TODO lists
* Session logs
* Step-by-step descriptions of recent work
* Generic programming knowledge
* Build/CI instructions that belong in repository documentation
* Duplicating `SPEC.md`
* Facts that are likely to become obsolete

# Memory vs. SPEC

The distinction is simple:

* `SPEC.md` answers: **"How does the software work?"**
* `MEMORY.md` answers: **"What should an AI remember when working on this software?"**

A `SPEC.md` describes the system's business logic.

A `MEMORY.md` describes knowledge that helps an AI reason about the system and make good decisions.

For example:

```text
SPEC.md:
"Users can cancel a subscription at any time. Cancellation takes effect
at the end of the current billing period."

MEMORY.md:
"Do not change cancellation to take effect immediately. This was
deliberately chosen because customers retain access until the end of
their paid period."
```

The first describes **how the product works**. The second preserves **knowledge that prevents an AI from accidentally changing it**.

# Hierarchy

The file structure can represent levels of knowledge => mirror it:

* Root `MEMORY.md` => knowledge relevant to the entire project.
* Deeper `MEMORY.md` files => knowledge specific to that subsystem.
* A `MEMORY.md` should only contain knowledge relevant to its scope.

Agents should consult the nearest applicable `MEMORY.md` files before modifying code.

# Principle

**Memory is not documentation for humans. It is persistent context for AI agents.**

The goal is not to explain everything.

The goal is to ensure that a future AI session **doesn't have to learn the same important lesson twice**.

