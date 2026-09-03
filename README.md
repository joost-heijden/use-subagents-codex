# use-subagents

A reusable Codex skill for splitting complex work into visible Codex tasks.

## Why use it?

For larger coding or product tasks, you often want Codex to:

1. inspect the repository and existing patterns;
2. implement the work in an isolated worktree;
3. review the result independently;
4. repair issues and review the complete change again;
5. verify tests, CI and any authorized GitHub action.

Without a fixed workflow, agents can use hidden subagents, mix implementation and review responsibilities, or stop after local tests pass. This skill makes those boundaries explicit.

## Default task routing

| Task type | Model | Permission |
| --- | --- | --- |
| Discovery and implementation | Luna, max reasoning | May change its owned worktree |
| Code, design or functional review | Sol, high reasoning | Read-only |
| Orchestration | Calling Codex task | Dispatches, waits, integrates and reports |

All workers must be visible as separate Codex tasks in the sidebar. The skill never silently falls back to hidden agents or a different model when the required capabilities are unavailable.

## Install

Clone or download this repository, then copy it into your Codex skills directory:

```sh
cp -R use-subagents-codex ~/.codex/skills/use-subagents
```

If the repository has another local path, replace `use-subagents-codex` with that path.

Start a new Codex task after installing so the skill index can refresh.

## Use

Invoke the skill explicitly:

```text
Use $use-subagents to coordinate this work through visible Codex tasks.
```

Then add the actual assignment, for example:

```text
Use $use-subagents to implement the customer planning flow in this repository.
Push the branch to GitHub, open a PR, and review the pushed result. Do not merge or deploy.
```

## Important boundaries

- Reviewers only report findings; they do not edit or fix code.
- One writer owns a worktree by default. Parallel writers are used only for non-overlapping work.
- A `NEEDS FIXES` review returns to the original writer, followed by a full re-review.
- Local tests, GitHub CI, deployment and production health are separate proof states.
- Push, pull request, merge, deployment and production actions require explicit authorization in the task.

## Requirements

The Codex environment must support visible task creation, task waiting, task reading and follow-up messages. The requested model bindings must also be available:

- workers: `gpt-5.6-luna` with `max` reasoning;
- reviewers: `gpt-5.6-sol` with `high` reasoning.

If a required capability is missing, the skill stops and reports the blocker.

## License

MIT
