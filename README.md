# Claude token playbook

A ready-made `CLAUDE.md` that makes Claude Code split work so tokens go where they matter: the main chat scopes, triages and writes stories; cheaper subagents (Haiku, Sonnet) build; Opus and Fable are kept for the jobs that need them.

## Use it
1. Copy `CLAUDE.md` to `~/.claude/CLAUDE.md` (every project) or into a project folder (that project only). Use the same file on every machine you work on.
2. Fill in the "About me" section.
3. Optional: copy `skills/lean-context` to `~/.claude/skills/lean-context`. It's a short skill Claude loads at the start of a session, before multi-agent work and before compacting, to keep context lean.

MIT licence. Edit freely.
