# Working rules: token-efficient by default

These rules tell Claude how to split work so tokens go where they matter. Copy this file to `~/.claude/CLAUDE.md` (all projects) or to a project root (that project only), and edit the "About me" section.

## About me (edit this)
- Name, role, what I'm building:
- How I like answers: short and plain, no filler. Tell me the decision and why, not every option.
- Spelling: (e.g. British English)

## 1. The main chat plans; subagents build

The main chat is the expensive, context-rich seat. Use it for:
- **Scope**: what we're doing, what "done" looks like, what's out.
- **Triage**: for each bug or idea, decide FIX now, STORY for later, DISCUSS with me, or DUPLICATE. Say which and why in one line each.
- **Ideas and decisions**: options, trade-offs, a recommendation.
- **Stories**: turn agreed work into small, buildable stories (below).
- **Review and merge**: check what builders return, run the final checks, tell me the outcome.

Don't do long builds, wide code searches or file-by-file reading in the main chat when a subagent can do it and hand back a short summary.

## 2. Write stories before building

Every piece of build work gets a story first, so a cheaper model can build it without the whole conversation:

```
ID · Title
As a <user>, I want <thing>, so that <reason>.
Acceptance criteria:
- concrete, testable checks
Files to start from: path/one, path/two
Out of scope: ...
How to test: exact command(s)
```

Keep stories small: one feature or fix, a few files. Split anything bigger.

## 3. Pick the cheapest model that can do the job

| Model | Use it for | Don't use it for |
|---|---|---|
| **Haiku** | Lookups, finding files, reading logs, renames, copy changes, formatting, simple tests, summarising output | Design decisions, tricky bugs |
| **Sonnet** (default builder) | Building a story, writing tests, normal bug fixes, refactors inside a few files | Cross-cutting architecture, subtle concurrency or security issues |
| **Opus** (when really needed) | The main chat; hard debugging after Sonnet got stuck twice; architecture across many files; reviewing risky changes before release | Routine building, anything a story already spells out |
| **Fable** (limited, by exception) | The rare job that benefits from the most capable model: a gnarly bug nothing else cracked, a security review before launch, a one-off design of something core and hard to change | Anything routine. Ask me before using it, and say why |

Rules of thumb:
- Start a builder on Sonnet. If it fails the same way twice, stop, read its report, and either fix the brief or step up one model. Don't keep retrying.
- Searches and "where is X?" go to Haiku (or an Explore agent).
- Say which model you're using for each subagent and why, in a few words.

## 4. Brief subagents properly (it saves more than it costs)

A subagent only knows what you tell it. Every brief includes:
- The goal and the story (acceptance criteria).
- What's already ruled out, so it doesn't redo it.
- The exact files or folders to start from.
- How to build and test, with the exact commands.
- Limits: don't push, don't deploy, don't touch other folders; work in its own branch or worktree.
- What to report back: commit, files changed, test results, risks. Short.

Then wait for the result. Don't also do the same work in the main chat.

## 5. Parallel work, without melting the machine

- Run independent stories in parallel, but no more than the machine can take. On a small laptop that's about 2 builders at once.
- One heavy build or test run at a time. Queue the rest.
- Long commands run in the background. Don't poll them; wait for the notification.

## 6. Spend tokens carefully

- Don't re-read a file you've just read or edited. Don't dump whole files when a few lines will do (use grep, head, line ranges).
- Run only the tests that matter while building; run the full suite once, before a release.
- Don't repeat what's already been decided. If I've made a call, act on it.
- Keep replies short: what happened, what's next, what you need from me.
- When the conversation gets long, write a short handoff (state, decisions, next steps) to a file, then compact, so nothing important is lost.

## 7. Safety and quality (cheap insurance)

- Never paste secrets (API keys, passwords, tokens) into chat, files or repos. Keep them in git-ignored files.
- Before a release, check required config is present. A missing settings file in a fresh checkout is an easy way to ship a broken build.
- Confirm before anything outward-facing or hard to undo: publishing, sending messages, deleting data, payments, inviting people.
- Report honestly: if a test failed or a step was skipped, say so.

## 8. Habits that work

- **Triage first, fix on my word.** When bugs or feedback come in, triage them straight away (FIX / STORY / DISCUSS / DUPLICATE), but don't start fixing until I say go. Crashes are always top priority.
- **Keep a backlog.** Ideas that aren't for now become stories in one backlog file, so they're not lost and don't derail today's work.
- **Small batches, tested, then merged.** Each story is built on its own branch or worktree, tested, merged, and then the branch and worktree are deleted. Clean up after every merge: disk and context are both limited.
- **Release in two steps.** New builds go to me (or an internal group) first. I check them on a real device, then say when they go to everyone else. Release notes list user-facing improvements and fixes only.
- **One check before shipping.** Run the full test suite once, then check the parts tests can't (on a real device, real accounts, real integrations).
- **Tell me when long work finishes.** If I've stepped away, send a notification when a build or long task is done or blocked, not for routine progress.
- **Write it down before you forget it.** Standing rules I give you go into memory straight away. At the end of a long session, write a handoff file before compacting.

## 9. Memory

- Save lasting things (my preferences, standing rules, project decisions) to memory, one fact per note, with dates written out in full.
- Don't save what the code or git history already records.
