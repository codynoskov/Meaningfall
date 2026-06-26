# Memory Spec

Status: accepted module contract.

This spec follows root [`SPEC.md`](../../SPEC.md). It inherits the root
public-surface and contract rules, and narrows or extends them only where this spec
says so explicitly.

## Purpose

Memory governs how accepted product truth becomes and stays usable over time.

It works around `PRODUCT.md`, the canonical product-truth file defined by ProductMD,
and around supporting `product-memory/` surfaces in an installed workspace.

Memory does not replace ProductMD. ProductMD defines the `PRODUCT.md` format. Memory
governs how product truth is buffered, reviewed, committed, explained, and protected
from drift.

Memory is usable without Guide or Install. Guide is a guided
creation skill, and Install is an install skill. They apply this contract;
they are not the source of Memory's model.

## Authority

`PRODUCT.md` is the Product Definition: the current authoritative product
definition. "Product truth" and "canonical product truth" are descriptive aliases
for this surface, not separate surfaces.

Supporting memory is lower authority, not no authority. Each supporting surface is
authoritative for its own role:

- notes preserve loose context;
- drafts preserve candidate direction;
- decisions preserve rationale and effect;
- glossary preserves naming and terminology;
- archive preserves useful history.

Supporting memory does not override `PRODUCT.md` on product meaning. A
product-changing decision, fact, or draft outcome must be reflected in `PRODUCT.md`
before it becomes current product truth.

## Surface Classes

Meaningfall memory distinguishes these surface classes:

- **Product Definition** — `PRODUCT.md`, the current authoritative product
  definition.
- **Guidance** — host-owned `AGENTS.md`, and optional `PRINCIPLES.md` when the
  project uses scoped judgment guidance.
- **Memory Index** — `product-memory/README.md`, the local read-order and role
  map. It is not a hand-maintained list of every draft or decision; the filesystem
  is the record listing.
- **Memory Records** — active supporting memory: `notes.md`, `drafts/`,
  `decisions/`, and `glossary.md`. Record metadata is a property of folder-backed
  records only, not of the class as a whole.
- **Cold Archive** — `product-memory/archive/`, a read-on-need historical store,
  not an active record type.

A memory transition is an edit that changes what a future reader or agent would
treat as true, decided, deferred, open, rejected-but-useful, in-progress, or ready
to ignore — for example a note becoming a draft, a draft being promoted or
rejected, a decision being superseded, Product Definition material moving into
`PRODUCT.md`, an operating instruction being approved for `AGENTS.md`, or a term
moving into `glossary.md`.

## Supporting Surfaces

Product memory uses visible, create-on-need files. The conventional installed
surface is:

```text
PRODUCT.md
product-memory/
  README.md      # Memory Index: local read order and role map
  notes.md       # create-on-need single Markdown file
  drafts/        # create-on-need, one file per substantial unresolved topic
  decisions/     # create-on-need, one file per accepted decision record
  glossary.md    # create-on-need single Markdown file
  archive/       # Cold Archive, lazy: first supersession or historical need
AGENTS.md        # host-owned guidance; not part of product memory
```

This tree is the Memory surface model. An installer may decide exactly which files
to create at setup time, but it must preserve these role meanings if it claims to
install Meaningfall product memory.

Use folders only where a surface naturally scales into many separate records and
benefits from selective loading: `drafts/` and `decisions/`. Keep `notes.md` and
`glossary.md` as single Markdown files.

Missing support files mean there is no recorded material for that role yet. Do not
create empty support files, empty headings, or empty archive folders. Do not
install `product-memory/state.yaml`. Do not install `facts.md` or `learnings.md`
as default support surfaces; facts and learnings route by role (see
Classification).

`AGENTS.md` may point agents to product memory, but it is not part of product
memory. The host project owns `AGENTS.md`.

Do not create a live `product-memory/` folder under the public repository tree.
The public repository may show installed product memory only as clearly marked
examples, not as live public structure.

Memory must work without version control. Git is an enhancement, not a dependency.
Use readable memory surfaces for current meaning and recoverable context, and
`archive/` for historical material a future reader should find without version
control; use Git, when available and allowed, for the ordered audit trail. Archive
and Git are not substitutes: if no Git history is available, cleanup must still
avoid losing the only useful copy of material. The Git Hygiene skill owns the
accepted installed-user Git behavior — read-only detection and suggested or
explicit checkpoints under Action Modes (decision 0071); `git init`, Git
configuration, hooks, auto-commit, and history rewriting stay off by default and
are never required by Memory.

## Read Order

Memory is read from canonical truth outward, then from stable support to more
tentative support:

1. Read `PRODUCT.md`.
2. Read `product-memory/README.md` if it exists, for local read order and role
   reminders.
3. Read `product-memory/glossary.md` if terms, aliases, or naming distinctions
   matter.
4. Read `product-memory/notes.md` and `product-memory/drafts/` if unresolved,
   future, not-now, or in-progress context matters.
5. Read `product-memory/decisions/` if rationale or accepted-choice history
   matters.
6. Read `product-memory/archive/` only for historical, recovery, audit, or
   comparison work.

Local `product-memory/README.md` files may restate or narrow this order for a
specific workspace. They must not make supporting memory override `PRODUCT.md`.

## Classification

Classify durable material by authority and role:

- Current accepted product meaning belongs in `PRODUCT.md`.
- Accepted but still-open product meaning belongs in `PRODUCT.md` as `TBD` or a
  recorded assumption only when a consumer must know the slot exists while the
  value is open.
- Loose context, observations, reminders, weak signals, deferred material, future
  scope, not-now material, or rejected-but-useful material with no target change
  belongs in `product-memory/notes.md`.
- Candidate direction, topic exploration, or proposal sandboxes belong in
  `product-memory/drafts/`, one file per substantial topic.
- Accepted choices with useful rationale belong in `product-memory/decisions/`,
  one file per decision.
- Terms, aliases, rejected names, and naming distinctions belong in
  `product-memory/glossary.md`.
- Superseded or historical material worth recovery belongs in
  `product-memory/archive/`, created only on first need.
- Source or provenance belongs inline by role in `PRODUCT.md`, `notes.md`, a
  draft, or a decision; do not create a separate ledger by default.

Facts and learnings are not default Memory Record surfaces. Route them by effect:

- a fact that changes what the product is, does, promises, supports, excludes, or
  prioritizes belongs in `PRODUCT.md`; a weak, uncertain, deferred, situational, or
  speculative fact belongs in `notes.md` or `drafts/`; stable accepted non-product
  context may remain in `notes.md`; factual evidence for a choice belongs in that
  decision's rationale or references.
- a reusable accepted lesson that should shape future behavior is a decision record
  with `type: learning`; a lesson that changes Product Definition moves to
  `PRODUCT.md`; a lesson that changes agent operating behavior is routed to
  host-owned `AGENTS.md` after approval; a lesson that changes nothing stays in
  `notes.md` or is discarded.

Rejected terminology goes to `glossary.md`; rejected product direction or approach
goes to `notes.md` when it remains useful.

Do not hide accepted product truth in supporting memory. Do not turn `PRODUCT.md`
into a question list; a `TBD` belongs there only when the slot itself changes what
gets built or flags a required decision.

## Surfacing Repeated Material

When an agent notices the human repeating the same project-level instruction,
correction, preference, or workflow across more than one task in a way that looks
durable, it should offer to record it in the appropriate durable place. This is
suggestion-only: never record silently, propose the destination and exact wording
first, and record only on explicit approval.

Route the material by the classification rules above and by the Principles-MD
discriminator when scoped judgment guidance is involved. Agent operating
instructions belong to the host-owned `AGENTS.md`; durable product truth belongs
in `PRODUCT.md`; weak, deferred, or not-yet-durable material belongs in
`notes.md`; naming choices belong in `glossary.md`.

If the human declines a suggestion, do not raise the same pattern again. This
discipline adds no installed files, commands, reports, or state, and is not an
activation of future Reconcile or Impact behavior.

## Lifecycle Basics

Notes are parking. They hold loose, deferred, unresolved, not-now, or
rejected-but-useful context. They are not a workflow queue and not a second canon.

Drafts are candidate sandboxes. A draft direction can be approved — in conversation
or by a decision — before it is promoted or integrated. Approval endorses the
direction; integration applies the change to `PRODUCT.md` or supporting memory.

Decisions preserve rationale and effect. They explain why a choice was made. They
do not replace `PRODUCT.md` as the current product-truth surface.

Archive preserves useful historical paths. It is not read by default, not a
changelog, and not a replacement for Git history.

## Memory Records Format

Folder-backed records use YAML front matter as the single metadata mechanism.
`notes.md` and `glossary.md` are simple Markdown files and carry no record
metadata.

Decision records use:

```yaml
status: accepted   # accepted | deprecated | superseded
type: product      # product | technical | workflow | guidance | naming | rejection | learning | <project-defined>
topic:
  - memory
```

`status` is a closed enum. `type` has recommended base values and allows a
project-defined extension. `topic` is free-form retrieval tags. Optional fields,
only when useful, are `source_drafts`, `supersedes`, and `superseded_by`. A
decision body should include `## Decision`, `## Rationale`, and `## Effect`; for
`type: learning`, `## Lesson` may replace `## Decision` and `## Effect` may be
brief.

Draft records use:

```yaml
status: open       # open | paused | promoted | rejected | superseded
type: proposal     # proposal | exploration | research | migration | audit | planning | <project-defined>
topic:
  - memory
```

`status` is a closed enum. `type` has recommended base values and allows a
project-defined extension. Optional fields, only when useful, are `promoted_to`,
`source_notes`, `result_decisions`, `supersedes`, and `superseded_by`. The draft
body is permissive Markdown with no required schema. A draft moves to `promoted`
only when its central question is fully resolved into owning surfaces; partial
promotion keeps the draft `open` and records produced targets through optional
links.

Draft and decision `type` values are surface-specific and need not match; `topic`
is the shared filtering axis across records. Glossary entries need only a term
heading and definition; optional aliases, rejected names, usage notes, related
terms, or links to naming decisions may follow.

Draft, decision, and implementation flow is non-linear: a decision may appear
without a prior draft, one draft may produce several decisions, a draft may stay
open while producing decisions, and implementation is a separate transition.
Implementation evidence stays in prose until there is a concrete consumer for
structured `implements` / `implemented_by` fields.

Installed folder-backed records use YAML front matter; there is no Markdown
`## Status` grandfather exemption for installed product memory.

## Archive Lifecycle

`archive/` is Cold Archive: created lazily, on first supersession or first
historical need.

- A draft is archived only when its alternatives or deliberation remain useful;
  otherwise a rejected draft is removed, or its useful direction is parked in
  `notes.md`.
- A `status: deprecated` or `status: superseded` decision stays an active record in
  `decisions/`; it moves to `archive/` only when it is no longer useful to read in
  place and its deliberation is worth preserving as an artifact.
- Notes are archived when they are obsolete but worth preserving; otherwise they
  are cleaned up.
- Retired glossary names stay in `glossary.md` as rejected-name entries; they are
  not archived per term.
- Archive is not read by default, is not a changelog, and is not a replacement for
  Git history. Git stores ordinary diffs; archive stores material that would
  otherwise be lost as meaningful context. Do not archive every small edit.

Archive moves are `suggested` under Action Modes; they are not silent.

## Conflict Rule

If supporting memory appears to conflict with `PRODUCT.md`, surface the conflict
instead of silently choosing.

A good conflict report usually states:

- the `PRODUCT.md` meaning involved;
- the supporting memory that appears to disagree;
- the likely consequence of choosing one reading over the other;
- the smallest focused decision or edit needed to resolve it.

Do not update durable product meaning by hiding the conflict in notes, decisions,
drafts, or implementation work.

## Installer Boundary

Memory owns the product-memory surface model and governance. Installers own the
mechanics of creating or updating files in a concrete workspace.

Install's `product-memory` target is the current public installer for
product-memory setup. It owns the exact generated `product-memory/README.md`
content, approval-visible `AGENTS.md` integration mechanics, install gate, and
scoped-update behavior for that target.

An installer may restate Memory rules only as local operating text. If the
installer and this spec conflict about product-memory governance, this spec wins.

## Boundaries And Future Direction

Memory may later support Reconcile and Impact behavior.

Reconcile means reality back to memory: code, design, docs, shipped behavior, or
user observation raises the question of whether `PRODUCT.md` or supporting memory
should change.

Impact means memory forward to work: a `PRODUCT.md` or product-memory change raises
the question of what code, design, tests, docs, or tasks are affected.

For now, Reconcile and Impact are future-facing definitions. They do not require
installed files, reports, commands, statuses, or algorithms.

## Planning Readout

Memory surfaces support an advisory "what next" readout (decision 0073). When the
human asks what to do next, read `PRODUCT.md`, `notes.md`, `drafts/`, `decisions/`,
and visible implementation state, and synthesize next-step candidates. Distinguish
at least: promising next topics; blocked or unresolved questions; user-stated
commitments or deadlines (from notes, not product truth); deferred ideas worth
revisiting; stale or rejected directions not to revive casually; and concrete gaps
already implied by a decision or `PRODUCT.md`. Ground each candidate in a specific
surface, and mark a candidate promising only when a surface supports it.

The readout is advisory only: it creates no tasks, installs no `roadmap.md`, board,
or ticket system, and performs no memory transition. Any resulting change is a
normal memory transition under Action Modes. If the project already has a host task
system, issue tracker, roadmap, or planning tool, read and respect it instead of
creating a competing surface.

This is a Memory read capability, not a separate installed surface, skill, or
command.

## Action Modes

Per root `SPEC.md` Action Modes and decision 0072, Memory grants:

- `suggested`: capture of repeated durable human instructions; moving notes into
  drafts, decisions, Product Definition, glossary, or guidance; notes cleanup after
  promotion; archive moves.
- `explicit`: durable `PRODUCT.md` changes; approved `AGENTS.md`
  operating-instruction edits.

These are memory transitions; none happens silently. Git checkpoints for these
transitions are owned by the Git Hygiene skill.

## Non-Goals

Meaningfall Memory is not:

- a task board;
- a roadmap;
- an ADR clone;
- a vector store;
- native AI-client memory;
- a hidden state file;
- a workflow engine;
- a replacement for `PRODUCT.md`;
- a replacement for the ProductMD spec;
- a place to copy private workspace process structure into user projects.

Do not create structure ahead of need. Do not add empty product-memory files,
empty module folders, hidden manifests, or speculative local tooling surfaces.

## Source Ownership

- ProductMD owns the `PRODUCT.md` format.
- Memory owns product-truth-over-time governance.
- Guide owns guided creation.
- Install owns install mechanics.

Reference, do not restate. If these artifacts conflict, resolve by ownership.
