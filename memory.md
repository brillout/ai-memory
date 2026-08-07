Store knowledge that AI agents should remember across sessions in `MEMORY.md` files:

- `MEMORY.md` => global memory that applies for the repository as a whole
- `some-dir/` => `some-dir/MEMORY.md` => applies only to the directory
- `some-file.ext` => `some-file.MEMORY.md` => applies only to the file

Agents should consult all applicable `MEMORY.md` files when reading or modifying code.

# Goal

A `MEMORY.md` is the answer an AI agent gives itself when a future session asks: **"What do I need to remember about this?"**

It contains durable, important, and uncommon/unique knowledge that should be remembered across agent sessions — things that would otherwise have to be repeatedly explained.

Litmus test: **if a fresh AI session should know about it, and the knowledge isn't available from the internet or reading the code, it belongs in `MEMORY.md`.**

- Memory is for **knowledge**, not a description of the codebase
- Prefer durable knowledge over temporary context
- Only document uncommon/unique knowledge: skip anything that can be found on the internet
- Don't document things that can inferred by reading the code
- Do not turn memory into a diary or session log
- Keep it concise: every sentence should earn its place
- ELI5: simple terms, no jargon

# Content

```md
## TLDR [optional]

List of one-sentence succinct summary of each knowledge listed below.

## Decisions [optional]

Important decisions that were made (and their rationale if available).

## Knowledge [optional]

Important and uncommon/unique knowledge when working on this area.

## Gotchas [optional]

Things that are easy to get wrong.

## Before modifying this file

Read this file's format at https://raw.githubusercontent.com/brillout/ai-memory/refs/heads/main/memory.md
```

Notes:

- The `## ... [optional]` sections are optional, and feel free to create other sections
- Keep memory **small and high-signal**
- Prefer updating existing knowledge over accumulating new entries
- Remove obsolete knowledge
- Consider using graphics (e.g. `mermaid` code blocks) whenever helpful

# What gets a MEMORY.md

Store knowledge that is:

- Useful across multiple agent sessions
- Not obvious from the code
- Important for making correct decisions
- Stable enough to remain useful

Examples:

- Things that were tried and deliberately rejected
- Project preferences that affect future work
- Important knowledge that is both uncommon/unique (cannot be found on the internet) and that cannot be inferred from the repository

Skip:

- Temporary task context
- TODO lists
- Session logs
- Step-by-step descriptions of recent work
- Generic programming knowledge
- Build/CI instructions that belong in repository documentation
- Facts that are likely to become obsolete
