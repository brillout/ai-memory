Store knowledge that AI agents should remember across sessions in `MEMORY.md` files:

- `MEMORY.md` => global memory that applies for the repository as a whole
- `some-dir/` => `some-dir/MEMORY.md` => applies only to the directory
- `some-file.ext` => `some-file.MEMORY.md` => applies only to the file

Agents should consult all applicable `MEMORY.md` files when reading or modifying code.


## Goal

A `MEMORY.md` is the answer an AI agent gives itself when a future session asks: **"What do I need to remember about this?"**

It contains durable, important, and unique knowledge that should be remembered across agent sessions — things that would otherwise have to be repeatedly explained.

Litmus test: **if a fresh AI session should know about it, and the knowledge isn't available from the internet or reading the code, it belongs in `MEMORY.md`.**


## Content

- Memory is for **knowledge**, not a description of the codebase
- Durable knowledge, not temporary context
- Likely going to be useful across *many* agent sessions
- Stable enough to remain useful, no temporary knowledge
- Important for making correct decisions
- Only unique knowledge: skip anything that can be found on the internet
- Skip anything that can be inferred by reading the code
- Don't turn memory into a diary or session log
- Keep it small and high-signal — every sentence should earn its place
- ELI5: simple terms, no jargon
- Delete on contradiction: when an entry turns out false, remove it — don't append a correction below it.

Examples:

- Business context
- Business constraint that exists nowhere in the code
- Unique insights
- Things that were tried but deliberately rejected and why

Skip:

- Temporary task context
- TODO lists
- Session logs
- Step-by-step descriptions of recent work
- Generic programming knowledge
- Facts that are likely to become obsolete
- Build/CI instructions that belong in repository documentation
- Anything a linter, type, or test already enforces => let the tool do the remembering
- Secrets, credentials, personal data
- Global preferences (style, tone, tooling) => those belong in the agent's config, not beside the code
- Session logs, changelogs, "what I did today" => that's history, not memory


## File content

```md
## TLDR [optional]

List of one-sentence succinct summary of each item listed below.

## Decisions [optional]

List of important decisions that were made (and their rationale if available).

## Knowledge [optional]

List of important and unique knowledge when working on this area.

## Gotchas [optional]

List of things that are easy to get wrong.

## Before modifying this file

Read this file's format at https://raw.githubusercontent.com/brillout/ai-memory/refs/heads/main/memory.md
```

Notes:

- The `## ... [optional]` sections are optional, and feel free to create other sections
- Prefer updating existing knowledge over accumulating new entries
- Remove obsolete knowledge
- Consider using graphics (e.g. `mermaid` code blocks) whenever helpful


# Maintenance

Unmaintained memory is worse than none — a wrong entry costs more than an absent one.

- Eagerly delete: when an entry turns out false (e.g. contridicts more recent knowledge), remove it — don't append a correction below it.
- DRY — one entry, one place: duplicated memory drifts apart and both copies become untrustworthy.
- Pin what moves: an entry that depends on an external version, service, or platform says so, so it can be re-checked.
