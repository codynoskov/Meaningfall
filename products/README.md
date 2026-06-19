# Products

This folder contains the public Meaningfall product family.

New public-facing product conventions and tools live here so they can later be extracted into standalone repositories if needed.

[`workflow.md`](workflow.md) is the shared working note for how these standalone products and related external conventions may work together. It is not itself a standalone product folder.

## Active Products

| Product | Folder | Role |
| --- | --- | --- |
| ProductMD | [`product-md/`](product-md/) | `PRODUCT.md` convention for product meaning and behavior. Current package: v0.1.12; current spec: v0.1.11. |
| Build Flow | [`build-flow/`](build-flow/) | Guided product-composition workflow; staged creation and review flows. Current scope is one stage, Product Brief, which creates or updates the starter product-memory surface around `PRODUCT.md`. Current package: v0.2.0. |
| Seed Loop | [`seed-loop/`](seed-loop/) | Neutral, domain-agnostic build-and-verify discipline (grow → root → settled), reused by ProductMD and Build Flow. Current package: v0.1.0. |

## Accepted Direction

Memory is the fourth product direction in the Meaningfall family. It owns governance of product truth over time: how `PRODUCT.md` and supporting product-memory surfaces are interpreted, reconciled, and maintained. Today, initialization ships as Build Flow's Product Brief stage following the install contract; the broader governance remains the deferred Memory direction.

The physical `products/memory/` package is deferred until there is concrete public tooling, documentation, or client pressure such as Reconcile, Impact, Lookup, Setup, or Studio integration. Until then, Memory direction is carried by the install contract, Build Flow behavior, and product-family documentation rather than by an empty package folder.

Studio is a possible future client/interface over ProductMD, Memory, and Build Flow behavior. It is not a package or umbrella product today.

## Boundaries

- ProductMD owns the `PRODUCT.md` format: what a valid canonical product-truth file is. It is stateless and per-file.
- Build Flow owns guided creation: stage orchestration, interview behavior, handoff, which artifacts a stage may create or update, and how Seed Loop is instantiated for a stage. It does not redefine the ProductMD format; if a stage reveals missing product meaning, that change belongs in ProductMD.
- The Product Brief stage, under [`build-flow/skills/product-brief/`](build-flow/skills/product-brief/), owns the path from rough prompt or interview to the starter product-memory surface: `PRODUCT.md`, `product-memory/README.md`, create-on-need supporting files, and default-on approval-visible `AGENTS.md` integration.
- Memory owns governance over product truth over time. It governs how `PRODUCT.md` becomes and stays true; it does not replace ProductMD or own the `PRODUCT.md` format.
- Seed Loop owns the neutral build-and-verify discipline; ProductMD and Build Flow reference it, and it references neither (it stays domain-agnostic).
- `workflow.md` owns current cross-product workflow notes, including ProductMD, external `DESIGN.md`, and later generation-tool boundaries.
- Older Meaningfall lab/reference material is outside this public product package. It may inform future work, but Build Flow Product Brief is the public creation path here and targets product memory around `PRODUCT.md`.

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
