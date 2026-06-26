# Product Memory Install Reference

Contract generation: **install-contract v1.2**.

This reference is the operational source for the Install skill's
`product-memory` target. ProductMD format rules remain in the ProductMD spec.
Install-independent product-memory governance lives in the Memory spec at
`../../../modules/memory/spec.md`.

## Install Shape

For a new product, Install creates or updates:

```text
PRODUCT.md
product-memory/
  README.md
  notes.md       # create-on-need single Markdown file
  drafts/        # create-on-need, one file per substantial unresolved topic
  decisions/     # create-on-need, one file per accepted decision record
  glossary.md    # create-on-need single Markdown file
  archive/       # lazy, first supersession
AGENTS.md        # default-on approval-visible integration; host-owned
```

Always create:

- `PRODUCT.md` — canonical product truth.
- `product-memory/README.md` — role map, read order, and install attribution.

Create supporting memory surfaces only when Memory classification produces content
for that role:

- `product-memory/notes.md` — single Markdown file, no record metadata.
- `product-memory/drafts/` — one file per substantial topic, YAML front matter.
- `product-memory/decisions/` — one file per accepted decision, YAML front matter.
- `product-memory/glossary.md` — single Markdown file, no record metadata.

Create lazily:

- `product-memory/archive/` — only when there is already superseded or historical
  material worth recovering.

Do not create:

- `product-memory/state.yaml`;
- a default `facts.md` or `learnings.md` support surface; facts and learnings route
  by role per the Memory spec;
- empty supporting files;
- empty headings inside supporting files;
- a live `product-memory/` folder under the public repository tree.

## Governance Source

Install owns install mechanics: what it creates, when supporting files are
created, the generated `product-memory/README.md`, approval-visible `AGENTS.md`
integration, the install gate, how the skill applies classification while
capturing material, and scoped update behavior.

Memory owns install-independent governance: authority, supporting-memory role
meanings, read-order principle, classification, lightweight lifecycle, conflict
handling, non-goals, and source ownership. See
`../../../modules/memory/spec.md`.

## Creation-Time Classification

Use the Memory spec's classification rules when Install captures material that
should persist.

Install-specific capture rules:

- Keep interview state (`supplied`, `accepted`, `inferred`, `TBD`, `excluded`, or
  `deferred`) in working memory or the caller's handoff, not as durable file
  metadata.
- Create a supporting file only when captured material remains after Memory
  classification.
- Put source or provenance inline in the destination selected by Memory; do not
  create a separate source ledger.
- Treat practices or principles from external prompts as optional review input, not
  product truth. They become product memory only when accepted for this product and
  routed through Memory classification.
- Do not hide accepted product truth in supporting memory.

## `product-memory/README.md`

Create this file for every new install:

```md
# Product Memory

`../PRODUCT.md` is the canonical accepted product truth.

This folder holds supporting product memory: notes, drafts, decisions, glossary, and archive.

Installed by Meaningfall Install.

Supporting surfaces are created when there is content for them. Missing surfaces mean there is no recorded material for that role yet. This file is a role map, not a hand-maintained list of every record.

This memory is yours to edit, extend, or prune as your project needs.

## Read Order

1. Read `../PRODUCT.md`.
2. Read this file for memory roles.
3. Read `glossary.md` if it exists and terms or names matter.
4. Read `notes.md` and `drafts/` if they exist and unresolved, future, or in-progress context matters.
5. Read `decisions/` if it exists and rationale or accepted-choice history matters.
6. Read `archive/` only if it exists and historical, recovery, or audit work requires it.

## Surfaces

These role meanings follow the Meaningfall Memory spec.

- `notes.md` — loose context, observations, reminders, weak signals, unresolved or deferred material. Simple Markdown, no record metadata.
- `drafts/` — candidate direction, topic exploration, and proposal sandboxes; one file per substantial topic, with YAML front matter.
- `decisions/` — accepted choices with rationale and effect; one file per decision, with YAML front matter. A reusable lesson is a decision with `type: learning`.
- `glossary.md` — terms, aliases, rejected names, and naming distinctions. Simple Markdown, no record metadata.
- `archive/` — superseded or historical material worth recovery; created on first need.
```

## Surfacing Repeated Material

Install delivers a suggestion-only capture discipline. It adds no capture engine,
command, or state file. The governing rule is owned by the Memory spec
(`../../../modules/memory/spec.md`); this section is local operating text and is
not an activation of Reconcile or Impact.

When an agent notices the human repeating the same project-level instruction,
correction, preference, or workflow across more than one task in a way that looks
durable — not a one-off for the current task — it should offer to record it so the
human need not repeat it.

This is suggestion-only and approval-visible:

- never record silently;
- state, briefly, the repeated pattern that was observed;
- propose one destination and a one-line reason for it;
- propose the exact text or diff to be written;
- record only on explicit approval; on silence or ambiguity, do not record;
- if the human declines, do not raise the same pattern again.

Route by role using Memory classification and the Principles-MD discriminator.
The targets below are common applications of that classification, not a separate
authority; do not maintain a competing routing table elsewhere:

- an agent operating instruction -> the host-owned body of `AGENTS.md`, as an
  approved edit to the human's own file, never inside the marked Meaningfall block;
- an accepted choice with rationale and a specific effect -> a record in
  `product-memory/decisions/`;
- a reusable process insight from a past episode -> a decision record in
  `product-memory/decisions/` with `type: learning`;
- a standing judgment disposition -> `PRINCIPLES.md`, only if it already exists or
  the human wants one;
- durable product truth -> a focused `PRODUCT.md` diff;
- a weak, deferred, or not-yet-durable preference -> `product-memory/notes.md`; a
  naming choice -> `product-memory/glossary.md`.

Captured operating instructions belong to the host, so they go in the host region
of `AGENTS.md`. The marked Meaningfall block stays a thin pointer to this
behavior; it does not accumulate captured rules. The behavior is default-on but
may be opted out for any reason, including host or organization policy; opt-out
suppresses the suggestions, not product-memory install.

## AGENTS.md Integration

Install should create or update `AGENTS.md` with a small marked
product-memory block by default unless the user opts out.

This is approval-visible:

- explain that the edit is recommended so future agents can discover product memory;
- if `AGENTS.md` exists, update only the marked Meaningfall block and leave unrelated host instructions unchanged;
- when updating, replace a found `meaningfall:product-memory v1` block with the
  current `v2` block;
- if `AGENTS.md` does not exist, create it as the project's agent-instruction file, not as a Meaningfall-owned file;
- respect opt-out for any reason, including host or organization policy.

Recommended block:

```md
<!-- meaningfall:product-memory v2 start -->
## Meaningfall Product Memory

Before changing durable product meaning, read `PRODUCT.md` first.

Use `product-memory/README.md` for the supporting memory read order and file roles. Supporting memory may provide notes, drafts, decisions, terminology, and parked material, but it does not override `PRODUCT.md` on product truth.

If supporting memory seems to conflict with `PRODUCT.md`, surface the conflict rather than silently choosing.

For durable product-meaning changes, propose a focused `PRODUCT.md` diff. Do not store transient task state, agent reasoning, or implementation chatter in `PRODUCT.md`.

If you notice the human repeating the same project-level instruction, correction, preference, or workflow across more than one task in a way that looks durable, offer to record it so they need not repeat it. Ask first, propose where it should live and the exact wording, and never record it silently. Route an agent operating instruction into this `AGENTS.md` file outside this Meaningfall block; route durable product material into `PRODUCT.md` or `product-memory/` by role. If the human declines, do not raise the same suggestion again.
<!-- meaningfall:product-memory v2 end -->
```

`meaningfall:product-memory v2` is the snippet generation, not an ownership claim
and not a version of Guide, Memory, any module, or any skill.

If the user opts out, say:

```text
I will not create or update AGENTS.md. Product memory is still installed, but future agents may need to be told manually to read PRODUCT.md and product-memory/README.md.
```

## Install Gate

Before finishing a new install, verify:

- `PRODUCT.md` exists or is output as a complete fenced block when file writing is unavailable.
- `product-memory/README.md` exists or is output as a complete fenced block.
- Supporting surfaces exist only when populated.
- `notes.md` and `glossary.md`, when created, are single Markdown files with content and no record metadata.
- Created `drafts/` and `decisions/` records carry YAML front matter with a `status` from the closed enum for that surface.
- No default `facts.md` or `learnings.md` support surface is created.
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

For an existing repository with `PRODUCT.md` but no `product-memory/`, do not
silently install `product-memory/` by default. Treat that as future setup pressure
unless the user explicitly asks Install to install memory.

## Non-Goals

This contract does not:

- define the ProductMD format;
- define Memory governance;
- implement Reconcile, Impact, migration, or repair workflows;
- define AGENTS repair, migration, or uninstall behavior;
- publish empty templates for installed product memory.
