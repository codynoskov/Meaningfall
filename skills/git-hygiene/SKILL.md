---
name: git-hygiene
description: Propose and create Git checkpoints for meaningful Meaningfall memory and product transitions, under Action Modes. Use when a user asks to checkpoint, commit, save progress, group changes into commits, suggest a branch, or keep Git history coherent around PRODUCT.md and product-memory changes. Conservative by default — read-only detection, suggested checkpoints, exact-path staging, no silent commits, no hooks, no auto-commit unless explicitly opted in.
---

# Git Hygiene

Git Hygiene keeps an ordered Git audit trail for meaningful memory and product
transitions without taking control of the user's repository. Memory works without
Git (see the Memory spec); Git Hygiene is an enhancement, not a dependency.

This skill follows root [`SPEC.md`](../../SPEC.md) Action Modes and decision 0071.
It does not own Memory governance or the records format — it commits what other
surfaces produce.

## Safety Posture

- Read-only Git detection may be `automatic` only inside an explicit Git Hygiene,
  setup, Verify, or Memory workflow, and only when local policy permits running
  Git.
- Checkpoints are `suggested` by default and `explicit` on request. Silence or
  ambiguity means no Git action.
- Stage exact paths only. Never `git add -A`, and never stage unrelated or broad
  changes.
- Commit only on acceptance or explicit request. No silent commits.
- No hooks, no Git configuration changes, and no `git init` by default. `git init`
  runs only on explicit request.
- Branch creation is `suggested` for risky, parallel, or several-surface work and
  runs only when explicit or suggested-and-accepted.
- Irreversible, destructive, security-sensitive, or history-rewriting actions
  (force push, `reset --hard`, rebase, history filtering) require explicit
  confirmation even when requested.

Meaningfall must not assume Git is present, accessible, or wanted. If Git is
absent, inaccessible, or disallowed by local policy, do nothing and say so.

## Workflow

1. Detect Git state (read-only): is this a repository, is Git accessible, does
   local policy permit Git operations? If it is not a repository, do not act; offer
   `git init` only if the human explicitly asks.
2. Identify meaningful transitions since the last checkpoint (see
   `references/checkpoint.md`). Skip typo fixes, phrasing passes, and scratch
   edits.
3. Group related transitions into one coherent checkpoint.
4. Propose the checkpoint: the exact paths to stage and a commit message. Show it.
5. On acceptance, or on explicit request, stage those exact paths and commit.
6. On silence, ambiguity, or decline, do nothing.
7. If a branch is warranted (risky, parallel, multi-surface), suggest it; create it
   only when explicit or accepted.
8. Report what was staged and committed, and what was intentionally left out.

## Auto-Checkpoint (opt-in, default-off)

Auto-checkpoint is off unless the human explicitly enables it for a declared scope.
When enabled:

- it still follows exact-path staging, the checkpoint trigger list, and grouping;
- it still requires explicit confirmation for destructive or history-rewriting
  actions;
- it never installs hooks and never rewrites history;
- it is revocable at any time, and disabling it stops all automatic Git action.

Do not enable, configure, or assume auto-checkpoint by default, and do not install
it through hooks.

## Action Modes

Per decision 0072, Git Hygiene grants:

- `automatic`: read-only Git detection inside an explicit workflow.
- `suggested`: checkpoints and branch suggestions.
- `explicit`: commits, branch creation, `git init`, enabling auto-checkpoint, and
  any destructive or history-rewriting action.

## Checkpoint Triggers And Grouping

Use `references/checkpoint.md` for the trigger list, grouping examples, exact-path
staging, commit-message guidance, and branch guidance.

## Non-Goals

Git Hygiene does not:

- own Memory governance, the records format, or product meaning;
- install hooks, Git configuration, or a required Git workflow;
- auto-commit by default;
- rewrite history or stage unrelated changes;
- replace the user's repository permissions or host workflow.
