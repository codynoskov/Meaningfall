# Meaningfall Repository Spec

Status: accepted repository-level contract.

Meaningfall uses visible repository files to preserve product meaning, guide product creation, and keep public product behavior inspectable.

This spec governs the public Meaningfall repository as a product-family repository. It defines repository-level public surface conventions and the contract system between public Meaningfall parts. It does not define an installed user workspace by itself.

Format specs, module specs and procedures, skill procedures, and install
references should state or imply their relationship to this root contract without
copying it.

## Public Product Standard

Everything in this public repository is public product material. It should be
compact, intentional, and good enough to stand without private context.

Do not place internal laboratory memory, private planning, chat-derived rationale,
unaccepted drafts, speculative scaffolding, or process-only instructions in public
Meaningfall files. Public surfaces should be complete enough to use, but no larger
than their role requires.

## Public Surface Types

Public Meaningfall surfaces have distinct roles:

- `README.md` is an entry point and router.
- `SPEC.md` and `spec.md` are normative contracts.
- `SKILL.md` is executable agent procedure.
- `references/` holds detailed support material for a format, module, or skill.
- `scripts/` holds executable helper code bundled with a skill or executable module.
- `assets/` holds templates, media, icons, or other files used by outputs.
- `agents/` holds optional client-specific skill metadata. It is not normative and
  must not be required to understand or execute a skill.
- `examples/` holds illustrative material, not normative rules unless a spec explicitly makes an example normative.
- `CHANGELOG.md` records release history, not current normative behavior.
- `NOTICE`, `LICENSE`, and `CONTRIBUTING.md` are repository metadata and contribution surfaces.
- `AGENTS.md` is agent operating guidance, not product truth.
- `index.yaml` is a machine-readable repository map, not narrative authority.
  Verify may check public repository surface coherence against it, but that
  check does not create a second authority beside owning contracts.
- `PRINCIPLES.md` holds scoped judgment guidance when the Principles-MD contract
  says the scope is appropriate.
- decisions record accepted rationale, not public product specification by themselves.

Public Meaningfall surfaces must be understandable from public files alone. Do not require unpublished notes, hidden state, chat history, planning material, or development paths to understand a public product, skill, example, or install contract.

## Specification Hierarchy

Root `SPEC.md` defines shared repository conventions.

Format specs define file-format contracts:

```text
formats/<format>/spec.md
```

Module specs and procedures define governed capabilities and reusable disciplines:

```text
modules/<module>/spec.md
modules/<module>/SKILL.md
modules/<module>/references/
```

Root skill procedures define user-facing callable workflows:

```text
skills/<skill>/SKILL.md
skills/<skill>/references/
```

Format and module specs should make their relationship to root `SPEC.md`
explicit. They should state, briefly, whether they inherit, narrow, extend, or
intentionally override root conventions. They should not copy root rules unless
the narrower restatement is necessary for clarity.

## Repository Metadata

Root `CHANGELOG.md`, `CONTRIBUTING.md`, `NOTICE`, and `LICENSE` apply to the
public Meaningfall repository as a whole.

Format, module, and skill folders should not carry local `CHANGELOG.md`,
`CONTRIBUTING.md`, or `NOTICE` files by default. Add local metadata only when
standalone extraction creates concrete pressure and this root spec accepts the
exception.

## Contract Rules

Use these rules across Meaningfall's public contract system:

- one rule has one owning contract;
- a contract may depend on another contract, but should not copy it;
- a narrower contract may inherit, narrow, extend, or explicitly override a broader contract;
- overrides require accepted rationale;
- README files point to contracts; they do not become contracts by accumulation;
- examples demonstrate contracts; they do not become hidden contracts;
- `AGENTS.md` instructs agents how to operate; it does not become product truth;
- installed workspace files apply public contracts locally; they are not copies of the public repository.

If public artifacts appear to conflict, resolve by ownership.

## Formats

A public format owns a file-format contract.

Use formats for named file conventions such as `PRODUCT.md` and `PRINCIPLES.md`:

```text
formats/<format>/
  README.md
  spec.md
  PRINCIPLES.md    # create-on-need, follows the Principles-MD convention
  examples/        # create-on-need
  references/      # create-on-need
```

A format README is an entry point. It should explain the format's purpose,
status, boundaries, and where the normative contract lives. It should not
duplicate the full spec.

## Modules

A public module owns a governed capability or reusable discipline.

Use modules for Meaningfall behavior or discipline that is more than one file
format and needs a stable public owner:

```text
modules/<module>/
  README.md        # router, only when useful
  spec.md          # create-on-need, normative contract
  SKILL.md         # create-on-need, one compact module-owned procedure
  skill/           # create-on-need, one large module-owned procedure
  skills/          # create-on-need, multiple named module-owned procedures
  PRINCIPLES.md    # create-on-need, follows the Principles-MD convention
  principles/      # create-on-need, large principles corpus
  examples/        # create-on-need
  references/      # create-on-need
  assets/          # create-on-need
```

A module does not need `spec.md` by default. Its files should express the kind of
authority the module actually owns. Do not create empty module folders to reserve
future behavior.

## Skills

A public skill owns executable guided behavior.

Skills have the same internal shape wherever they live:

```text
<skill>/
  SKILL.md
  references/      # create-on-need, readable support material
  scripts/         # create-on-need, executable helper code
  assets/          # create-on-need, output resources
  agents/          # create-on-need, client metadata only
  PRINCIPLES.md    # create-on-need, follows the Principles-MD convention
```

`SKILL.md` owns the portable executable procedure. `references/` supports
agent reasoning and should be loaded only when needed. `scripts/` supports
repeatable execution. `assets/` supports generated outputs. `agents/` may help a
specific client present or discover a skill, but it must not own procedure,
contract, or product meaning.

Use root `skills/` for public distributed skills that are user-facing workflows
and do not belong entirely to one durable owning module:

```text
skills/<skill>/
```

Use module-owned procedures when executable behavior is an operational part of
one module and applies that module's contract or discipline:

```text
modules/<module>/SKILL.md
modules/<module>/skill/SKILL.md
modules/<module>/skills/<skill>/SKILL.md
```

Root skills may orchestrate formats and modules, but they should not copy
module-owned contract-critical behavior once that behavior has a module owner.
Root skills are public, inspectable, and callable; canonical Meaningfall skills
are governed product material, not assumed user-editable customization files.

User customization belongs in user-owned workspace guidance, wrappers, overlays,
or another accepted customization surface. It should not mutate canonical
Meaningfall skills directly.

## README Contract

READMEs are entry points and routers, not the main home for normative rules.

Use:

- root `README.md` for repository orientation, public product map, start prompt, and main entrypoints;
- `formats/<format>/README.md` for one format's purpose, status, boundaries, and spec link;
- `modules/<module>/README.md` for one module's purpose, status, boundaries, and owned contract or procedure links;
- `skills/<skill>/README.md` only when humans need an entry page separate from `SKILL.md`;
- installed `product-memory/README.md` for local read order and local memory roles, not as a copy of public specs.

Do not create `formats/README.md` or `modules/README.md` by default. Add a local
router only when root `README.md`, root `SPEC.md`, and `index.yaml` are not enough
to prevent wrong-file navigation.

If a README starts carrying durable rules, move those rules into the nearest spec, contract, decision, or root `SPEC.md` section and keep the README as a pointer.

## Current Ownership Map

Current durable owners:

| Concern | Owner |
| --- | --- |
| Repository-level public surface rules | root `SPEC.md` |
| `PRODUCT.md` format | `formats/product-md/` |
| Product truth over time | `modules/memory/` |
| `PRINCIPLES.md` convention | `formats/principles-md/` |
| Grow/root/settled discipline | `modules/seed-loop/` |
| Guided product-memory creation | `skills/guide/` |
| Meaningfall install processes | `skills/install/` |
| Meaningfall verification processes | `skills/verify/` |
| Git checkpoint hygiene | `skills/git-hygiene/` |
| Product-memory install target | `skills/install/references/product-memory.md` |
| Public repository surface verification | `skills/verify/references/repository-surface.md` |
| Installed product-memory verification | `skills/verify/references/product-memory.md` |

Build Flow is not a current product owner. Old Build Flow compatibility paths have
been removed from active public routing; Git history preserves the removed files.

## Reference And Example Contract

References support a format, module, or skill with detail that would make the
main spec or procedure too dense.

Examples demonstrate valid or useful use. They should not become hidden specs. If an example is meant to be normative, the owning spec must say so explicitly.

## Installed Workspace Boundary

The public Meaningfall repository describes and distributes Meaningfall. An installed user workspace applies Meaningfall.

The public repository contains public contracts, formats, modules, skills, references,
examples, compatibility surfaces, and repository metadata. It is not itself an
installed user workspace.

An installed user workspace contains the user's project files plus the Meaningfall files created or updated there, such as `PRODUCT.md`, `product-memory/`, and optional host-owned `AGENTS.md` guidance. It is not a copy of the public repository.

Do not make installed workspaces look like copies of the public repository. Do not install public repository structure by default.

Public repository folders must not look like installed user workspaces. Do not
place a live `product-memory/` folder under the public repository tree. Show
installed memory only as clearly marked examples.

Installed product memory stays visible and lightweight: a canonical `PRODUCT.md`, an always-present `product-memory/README.md`, create-on-need supporting files, a lazy archive, and no hidden state file.

The exact installed shape is owned by the Install skill's `product-memory`
target and is not restated here.

Do not install hidden state files, empty scaffolds, task boards, roadmap files, local `skills/`, local `principles/`, or public-spec copies into user projects by default.

## `AGENTS.md`

`AGENTS.md` is agent operating guidance, not product truth.

In the Meaningfall repository, `AGENTS.md` should stay operational: startup, routing, hard rules, and editing constraints.

In an installed user workspace, Meaningfall may add or update a small marked product-memory block only when that edit is visible and approval-controlled. The host project owns `AGENTS.md`.

## Action Modes

Meaningfall workflows share a vocabulary for how a single durable action is
initiated and authorized. A mode is a property of an individual action, not a
global system state. It is orthogonal to opt-in, opt-out, or enablement policy:
those decide whether a behavior is active at all, while the mode says how one
action is initiated and authorized.

- `explicit` — the human directly asks for the action; the agent may act within
  the requested scope.
- `automatic` — the agent may act without interrupting the human, but only inside
  an explicit or already accepted workflow, and only when the action is low-risk,
  local, expected, and reversible or reviewable.
- `suggested` — the agent notices a useful durable transition, proposes the exact
  action, destination, and wording or diff, and acts only if the human accepts.
  Silence or ambiguity means no durable write.

Durable memory or file transitions default to `suggested` unless the human
explicitly requested them, an accepted workflow narrowly covers them, or the human
has given a standing revocable opt-in for the declared scope.

Accepting this vocabulary grants no automatic behavior to any format, module,
skill, or workflow by itself. Per-workflow mode grants belong in each workflow's
own contract or decision.

Irreversible, destructive, security-sensitive, or history-rewriting actions
require explicit confirmation even when they are requested.

A separate shared reference may be created only if this section grows too large
and this spec explicitly authorizes that root-owned reference shape.

## Create-On-Need

Do not create structure before there is content, behavior, or client pressure that needs it.

Avoid empty public formats, empty modules, empty installed memory files, empty
archive folders, hidden manifests, and speculative local tooling surfaces.

Prefer the simplest structure that preserves readability and function. Use one
file before creating a folder. Promote a file to a folder only when multiple
artifacts, separate loading behavior, executable resources, or clear navigation
pressure make the folder simpler than the file.

Generation surfaces must be explicit before generation uses them. If a generated
workflow may create folders or files, the owning contract, skill, or reference
must name the allowed output shapes and their roles. Generation should minimize
deviation from this spec and from the owning format, module, or skill contract.

Do not introduce a new public folder kind, file kind, entity file, generated
surface, or spontaneous output location that this spec or an owning contract does
not describe. Treat that as structure pressure: the new shape needs an owning
contract or a revision to this repository spec before generators rely on it.

## Promotion And Compatibility

Promote a draft into public product material only when the rule is accepted, useful beyond an unaccepted discussion, and has a clear owner.

Accepted rationale belongs in decisions. Public normative behavior belongs in
the appropriate format spec, module spec, module procedure, skill, install
reference, or root `SPEC.md`.

Distinct streams such as format version, module version, skill version, spec
version, install-contract generation, and snippet generation are tracked
separately and not conflated.

Compatibility surfaces should be visibly marked as compatibility or history. They may preserve old paths and explain migration, but they should not look like the durable canonical home once a new canonical home exists.

## Non-Goals

Root `SPEC.md` is not:

- a product spec;
- a skill procedure;
- an installed workspace template;
- a task board;
- a roadmap;
- a changelog;
- a replacement for decisions;
- a place for planning material.
