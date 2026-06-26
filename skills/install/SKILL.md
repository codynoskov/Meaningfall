---
name: install
description: Install or update Meaningfall surfaces in a concrete workspace by applying the owning public contracts. Use when a user asks to install, initialize, set up, repair, or check installed Meaningfall files such as Product Memory around PRODUCT.md, product-memory/README.md, create-on-need supporting memory files, or approval-visible AGENTS.md integration.
---

# Install

Install applies Meaningfall contracts to a workspace. It owns install
procedure, not product meaning or module governance.

Supported target:

- **product-memory** — install or update the visible product-memory surface around
  `PRODUCT.md`.

Future targets may be added here as Meaningfall gains more installable surfaces.

## Workflow

1. Identify the install target. If the user does not name one, infer the narrowest
   target from the request.
2. Read the target reference before changing files.
3. Read the owning format or module contracts named by the target reference.
4. Apply only the requested install/update/repair scope.
5. Preserve host-owned material and unknown local instructions.
6. Run the target install gate.
7. Report created, updated, skipped, and intentionally absent files.

## Targets

### product-memory

Use `references/product-memory.md` when installing or checking product memory.

This target applies:

- ProductMD for `PRODUCT.md`;
- Memory for product-memory governance;
- the target reference for exact install mechanics.

Do not create supporting memory files unless they have content. Do not install
`product-memory/state.yaml`. Treat `AGENTS.md` as host-owned operating guidance.

## Action Modes

Per root `SPEC.md` Action Modes and decision 0072, Install grants:

- `automatic`: read-only detection of existing `PRODUCT.md`, `product-memory/`, and
  host-owned `AGENTS.md`.
- `suggested` (approval-visible): default-on install steps and the marked
  `AGENTS.md` product-memory block edit; the human sees and can opt out.
- `explicit`: edits to host-owned `AGENTS.md` outside the marked block.
