# Claude token playbook

A ready-made `CLAUDE.md` for [Claude Code](https://claude.com/claude-code) that gets the most done per token, without losing track of your work.

The idea: the main chat (the most capable, most expensive model) does the thinking, such as scoping, triage, decisions and writing stories. Cheaper subagents (Haiku, Sonnet) do the building, searching and testing. Opus and Fable are kept for the jobs that really need them. Context is saved regularly to a file, so the main chat stays small and nothing important is lost when it compacts.

## What's in it

| File | What it is |
|---|---|
| `CLAUDE.md` | The working rules. Claude reads this at the start of every session. |
| `skills/lean-context/SKILL.md` | A short checklist skill Claude loads at the start of a session, before multi-agent work and before compacting. |

### What the rules cover
1. **Start cheap:** read the project's context file first, read only what's needed.
2. **Keep the main chat lean:** a context file per project, updated at every milestone; compact at about half the context window; the same setup on every machine.
3. **The main chat plans, subagents build:** scope, triage (fix / story / discuss / duplicate), decide, then hand off.
4. **Stories before building:** acceptance criteria, files, how to test; a backlog for later ideas.
5. **The cheapest model that's still right first time:** Haiku, Sonnet, Opus, Fable, and when to step up.
6. **Tight briefs for subagents:** goal, files, rules, "done", a stop condition, a short report.
7. **Parallel work sized to the machine:** it checks your cores and memory and sets its own limit.
8. **Let the machine do the work:** scripts, queues, background jobs, caches.
9. **Research first,** so things land right first time.
10. **Visual review pages:** an HTML page with per-item (and spoken) feedback, used when something needs eyes.
11. **Verify before anyone else sees it:** checks that stop at the first failure, honest test results.
12. **Release in two steps:** to you first, then wider.
13. **Safety and privacy:** no secrets in files, no moving money, ask before anything outward-facing.
14. **Lean replies and rules.**

## Install

**macOS or Linux**
```bash
mkdir -p ~/.claude/skills
git clone https://github.com/LeeProline/claude-token-playbook.git
cp claude-token-playbook/CLAUDE.md ~/.claude/CLAUDE.md
cp -R claude-token-playbook/skills/lean-context ~/.claude/skills/
```

**Windows (PowerShell)**
```powershell
git clone https://github.com/LeeProline/claude-token-playbook.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item claude-token-playbook\CLAUDE.md "$HOME\.claude\CLAUDE.md"
Copy-Item -Recurse claude-token-playbook\skills\lean-context "$HOME\.claude\skills\"
```

If you already have a `~/.claude/CLAUDE.md`, merge the two rather than overwriting it.

Then open `~/.claude/CLAUDE.md` and fill in **About me**: how you like answers, your spelling, and (optionally) how many parallel builders your machine can take.

## Getting started

- **Day one:** sections 1 to 6 give most of the savings. Read those.
- **As projects grow:** the rest (parallel work, scripts, visual reviews, release steps) become useful.
- **Make it yours:** when Claude does something you don't like, tell it to save a rule. The file gets better the more you use it.
- **More than one computer?** Keep the same `CLAUDE.md` on each, and keep each project's context file in the project's repo, so any machine can pick up where another left off.

## Licence

MIT. Copy it, change it, share it.
