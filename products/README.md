# Products

This folder contains public Meaningfall product work. Product packages live here so
they can later be extracted into standalone repositories if needed.

## Active Products

| Product | Folder | Role |
| --- | --- | --- |
| ProductMD | [`product-md/`](product-md/) | `PRODUCT.md` convention for product meaning and behavior. Current package: v0.1.12; current spec: v0.1.11. |
| Build Flow | [`build-flow/`](build-flow/) | Compatibility/history package for the former Product Brief home. Its version stream is frozen during the compatibility window. |
| Seed Loop | [`seed-loop/`](seed-loop/) | Neutral, domain-agnostic build-and-verify discipline (grow → root → settled), reused by ProductMD and Product Brief. Current package: v0.1.0. |

## Accepted Direction

Memory is the fourth product direction in the Meaningfall family. It owns governance of product truth over time: how `PRODUCT.md` and supporting product-memory surfaces are interpreted, reconciled, and maintained. Today, initialization ships through the root [`../skills/product-brief/`](../skills/product-brief/) public skill following the install contract; the broader governance remains the deferred Memory direction.

The physical `products/memory/` package is deferred until there is concrete public tooling, documentation, or client pressure such as Reconcile, Impact, Lookup, Setup, or Studio integration, plus an accepted normative Memory contract/spec or equivalent public artifact to package there. Until then, Memory direction is carried by the Product Brief install contract and product-family documentation rather than by an empty package folder.

Studio is a possible future client/interface over ProductMD, Memory, and Build Flow behavior. It is not a package or umbrella product today.

## Boundaries

- ProductMD owns the `PRODUCT.md` format: what a valid canonical product-truth file is. It is stateless and per-file.
- Product Brief, under [`../skills/product-brief/`](../skills/product-brief/), owns the guided path from rough prompt or interview to the starter product-memory surface: `PRODUCT.md`, `product-memory/README.md`, create-on-need supporting files, and default-on approval-visible `AGENTS.md` integration.
- Build Flow remains as compatibility/history for the earlier Product Brief package path. It no longer owns Product Brief as the durable canonical home unless a later accepted Build Flow spec or contract re-establishes it as a product package.
- Memory owns governance over product truth over time. It governs how `PRODUCT.md` becomes and stays true; it does not replace ProductMD or own the `PRODUCT.md` format.
- Seed Loop owns the neutral build-and-verify discipline; ProductMD and Product Brief reference it, and it references neither (it stays domain-agnostic).
- Internal lab notes, process memory, and private planning material are not part of this public package.

Public product folders must not look like installed user workspaces. This repository may describe and demonstrate installed product memory, but it must not contain a live `product-memory/` folder under `products/` as if Meaningfall itself were an installed user project. Public examples of installed memory must live under clearly marked example paths and show only the files that exist in that example.

## Deferred Or Reference Areas

These are not active standalone products yet:

- Memory package (`products/memory/`)
- Studio
- Resolver
- LLM Resolution Harness
- Core registry
- adapters
- Astro realization
- chat-driven pseudo CMS

They may influence the active products, but should not become new folders here until there is concrete pressure.

## License

Unless a product folder states otherwise, public product material in this repository is licensed under the Apache License, Version 2.0 in the repository root. Product folders intended for later standalone extraction carry local `NOTICE` files for attribution.
