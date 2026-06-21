# Product Memory Install Contract

Contract generation: **install-contract v1.1**.

This reference is the operational source of truth for Product Brief's product-memory install behavior. `SKILL.md` carries the runnable interview and skill flow; this file carries the detailed install contract and install gate. ProductMD format rules remain in the ProductMD spec and `references/verification.md`.

## Install Shape

For a new product, Product Brief installs:

```text
PRODUCT.md
product-memory/
  README.md
  notes.md       # create-on-need
  facts.md       # create-on-need
  drafts.md      # create-on-need
  decisions.md   # create-on-need
  learnings.md   # create-on-need
  glossary.md    # create-on-need
  archive/       # lazy, first supersession
AGENTS.md        # default-on approval-visible integration; host-owned
```

Always create:

- `PRODUCT.md` — canonical product truth.
- `product-memory/README.md` — role map, read order, and install attribution.

Create only when populated:

- `product-memory/notes.md` — loose remembered context that is worth saving but is not yet verified, decided, or structured.
- `product-memory/facts.md` — project or external context treated as true, when it is useful supporting memory and not already better placed in `PRODUCT.md`.
- `product-memory/drafts.md` — isolated sandboxes for thinking through candidate product direction or project-memory changes.
- `product-memory/decisions.md` — committed choices with rationale, especially when the why compresses a longer AI-assisted discussion.
- `product-memory/learnings.md` — rare reusable process insights that should influence future drafts or decisions.
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

## Product-Design Memory Model

Use product-design language for supporting memory. Avoid technical AI-memory categories when a product-work term is clearer.

Active supporting memory uses these objects:

- **Note** — a loose piece of remembered context. It may be a thought, reminder, observation, or weakly shaped information. It is worth saving but not necessarily verified, decided, or structured.
- **Fact** — something treated as true in the project: reality, current state, known information, or external/project context. Product-changing facts belong in `PRODUCT.md`; `facts.md` is for useful supporting context that should not become a shadow product spec.
- **Draft** — a sandbox for thinking, discussing, testing, and shaping a topic. A draft is not a required pipeline stage before a decision. It can evolve over many iterations and can stay isolated from main product memory until it is ready.
- **Decision** — an independent committed memory chunk. Decisions are useful compression for AI-assisted conversations: instead of rereading the whole dialogue, future work can recover what was chosen, why, and what effect it has.
- **Learning** — a reusable insight from process, discussion, testing, failure, rejection, comparison, cancellation, or integration work. A learning should influence future work, but it is not itself a decision.

Archive is not an active memory object. Archive stores the path: old versions, full iteration logs, rejected or superseded material, raw discussion traces, and historical routes that should remain searchable without automatically guiding future work.

The model is a network, not a pipeline. Drafts are thinking spaces, decisions are committed chunks, learnings are reusable insights, facts describe reality, notes capture loose context, and archive preserves historical traces.

## Draft Lifecycle

Drafts are isolated sandboxes. A user or AI can open a draft for a topic without polluting `PRODUCT.md` or the rest of active product memory.

A substantial draft should keep:

- current version;
- current summary;
- open questions;
- related notes, facts, decisions, and learnings;
- a link or reference to archived iteration logs when those logs are worth preserving.

Keep the full draft iteration log in `archive/`, not active memory. Active draft memory should keep only the current useful version and a compact evolution summary.

Allowed draft statuses are:

- `isolated` — captured but not yet connected to active product memory;
- `active` — currently being explored;
- `reviewed` — examined and ready for acceptance, return, rejection, or split;
- `accepted` — approved as a good proposal or direction;
- `integrating` — being applied to `PRODUCT.md` or supporting memory;
- `integrated` — successfully applied;
- `returned` — accepted, but integration did not succeed yet;
- `rejected` — not accepted as direction;
- `superseded` — replaced by a newer draft or decision;
- `archived` — no longer active; preserved historically.

Acceptance and integration are separate:

- **Acceptance** means the draft is approved as a good proposal or direction.
- **Integration** means the accepted draft was successfully applied to product memory.

A returned draft means: the proposal was accepted, but merging it into the product memory did not succeed yet. Common return reasons are conflict with an existing decision, missing dependency, scope that needs splitting, failed implementation, context mismatch, or a need to convert the draft into smaller notes, facts, decisions, or learnings.

## Decision Lifecycle

Decisions are independent atomic memory chunks. A decision may relate to drafts, notes, facts, learnings, archive entries, or other decisions, but it does not have to belong to a draft.

A decision may happen:

- directly, without a draft;
- during draft work;
- after reviewing a draft;
- after a learning;
- after cancelling an old decision;
- after discovering a conflict.

A useful decision record includes title, decision, status, rationale, effect, scope, origin, related drafts, related notes/facts/learnings, and supersedes or cancels links where applicable.

Use status values such as:

- `active` — the decision currently guides work;
- `superseded` — replaced by a newer decision;
- `cancelled` — explicitly withdrawn or reversed;
- `archived` — preserved historically and no longer active.

Do not delete old decisions when they stop guiding work. Mark them cancelled, superseded, or archived. Cancelling a decision is meaningful: it can create uncertainty, launch a new draft, or produce a new decision.

Decision cancellation pattern:

```text
decision cancelled
  -> uncertainty created
  -> optional draft explores replacement direction
  -> new decisions, facts, notes, or learnings emerge
```

## Rationale And Learning

Rationale is local to a decision. It answers: why did this choice make sense at that time?

Learning is reusable beyond one decision. It answers: what did the process teach us that should influence future work?

Example:

- Decision: Use notes, facts, drafts, decisions, and learnings as the active product-memory concepts.
- Rationale: These terms fit product-design work better than technical AI-memory labels.
- Learning: Designer-facing AI-memory systems should use process-native product-design language where possible.

## Archive Rules

Archive stores historical paths that should remain searchable but should not automatically guide future work.

Use `archive/` for:

- full draft iteration logs;
- old draft versions;
- rejected drafts when the rejection path is useful;
- superseded notes, facts, and learnings;
- cancelled or superseded decisions;
- raw discussion traces;
- historical alternatives that may help recovery, audit, or future comparison.

Do not archive every tiny edit. Archive material when losing the artifact would make future recovery, explanation, or comparison meaningfully harder.

## Creation-Time Classification

Use these placement rules when Product Brief captures material that should persist:

- Current accepted product meaning -> `PRODUCT.md`.
- Accepted but open product meaning -> `PRODUCT.md` as `TBD` or a recorded assumption only when a consumer must know that the slot exists even while the value is open.
- Loose context, observations, reminders, weak signals, deferred material, future scope, not-now material, or rejected-but-useful material with no target change -> `product-memory/notes.md`.
- Supporting project or external facts that matter but should not be canonical product truth -> `product-memory/facts.md`.
- Candidate direction, topic exploration, or a proposal sandbox -> `product-memory/drafts.md`.
- Accepted choices with useful rationale -> `product-memory/decisions.md`.
- Reusable process insights that should influence future work but are not choices -> `product-memory/learnings.md`.
- Terms, aliases, rejected names, and naming distinctions -> `product-memory/glossary.md`.
- Source or provenance -> inline by role in `PRODUCT.md`, `facts.md`, `decisions.md`, `drafts.md`, `learnings.md`, or `notes.md`; do not create a separate ledger.

Rejected terminology goes to `glossary.md`; rejected product direction or approach goes to `notes.md` when it remains useful.

Do not hide accepted product truth in supporting memory. Do not turn `PRODUCT.md` into a question list; a `TBD` belongs there only when the slot itself changes what gets built or flags a required decision.

## `product-memory/README.md`

Create this file for every new install:

```md
# Product Memory

`../PRODUCT.md` is the canonical accepted product truth.

This folder holds supporting product memory: notes, facts, drafts, decisions, learnings, glossary, and archive.

Installed by Meaningfall Product Brief.

Supporting files are created when there is content for them. Missing files mean there is no recorded material for that role yet.

This memory is yours to edit, extend, or prune as your project needs.

## Read Order

1. Read `../PRODUCT.md`.
2. Read this file for memory roles.
3. Read `glossary.md` if it exists and terms or names matter.
4. Read `facts.md` if it exists and supporting project or external context matters.
5. Read `notes.md` and `drafts.md` if they exist and unresolved, future, or in-progress context matters.
6. Read `decisions.md` and `learnings.md` if they exist and rationale or reusable insight matters.
7. Read `archive/` only if it exists and historical, recovery, or audit work requires it.

## Surfaces

- `notes.md` — loose context, observations, reminders, weak signals, unresolved or deferred material.
- `facts.md` — supporting project or external facts that matter but do not replace `PRODUCT.md`.
- `glossary.md` — canonical terms, aliases, rejected names, distinctions.
- `drafts.md` — isolated proposal and topic sandboxes with compact current summaries.
- `decisions.md` — committed choices with rationale and effect.
- `learnings.md` — rare reusable insights from the work process.
- `archive/` — old versions, full iteration logs, rejected or superseded material, and other historical traces; created on first need.
```

## Supporting File Sketches

These are maximal references, not templates. Instantiate only the files and sections that have content. Never create a file or heading just because it appears here.

### `notes.md`

```md
# Notes

Loose product memory.

## Deferred

- Team pricing is plausible, but not part of the first build.
```

### `facts.md`

```md
# Facts

Supporting facts treated as true for this project. Product-changing facts also belong in `../PRODUCT.md`.

## Market Context

- The first release is aimed at solo designers and small product teams, not enterprise design ops.
```

### `decisions.md`

```md
# Decisions

## 2026-06-19 — First Scope

Status: active

Decision: Start with individual workspaces before team workspaces.

Rationale: The first useful version can prove the core workflow without account administration.

Effect: Team roles and administration stay out of the first `PRODUCT.md` scope.

Origin: Product Brief interview.
```

### `drafts.md`

```md
# Drafts

## Team Workspace Model

Status: active

Current version: Add team workspaces to `map.product`.

Current summary: Team workspaces may be needed after individual workspaces prove the core workflow.

Open question: Whether team roles are fixed or configurable.

Related decisions:
- 2026-06-19 — First Scope

Archive: `archive/team-workspace-model-log.md` if a full iteration log is later worth preserving.
```

### `learnings.md`

```md
# Learnings

Reusable insights from the work process, not choices.

## Product Language

Learning: Product designers respond better to process-native terms such as note, draft, decision, and learning than to technical AI-memory categories.

Use when: Naming future memory surfaces, prompts, or review flows.
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

Use `product-memory/README.md` for the supporting memory read order and file roles. Supporting memory may provide notes, facts, drafts, decisions, learnings, terminology, and parked material, but it does not override `PRODUCT.md` on product truth.

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
- implement Reconcile, Impact, migration, or repair workflows;
- define AGENTS repair, migration, or uninstall behavior;
- create a public Memory package;
- publish empty templates for installed product memory.
