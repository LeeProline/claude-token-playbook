---
name: lean-context
description: Get the most done per token. Use at the start of a session, before planning multi-step or multi-agent work, when context is getting large, and before ending a long session or compacting.
---

# Lean context: get the most done per token

The budget is finite and shared across projects. Spend tokens where judgement is needed; let scripts and the machine do the rest.

## 1. Before starting
- Restate the goal in one line.
- Pick the cheapest route that is still right first time.
- Check for a handoff or state file (HANDOFF*.md, PLAN*.md, a queue or status file) and read that first instead of re-exploring.
- Read only the files and line ranges you need (search first, then read with offset/limit). Never dump whole large files, logs or JSON into context.

## 2. Models and agents
- Do the thinking-heavy design once; give bulk building, research and mechanical work to the cheapest model that can do it (mid-size for building, smallest for runs and checks); top model only for hard architecture or when asked.
- Run agents in parallel when the work is independent (separate worktrees or files); never two agents editing the same files.
- Brief agents tightly: goal, exact files, rules, what "done" means, a token-light instruction, a stop condition; ask for a 4 to 8 line report.
- Tell agents to write a handoff file and stop when budget runs low.
- Prefer continuing an agent with a short message over spawning a fresh one with a long brief, unless its context is huge (then a fresh agent from the handoff file).

## 3. Let the machine work, not the model
- Turn repeated work into a script or queue that runs unattended (builds, renders, exports, checks); the model writes it once.
- Make outputs land somewhere the user can see without the model in the loop (a live page that reads a folder, a report file).
- Store the user's feedback in files agents read directly instead of relaying through chat.
- Watch long jobs with a monitor or a background command that exits on completion; never poll in a loop or sleep and re-check.
- Put a cheap automatic check (numbers, a contact sheet) between a build and the user.

## 4. Keep context small
- Summarise tool output in a line; batch small requests into one agent message.
- Keep replies short: what changed, what's next, what needs the user; no recaps.
- When notes contain lasting rules, write them once into the project's rules file and to memory.

## 5. Avoid waste
- Don't re-render or re-run unchanged things (use caches and draft modes; full quality once at the end).
- Don't show the user work that hasn't passed its checks (each failed review round costs tokens twice).
- Don't plan an unattended run without first proving the pipeline on one or two items.
- Don't keep exploring once you have enough to act.
- Stop background watchers and servers you no longer need.

## 6. Before ending a long session and before any compaction
- Everything committed or saved.
- The handoff file says exactly where things stand and the next steps.
- Durable lessons saved to memory; note anything the user must decide.
- Refresh the handoff at natural milestones so it is current when compaction happens, and read it first afterwards.
