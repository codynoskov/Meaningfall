# Git Hygiene Checkpoints

Applied guidance for Git Hygiene checkpoints. Authority for Git behavior is root
`SPEC.md` Action Modes and decision 0071. This reference lists triggers, grouping,
staging, message, and branch guidance; it grants no new automatic behavior.

## Checkpoint Triggers

Pay attention to a checkpoint when a meaningful memory or product transition
happens, including:

- a durable `PRODUCT.md` change;
- a new decision record, or a decision status change;
- a `supersedes` / `superseded_by` link added;
- a note added, promoted, merged, cleaned up, removed, or moved into a draft,
  decision, Product Definition, glossary entry, or approved guidance;
- a draft status change to `paused`, `promoted`, `rejected`, or `superseded`;
- an accepted change beginning or completing implementation;
- an archive move;
- an approved edit to host-owned `AGENTS.md`.

Do not create a separate checkpoint for typo fixes, phrasing passes, scratch text,
or every file save.

## Grouping

Group related transitions into one coherent checkpoint. For example:

```text
notes cleanup
draft created from promoted notes
source link in draft
```

```text
PRODUCT.md change
decision recording the rationale
glossary term update
```

Avoid one commit mixing unrelated memory, product, and implementation changes, and
avoid many microscopic commits that skip the real transition.

## Exact-Path Staging

- Stage only the paths involved in the checkpoint.
- Never stage unrelated or broad changes, and never `git add -A`.
- If unrelated changes are present in the working tree, leave them and say so.

## Commit Messages

- Use a short, semantic summary of the transition. A Conventional Commits style is
  a useful reference point, not a requirement.
- Describe the memory or product transition, not the file mechanics.
- One checkpoint, one coherent message.

## Branches

- Stay on the current branch for ordinary small changes when the tree is clean.
- Suggest a short-lived branch for risky, parallel, or multi-surface changes, or
  when a change touches public contracts or several memory surfaces together.
- Create a branch only when explicit or suggested-and-accepted.
- Surface stale branches and worktrees for cleanup after merge or abandonment.
