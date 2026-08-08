Store knowledge communicated by a human that AI agents should remember across sessions in `MEMORY.md` files:

- `MEMORY.md` => global memory that applies for the repository as a whole
- `some-dir/` => `some-dir/MEMORY.md` => applies only to the directory
- `some-file.ext` => `some-file.MEMORY.md` => applies only to the file

Agents should consult all applicable `MEMORY.md` files when reading or modifying code.


## Goal

A `MEMORY.md` captures knowledge that was communicated to an AI agent and is useful for future sessions.

It contains durable, important, and unique knowledge that would otherwise need to be repeatedly communicated.

The AI agent decides what knowledge is worth remembering, but the knowledge itself must come from communication with a human. The agent may summarize, reorganize, and clarify it, but should not add knowledge based solely on its own discoveries, reasoning, code inspection, or research.

**Litmus test:** knowledge belongs to `MEMORY.md` if a fresh AI session should know it, it isn't available on the internet or by reading the code, and it was communicated to the agent.


## Content

- Knowledge communicated to the agent, not a description of the codebase
- Durable knowledge, not temporary context
- Likely to be useful across *many* agent sessions
- Stable enough to remain useful over time
- Important for making correct decisions
- Only unique knowledge: skip anything that can be found on the internet
- Skip anything that can be inferred by reading the code
- Don't turn memory into a diary or session log
- Keep it small and high-signal — every sentence should earn its place
- ELI5: simple terms, avoid unnecessary jargon
- Delete obsolete knowledge: when an entry is no longer true, remove it instead of keeping historical corrections

Examples of knowledge communicated by:

- Business context
- Business constraints not defined anywhere
- Unique domain knowledge
- Important decisions (and their rationale if available)
- Things that were tried but deliberately rejected
- Non-obvious gotchas

Skip:

- Knowledge discovered by the agent itself
- Knowledge inferred from reading the code
- Temporary task context
- TODO lists
- Session logs
- Step-by-step descriptions of recent work
- Generic programming knowledge
- Facts likely to become obsolete
- Build/CI instructions that belong in repository documentation
- Anything a linter, type checker, or test already enforces
- Secrets, credentials, or personal data
- Global preferences (style, tone, tooling) if already defined in agent configuration
- Changelogs and historical records


## File format

```md
## TLDR [optional]

List of one-sentence succinct summary of each item listed below.

## Decisions [optional]

List of important decisions that were communicated by a human (and their rationale if available).

## Knowledge [optional]

List important and unique knowledge communicated to the agent.

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
