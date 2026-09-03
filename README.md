# use-subagents

A reusable Codex skill for coordinating work through user-visible Codex tasks.

It provides a small orchestration contract:

- execution and discovery tasks use Luna with max reasoning;
- reviews use Sol with high reasoning;
- reviewers remain read-only;
- repair work returns to the original writer;
- push, pull request, merge, deployment, and production actions remain separately authorized.

## Install

Copy this repository into the Codex skills directory:

```sh
cp -R . ~/.codex/skills/use-subagents
```

Then invoke it with:

```text
Use $use-subagents to coordinate this work through visible Codex tasks.
```

The skill requires Codex task creation, task waiting, task reading, and follow-up messaging to be available. It stops instead of silently falling back to hidden agents or a different model.
