# Superpowers notes

These are the facts the pages rely on, summarized from [obra/superpowers](https://github.com/obra/superpowers) at **v7.0.1, commit `2ce8aa1` (2026-10-21)**. Skills change often, so check the current files before relying on these.

To read them again:

```bash
git clone --depth 1 https://github.com/obra/superpowers.git
```

## Files read

Most of what follows comes from `skills/subagent-driven-development/`: `SKILL.md`, `implementer-prompt.md`, the start of `task-reviewer-prompt.md`, and `references/`. The rest comes from `writing-plans`, `dispatching-parallel-agents`, `using-superpowers` and its Claude Code notes, and the start of `verification-before-completion`.

`brainstorming`, `using-git-worktrees` and `finishing-a-development-branch` were read through a fetched summary rather than line by line, so check those first if something looks off.

## The flow

1. `brainstorming`: nothing gets built until the design is approved. Specs go in `docs/superpowers/specs/`.
2. `writing-plans`: plans go in `docs/superpowers/plans/`. The person then chooses Subagent-driven or Native.
3. `using-git-worktrees`: an isolated branch and a test baseline.
4. `subagent-driven-development`: a pre-flight conflict scan, then the task loop.
5. Final whole-branch review on the most capable model, with one fix wave.
6. `finishing-a-development-branch`: tests must pass, then merge, open a pull request, or keep the branch.

## The task loop

- The controller records BASE and writes a brief file for the task.
- One implementer works at a time, and it never spawns its own subagents.
- It reports DONE, DONE_WITH_CONCERNS, NEEDS_CONTEXT or BLOCKED.
- One task reviewer gives two verdicts: spec compliance and quality.
- **Fix loop:** up to five rounds. Rounds 1 to 3 resume the same implementer, and rounds 4 and 5 use a fresh one on a stronger model. Each round ends with a scoped re-review, then the controller rules on anything left at the cap.
- The ledger (`progress.md`, under `.superpowers/sdd/`) is what survives compaction.

## Stopping and rulings

The controller stops for only four things: an irreversible or destructive operation, a security-sensitive action, an outside side effect that normally needs asking, and a plan where every way forward is a guess. Everything else gets a recorded ruling, and all rulings appear in a final "Rulings I made" list.

## Model tiers

| Role | Tier |
|---|---|
| Implementer, plan has the complete code, or a single-file mechanical fix | Cheapest |
| Implementer from prose, multi-file work, debugging | Mid-tier |
| Design judgment, broad codebase knowledge | Most capable |
| Task reviewer | Mid-tier at least, scaled to risk |
| Scoped re-review of a small fix | Cheap to mid-tier |
| Fix rounds 4 and 5 | At least one tier above the stuck implementer |
| Final whole-branch review | Most capable |

Always name the model, because an omitted one inherits the session's.

## Parallel work

`dispatching-parallel-agents` is for separate problems with no shared state, such as unrelated failures. It isn't for implementers in the task loop.

## Where the sources disagree

The pages follow the skill files in both cases:

- **Worktree order:** the README lists the worktree before planning. `writing-plans` says it's created at execution time.
- **Plan contents:** the README says tasks have complete code. `writing-plans` says to leave out function bodies that the signature and tests already determine.

## Install

The playbook gives the Claude Code command, `/plugin install superpowers@claude-plugins-official`. Other tools are in the Superpowers README. The skill's helper scripts run through `bash`, so Windows users need it available to their agent.
