# ProductMD

ProductMD is a small Markdown convention for describing what a product is and how it behaves.

Add a root-level `PRODUCT.md` to give humans and AI agents durable product context — before, during, and after implementation. It is plain Markdown with optional YAML frontmatter; no tool or build step is required to read or edit it.

ProductMD sits beside other repo-native context files:

| File | Describes |
| --- | --- |
| `README.md` | What the repository is. |
| `AGENTS.md` | How agents should work in the repository. |
| `PRODUCT.md` | What the product is and how it behaves. |
| `SKILL.md` | How to perform a reusable task. |

## Why

Every new AI session reconstructs product context from prompts, tickets, READMEs, and code. `PRODUCT.md` gives that context a small, inspectable, repo-native home, so identity, behavior-changing states, durable product-map structure, semantic composition roles and reusable profiles, named navigations, operations, and internal mechanics are not re-derived each time.

The single source of truth for the format is the spec: [`spec.md`](spec.md).

## What a PRODUCT.md looks like

```md
---
profile:
  identity:
    name: Acme
    kind: research workspace
    audience: small teams

entities:
  notes:
    collection: true
    views:
      - in-card
      - in-summary
  library:
    collection: true
    views:
      - in-card
    relations:
      - notes

conditions:
  states:
    account:
      - anonymous
      - subscriber
    access:
      - public
      - paywalled

actions:
  account:
    - signin
  billing:
    - checkout

map:
  product:
    contains:
      props:
        composition:
          uses: site-orientation
      home:
        home: true
      research:
        props:
          composition:
            uses: reading
        contains:
          previews: {}
          library: {}
  system:
    contains:
      signin: {}
      checkout: {}

compositions:
  site-orientation:
    shell: {}
    complement: {}
  reading:
    shell:
      nav:
        local: local-section
    complement:
      related: {}

navigations:
  local-section:
    from: -1
    depth: 1

mechanics:
  access:
    - paywall-resolution
---

# Acme

## Overview

Acme helps small teams collect, organize, and reuse research notes.

Anonymous visitors can open public previews of notes and library collections. Subscribers can open the full library. `checkout` is a system item because it supports an access-changing billing action, and the `paywall-resolution` mechanic preserves the logic that decides when a preview becomes paywalled content.
```

See [`spec.md`](spec.md) for the full field reference and [`examples/`](examples/) for complete files at different levels of product pressure.

## Create One With Guide

You do not have to write `PRODUCT.md` by hand. **Guide** is the guided product-memory skill; it interviews you and creates or updates an editable `PRODUCT.md`, then uses Install when product memory should be installed around it. It is packaged as an Agent Skill (the open `SKILL.md` standard), so it runs in skill-aware tools and can be followed from the root GitHub start prompt.

See the repository root [`README.md`](../../README.md) for the start prompt. The skill itself lives at [`../../skills/guide/`](../../skills/guide/) and references this spec — it does not restate the format.

## Use with agents

After `PRODUCT.md` exists, agents should read it before planning or changing
product behavior. Install creates or updates the canonical default-on marked
product-memory block for new product-memory installs; the snippet below is only a
minimal manual alternative focused on ProductMD format coherence.

```md
Before changing product behavior, read `PRODUCT.md` and treat it as durable product context:

- preserve the product identity, audience, scope, and boundaries from the body
- keep `entities` coherent across collection facts, views, relations, map structure, and body guidance
- respect behavior-changing states in `conditions`
- treat `actions` as product operations, not implementation task lists
- keep `map` branches, spaces, contained items, and `props` coherent with product structure
- preserve composition roles, reusable `compositions`, `props.composition.uses`, named `navigations`, and any reserved `nav` exposures when changing product, system, notification, integration, page, or flow structure
- preserve `mechanics` domains without turning them into implementation specs

If implementation conflicts with `PRODUCT.md`, ask whether the product meaning should change before coding around it.
```

## Documentation

- [`spec.md`](spec.md) — the ProductMD specification. Single source of truth for the format.
- [`examples/`](examples/) — complete `PRODUCT.md` files.
- [Guide](../../skills/guide/) — the guided product-memory skill that creates or updates `PRODUCT.md`.
- [Install](../../skills/install/) — the Install skill for concrete Meaningfall workspace surfaces.
- [Verify](../../skills/verify/) — the Verify skill for Meaningfall artifacts and ProductMD output.
- root [`CHANGELOG.md`](../../CHANGELOG.md) · root [`CONTRIBUTING.md`](../../CONTRIBUTING.md) · root [`NOTICE`](../../NOTICE) · root [`LICENSE`](../../LICENSE)

## Status

ProductMD format v0.1.12 ships the ProductMD v0.1.11 specification. This release adds contribution-placement guidance for classifying user additions; guided creation is owned by Guide.

ProductMD v0.1 is intentionally small. Examples and the Guide skill should improve the convention without turning `PRODUCT.md` into a runtime, CMS, workflow engine, ontology language, or implementation format.
