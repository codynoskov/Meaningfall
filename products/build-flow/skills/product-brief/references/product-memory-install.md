# Product Memory Install Contract

Contract generation: **install-contract v1**.

This reference is the operational source of truth for Product Brief's product-memory install behavior. `SKILL.md` carries the runnable interview and stage flow; this file carries the detailed install contract and install gate. ProductMD format rules remain in the ProductMD spec and `references/verification.md`.

## Install Shape

For a new product, Product Brief installs:

```text
PRODUCT.md
product-memory/
  README.md
  notes.md       # create-on-need
  decisions.md   # create-on-need
  drafts.md      # create-on-need
  glossary.md    # create-on-need
  archive/       # lazy, first supersession
AGENTS.md        # default-on approval-visible integration; host-owned
```

Always create:

- `PRODUCT.md` — canonical product truth.
- `product-memory/README.md` — role map, read order, and install attribution.

Create only when populated:

- `product-memory/notes.md` — unresolved, deferred, future, not-now, or rejected-but-useful material.
- `product-memory/decisions.md` — accepted rationale when the why is non-obvious, contested, or useful to preserve.
- `product-memory/drafts.md` — candidate product-meaning changes that target a specific future `PRODUCT.md` owner or change.
- `product-memory/glossary.md` — terms, aliases, rejected names, and naming distinctions.

Create lazily:

- `product-memory/archive/` — superseded or historical memory worth recovering. Do not create it during initial install unless there is already material to archive.

Do not create:

- `product-memory/state.yaml`;
- empty supporting files;
- empty headings inside supporting files;
- a live `product-memory/` folder under the public `products/` tree;
- `products/memory/` only to house this contract.

## Authority

`PRODUCT.md` is canonical product truth. Supporting memory is lower authority, not no-authority: each supporting surface is authoritative for its own role, but none overrides `PRODUCT.md` on product meaning.

If supporting memory appears to conflict with `PRODUCT.md`, surface the conflict instead of silently choosing. Conflict detection and repair workflows are future Memory / Build Flow behavior; this contract only defines install-time placement and guidance.

## Creation-Time Classification

Use these placement rules when Product Brief captures material that should persist:

- Current accepted product meaning -> `PRODUCT.md`.
- Accepted but open product meaning -> `PRODUCT.md` as `TBD` or a recorded assumption only when a consumer must know that the slot exists even while the value is open.
- Deferred, future, not-now, unresolved, or rejected-but-useful material with no target change -> `product-memory/notes.md`.
- Candidate direction targeting a specific `PRODUCT.md` owner or change -> `product-memory/drafts.md`.
- Accepted rationale -> `product-memory/decisions.md` when the why is useful to preserve.
- Terms, aliases, rejected names, and naming distinctions -> `product-memory/glossary.md`.
- Source or provenance -> inline by role in `PRODUCT.md`, `decisions.md`, `drafts.md`, or `notes.md`; do not create a separate ledger.

Rejected terminology goes to `glossary.md`; rejected product direction or approach goes to `notes.md` when it remains useful.

Do not hide accepted product truth in supporting memory. Do not turn `PRODUCT.md` into a question list; a `TBD` belongs there only when the slot itself changes what gets built or flags a required decision.

## `product-memory/README.md`

Create this file for every new install:

```md
# Product Memory

`../PRODUCT.md` is the canonical accepted product truth.

This folder holds supporting product memory: notes, glossary, drafts, decisions, and archive.

Installed by Meaningfall Product Brief.

Supporting files are created when there is content for them. Missing files mean there is no recorded material for that role yet.

This memory is yours to edit, extend, or prune as your project needs.

## Read Order

1. Read `../PRODUCT.md`.
2. Read this file for memory roles.
3. Read `glossary.md` if it exists and terms or names matter.
4. Read `notes.md` and `drafts.md` if they exist and unresolved or future context matters.
5. Read `decisions.md` if it exists and rationale matters.
6. Read `archive/` only if it exists and historical, recovery, or audit work requires it.

## Surfaces

- `notes.md` — unresolved, deferred, future, not-now, rejected-but-useful material.
- `glossary.md` — canonical terms, aliases, rejected names, distinctions.
- `drafts.md` — proposals and candidate changes before approval.
- `decisions.md` — accepted rationale.
- `archive/` — superseded or historical memory; created on first supersession.
```

## Supporting File Sketches

These are maximal references, not templates. Instantiate only the files and sections that have content. Never create a file or heading just because it appears here.

### `notes.md`

```md
# Notes

Non-canonical product memory.

## Deferred

- Team pricing is plausible, but not part of the first build.
```

### `decisions.md`

```md
# Decisions

## 2026-06-19 — First Scope

Decision: Start with individual workspaces before team workspaces.

Why: The first useful version can prove the core workflow without account administration.
```

### `drafts.md`

```md
# Drafts

## Team Workspace Model

Candidate change: Add team workspaces to `map.product`.

Open question: Whether team roles are fixed or configurable.
```

### `glossary.md`

```md
# Glossary

## Terms

### Workspace

The user's primary area for saved work.

Aliases:
- Project space

Avoid:
- Dashboard
```

## AGENTS.md Integration

Product Brief should create or update `AGENTS.md` with a small marked product-memory block by default unless the user opts out.

This is approval-visible:

- explain that the edit is recommended so future agents can discover product memory;
- if `AGENTS.md` exists, update only the marked Meaningfall block and leave unrelated host instructions unchanged;
- if `AGENTS.md` does not exist, create it as the project's agent-instruction file, not as a Meaningfall-owned file;
- respect opt-out for any reason, including host or organization policy.

Recommended block:

```md
<!-- meaningfall:product-memory v1 start -->
## Meaningfall Product Memory

Before changing durable product meaning, read `PRODUCT.md` first.

Use `product-memory/README.md` for the supporting memory read order and file roles. Supporting memory may provide context, rationale, drafts, terminology, and parked material, but it does not override `PRODUCT.md` on product truth.

If supporting memory seems to conflict with `PRODUCT.md`, surface the conflict rather than silently choosing.

For durable product-meaning changes, propose a focused `PRODUCT.md` diff. Do not store transient task state, agent reasoning, or implementation chatter in `PRODUCT.md`.
<!-- meaningfall:product-memory v1 end -->
```

`meaningfall:product-memory v1` is the snippet generation, not an ownership claim and not the Build Flow package version.

If the user opts out, say:

```text
I will not create or update AGENTS.md. Product memory is still installed, but future agents may need to be told manually to read PRODUCT.md and product-memory/README.md.
```

## Install Gate

Before finishing a new install, verify:

- `PRODUCT.md` exists or is output as a complete fenced block when file writing is unavailable.
- `product-memory/README.md` exists or is output as a complete fenced block.
- Supporting files exist only when populated.
- Supporting files contain only sections with content.
- `product-memory/state.yaml` does not exist.
- `product-memory/archive/` does not exist unless there is superseded or historical material.
- `AGENTS.md` was created or updated with the marked block, or the user opted out.
- The handoff names the created files, supporting files intentionally not created, review needs, known `TBD`s, deferred material, and safest next action.

## Scoped Updates

For a scoped update to an existing product with installed product memory:

- preserve existing product-memory files;
- update only the requested product scope and any earlier product meaning the update makes necessary;
- create a supporting file only when new persistent material belongs there;
- do not reinstall the whole product-memory surface unless the user explicitly asks.

For an existing repository with `PRODUCT.md` but no `product-memory/`, do not silently install `product-memory/` by default. Treat that as future Setup pressure unless the user explicitly asks Product Brief to install memory.

## Non-Goals

This contract does not:

- define the ProductMD format;
- replace `references/verification.md`;
- design the full Memory lifecycle, Reconcile, or Impact;
- define AGENTS repair, migration, or uninstall behavior;
- create a public Memory package;
- publish empty templates for installed product memory.
