# Agent Instructions

This project uses **bd** (beads) for issue tracking. Run `bd onboard` to get started.

## Starting a New Task

**BEFORE beginning any work**, you MUST:

1. **Read llmemory** - Review project context and previous decisions:
   ```bash
   # Read all llmemory files to understand:
   cat .llmemory/facts.jsonl      # Project facts and structure
   cat .llmemory/decisions.jsonl  # Design decisions and rationale
   cat .llmemory/summaries.jsonl  # Current project state
   cat .llmemory/tasks.jsonl      # Completed and pending tasks
   cat .llmemory/index.json       # Recent project updates
   ```

2. **Understand the context** - Know what's been built, why decisions were made, and current state
3. **Check for relevant issues** - Run `bd ready` to see available work
4. **Begin work** - Only after understanding the full context

**WHY THIS MATTERS:** llmemory contains critical context about design decisions, architecture choices, and project history. Working without this context leads to inconsistent implementations and wasted effort.

## Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --status in_progress  # Claim work
bd close <id>         # Complete work
bd sync               # Sync with git
```

## MCP Servers

Use MCP servers only when you need external docs, repository context, or structured data that is not in the local workspace. Prefer MCP resources/templates over web search when available.

**Available MCPs and usage:**
- `list_mcp_resources` / `list_mcp_resource_templates`: discover what data a server exposes before fetching anything.
- `read_mcp_resource`: read a specific resource URI returned by the list calls.
- `octocode`: GitHub code search, file contents, repo structure, and PR history. Use for cross-repo discovery or upstream references.
- `deepwiki`: high-level repo documentation and Q&A for GitHub projects.
- `context7`: library documentation. Always call `resolve-library-id` first, then `get-library-docs`.
- `astrodocs`: Astro framework docs search.
- `sequential-thinking`: structured multi-step analysis for complex reasoning or planning.
- `playwright`: browser automation for interactive UI verification or scraping when needed.

**Quick examples:**
- `list_mcp_resources` / `list_mcp_resource_templates`: "What resources does the configured server expose?"
- `read_mcp_resource`: "Fetch the specific resource URI returned by the list call."
- `octocode`: "Find how another repo implements a feature" or "inspect a specific file/PR in GitHub."
- `deepwiki`: "Get a repo's architecture overview or answer how a module is intended to work."
- `context7`: "Look up official API usage for a library version."
- `astrodocs`: "Search Astro-specific docs for a config or API question."
- `sequential-thinking`: "Break down a complex refactor into steps before editing."
- `playwright`: "Verify a UI interaction or capture a page snapshot in a browser."

**Rules of thumb:**
- Use local tools (`rg`, file reads) for anything inside this repo.
- Use MCP only when external context is required, and keep queries narrow.
- Prefer list ? read: discover resources/templates first, then fetch specifics.
- Summarize key findings; avoid dumping large raw outputs.

## Completing a Task

**After completing ANY task** (fixing a bug, implementing a feature, etc.), you MUST:

1. **Update llmemory** - Document what was accomplished:
   ```bash
   # Add to .llmemory/tasks.jsonl - what was done
   # Add to .llmemory/facts.jsonl - any new facts about the project
   # Add to .llmemory/decisions.jsonl - any design/technical decisions made
   # Update .llmemory/index.json - add entry with date, description, files modified
   ```

2. **Update beads** - Close or update the relevant issue:
   ```bash
   bd close <issue-id>  # If task is complete
   bd update <issue-id> --status in_progress  # If still working
   ```

**WHY THIS MATTERS:** llmemory provides continuity between sessions. Without updates, the next agent won't know what you did or why, leading to duplicated effort or inconsistent implementations.

## Landing the Plane (Session Completion)

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **Update llmemory** - Document all completed work (see "Completing a Task" above)
2. **File issues for remaining work** - Create issues for anything that needs follow-up
3. **Run quality gates** (if code changed) - Tests, linters, builds
4. **Update issue status** - Close finished work, update in-progress items
5. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git pull --rebase
   bd sync
   git push
   git status  # MUST show "up to date with origin"
   ```
6. **Clean up** - Clear stashes, prune remote branches
7. **Verify** - All changes committed AND pushed
8. **Hand off** - Provide context for next session

**CRITICAL RULES:**
- Work is NOT complete until `git push` succeeds
- NEVER stop before pushing - that leaves work stranded locally
- NEVER say "ready to push when you are" - YOU must push
- If push fails, resolve and retry until it succeeds

