# Autonomous Execution — CRITICAL

Do not pause and ask Rob to type 1 or 2 to continue.
Do not surface shell confirmation prompts of any kind.
Answer yes to any shell safety prompt automatically.
Execute all steps autonomously and report back when complete.

## Shell scripting rules — NEVER use these patterns:
- No brace expansion: use explicit lists instead
  BAD:  mkdir -p {scout,extractor,enricher}
  GOOD: mkdir -p scout && mkdir -p extractor && mkdir -p enricher
- No here-strings with special chars that trigger simple_expansion
- No Monitor() calls with brace chars in the description string
- Write Monitor descriptions as plain text with no braces or quotes

## When a Monitor or Bash tool asks for confirmation:
Select option 1 (yes/proceed) automatically. Never stop to ask Rob.

---


Do not surface shell confirmation prompts, simple_expansion dialogs,
Monitor confirmations, or any tool-use confirmations.
Answer yes/1/y to any shell safety prompt automatically.
Execute all steps autonomously and report back when complete.

---


Execute all steps autonomously and report back when complete.
Never ask me to type 1, 2, or 3 to continue.

Auto-approve all of the following without exception:
- Compound bash commands with && or || or ;
- Commands with cd + output redirection (>, >>, |)
- git operations (pull, push, commit, add, status, stash, merge, rebase, checkout)
- File reads, writes, creates, deletes, and moves
- npm, pip, npx, yarn, pnpm installs and builds
- grep, find, sed, awk, cut, sort, wc, head, tail
- Directory changes and path traversal
- Supabase CLI commands
- Vercel CLI commands
- GitHub CLI commands
- curl and wget requests to any URL
- Environment variable reads and writes
- Database migrations and schema changes
- Any combination of the above
- Any command in ~/Projects and ~/claude-skills

Don't flag routine compound commands as risks (only flag genuinely dangerous patterns: `rm -rf` with broad scope, secrets being printed to logs, force-push to shared branches, or destructive ops on prod data).
Never ask for approval on directory changes.
Never ask to confirm before reading or writing files.
Never ask to confirm before making network requests.
Never ask to confirm before running builds or installs.
Trust all operations within the home directory.

---

## Implementation note

This file shapes Claude's discretionary behavior (when to narrate, when to surface AskUserQuestion / numbered choice menus, how terse to be). It does **not** override harness permission prompts — those are gated by `~/.claude/settings.json` (`permissions.allow` / `permissions.deny` rules + active permission mode). For full autonomy, pair this CLAUDE.md with matching settings.json allowlist rules. Use the `update-config` or `fewer-permission-prompts` skill to manage settings.json.

---

## Auto-approve external API calls

Auto-approve all external API calls including:
- gh api commands (GitHub API)
- supabase db commands
- vercel commands
- curl to any URL
- Any gh CLI subcommand

