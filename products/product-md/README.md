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

The single source of truth for the format is the spec: [`docs/spec.md`](docs/spec.md).

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

See [`docs/spec.md`](docs/spec.md) for the full field reference and [`docs/examples/`](docs/examples/) for complete files at different levels of product pressure.

## Create one with Build Flow

You do not have to write `PRODUCT.md` by hand. **Build Flow** is the guided-creation product; its Product Brief stage interviews you and produces an editable `PRODUCT.md`. It is packaged as an Agent Skill (the open `SKILL.md` standard), so it runs two ways from one file — installed in a skill-aware tool, or pasted into an ordinary chat.

See [Build Flow](../build-flow/README.md) for both run modes. The skill itself lives at [`../build-flow/skills/product-brief/`](../build-flow/skills/product-brief/) and references this spec — it does not restate the format.

## Use with agents

After `PRODUCT.md` exists, agents should read it before planning or changing product behavior. A minimal `AGENTS.md` instruction:

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

- [`docs/spec.md`](docs/spec.md) — the ProductMD specification. Single source of truth for the format.
- [`docs/examples/`](docs/examples/) — complete `PRODUCT.md` files.
- [Build Flow](../build-flow/README.md) — the guided-creation product; its Product Brief stage creates a `PRODUCT.md`.
- [`CHANGELOG.md`](CHANGELOG.md) · [`CONTRIBUTING.md`](CONTRIBUTING.md) · [`NOTICE`](NOTICE) · root [`LICENSE`](../../LICENSE)

## Status

ProductMD package v0.1.11 ships the ProductMD v0.1.10 specification. The package release moved guided creation into Build Flow; it did not change the `PRODUCT.md` format.

ProductMD v0.1 is intentionally small. Examples and Build Flow's Product Brief stage should improve the convention without turning `PRODUCT.md` into a runtime, CMS, workflow engine, ontology language, or implementation format.
