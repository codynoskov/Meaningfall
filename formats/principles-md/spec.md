# Principles-MD Spec

Status: accepted format contract.

This spec follows root [`SPEC.md`](../../SPEC.md). It inherits the root
public-surface and contract rules, and narrows or extends them only where this spec
says so explicitly.

## Purpose

Principles-MD defines the `PRINCIPLES.md` convention for scoped judgment guidance.

`PRINCIPLES.md` helps humans and agents choose well when specs, READMEs, or
procedures intentionally leave room for judgment.

## What `PRINCIPLES.md` Is

`PRINCIPLES.md` is scoped judgment guidance.

It records durable preferences, tradeoffs, interpretation rules, and working posture
for a clear scope. It is a standing disposition applied across future
under-determined choices.

Useful content can include:

- design posture for a product family;
- review posture for a package;
- tradeoff guidance for a domain;
- durable "prefer this when uncertain" rules;
- interpretive guidance that affects many future choices but is not itself product
  meaning.

## What `PRINCIPLES.md` Is Not

A principle is reusable judgment guidance. It is not:

- product truth;
- normative product behavior;
- an agent operating instruction;
- accepted rationale or a one-time durable choice;
- a reusable process insight from a past episode;
- a term or naming definition;
- a task, roadmap, backlog, or changelog;
- a hidden memory layer.

Route product truth to `PRODUCT.md`. Route normative behavior to the relevant spec.
Route agent operating instructions to `AGENTS.md`. Route accepted rationale to a
decision surface. Route naming definitions to a glossary.

Discriminator: a decision resolves one question once, with rationale and a specific
effect; a learning is an insight extracted from a past episode; a principle is a
standing disposition applied across many future under-determined choices.

## Scope And Placement

A `PRINCIPLES.md` file should live near the surface it governs, such as a format,
module, skill, or installed project root.

Examples of possible scopes:

```text
formats/<format>/PRINCIPLES.md
modules/<module>/PRINCIPLES.md
skills/<skill>/PRINCIPLES.md
<project-or-owned-surface>/PRINCIPLES.md
```

This is not an instruction to create these files. Create a `PRINCIPLES.md` file only
when there is real scoped judgment guidance that does not belong more cleanly in a
spec, README, `AGENTS.md`, `PRODUCT.md`, decision surface, learning, or glossary.

Do not create `PRINCIPLES.md` by default in installed user workspaces.

## File Shape

A `PRINCIPLES.md` file should stay short and readable.

```markdown
# Principles

Status: draft | accepted

Scope: <what this file governs>

## Purpose

## Applies To

## Principles

## What This Does Not Decide
```

Do not introduce default YAML frontmatter unless real consumers need
machine-readable fields.

## Conflict Rule

If a `PRINCIPLES.md` file conflicts with a spec, the spec wins for normative
behavior.

If a `PRINCIPLES.md` file conflicts with `PRODUCT.md`, `PRODUCT.md` wins for product
meaning.

Against Memory, Memory wins for product-truth governance. Principles only fills
judgment that those contracts intentionally leave open.

If a `PRINCIPLES.md` file conflicts with `AGENTS.md`, surface the conflict.
`AGENTS.md` owns agent operating instructions, while `PRINCIPLES.md` owns judgment
guidance.

If two principles files apply to the same work and appear to conflict, prefer the
more specific scope only when it clearly narrows the broader guidance. Otherwise
surface the conflict instead of silently choosing.

## Non-Goals

Do not use Principles-MD to:

- publish planning material;
- duplicate product specs;
- replace decisions;
- create another memory layer;
- install local `principles/`;
- create default installed `PRINCIPLES.md`;
- create a root public `PRINCIPLES.md` only to reserve the idea.
