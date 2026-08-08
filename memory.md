Store knowledge communicated by a human that AI agents should remember across sessions in `MEMORY.md` files:

- `MEMORY.md` => global memory that applies to the whole repository
- `some-dir/` => `some-dir/MEMORY.md` => applies only to the directory
- `some-file.ext` => `some-file.MEMORY.md` => applies only to the file

Agents should consult all applicable `MEMORY.md` files when reading or modifying code.


## Goal

A `MEMORY.md` captures knowledge that was communicated to an AI agent and is useful for future sessions.

It contains durable, important, and unique knowledge that would otherwise need to be repeatedly communicated.

The AI agent decides what knowledge is worth remembering, but the knowledge itself must come from communication with a human. The agent may summarize, reorganize, and clarify it, but should not add knowledge based solely on its own discoveries, reasoning, code inspection, or research.

**Litmus test:** knowledge belongs to `MEMORY.md` if a fresh AI session should know it, it isn't available on the internet or by reading the code, and it was communicated by a human.


## Content

- Durable knowledge, not temporary context — stable enough to remain useful over time
- Likely to be useful across *many* agent sessions
- Important for making correct decisions
- Only unique knowledge: skip anything that can be found on the internet
- Skip anything that can be inferred by reading the code
- Don't turn memory into a diary or session log
- Keep it small and high-signal — every sentence should earn its place

Examples:

- Business context
- Business constraints not defined anywhere else
- Unique domain knowledge
- Important decisions (and their rationale if available)
- Things that were tried but deliberately rejected
- Non-obvious gotchas

Skip:

- Knowledge discovered by the agent itself
- Knowledge inferred from reading the code
- Temporary task context
- TODO lists
- Facts likely to become obsolete
- Session logs, changelogs, and historical records
- Step-by-step descriptions of recent work
- Generic programming knowledge
- Secrets, credentials, or personal data
- Anything already defined somewhere else
  - Build/CI instructions already defined in repository documentation
  - Global preferences (style, tone, tooling) already defined in agent configuration
  - Anything a linter, type checker, or test already enforces


## File format

```md
## TLDR [optional]

List of one-sentence succinct summary of each item listed below.

## Decisions [optional]

List of important decisions that were communicated by a human (and their rationale if available).

## Knowledge [optional]

List of important and unique knowledge communicated to the agent.

## Before modifying this file

Read this file's format at https://raw.githubusercontent.com/brillout/ai-memory/refs/heads/main/memory.md
```

Notes:

- The `## ... [optional]` sections are optional; create other sections when useful
- Consider using graphics (e.g. `mermaid` code blocks) whenever helpful


## Maintenance

Unmaintained memory is worse than none — a wrong entry costs more than an absent one.

- **Delete obsolete knowledge:** when an entry turns out false (e.g. contridicts more recent knowledge), remove it; don't append corrections (no history)
- **DRY — one entry, one place:** duplicated memory drifts apart and makes both copies unreliable


## Installation

If the repository hasn't any `MEMORY.md` yet, then create `MEMORY.md` at the repository root:

```
No memory yet.

AI agents should store knowledge communicated by humans that they should remember across sessions in `MEMORY.md` files.

## Before modifying this file

Read this file's format at https://raw.githubusercontent.com/brillout/ai-memory/refs/heads/main/memory.md
```

If the repository already has `MEMORY.md` then there is nothing to do. (Agents automatically see and maintain the `MEMORY.md` files.)
