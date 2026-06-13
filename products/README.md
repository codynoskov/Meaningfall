# Products

This folder contains the public Meaningfall product family.

## Active Products

| Product | Folder | Role |
| --- | --- | --- |
| ProductMD | [`product-md/`](product-md/) | `PRODUCT.md` convention for product meaning and behavior. Current package: v0.1.11; current spec: v0.1.10. |
| Build Flow | [`build-flow/`](build-flow/) | Guided product-composition workflow. Current scope is one stage, Product Brief, which creates or updates `PRODUCT.md`. Current package: v0.1.0. |
| Seed Loop | [`seed-loop/`](seed-loop/) | Neutral, domain-agnostic build-and-verify discipline (grow -> root -> settled), reused by ProductMD and Build Flow. Current package: v0.1.0. |

## Boundaries

- ProductMD owns product meaning and the `PRODUCT.md` format.
- Build Flow owns guided creation: stage orchestration, interview behavior, handoff, which artifacts a stage may create or update, and how Seed Loop is instantiated for a stage. It does not redefine the ProductMD format; if a stage reveals missing product meaning, that change belongs in ProductMD.
- The Product Brief stage, under [`build-flow/skills/product-brief/`](build-flow/skills/product-brief/), owns the path from rough prompt or interview to `PRODUCT.md`.
- Seed Loop owns the neutral build-and-verify discipline; ProductMD and Build Flow reference it, and it references neither (it stays domain-agnostic).

## License

Unless a product folder states otherwise, public product material in this repository is licensed under the Apache License, Version 2.0 in the repository root. Product folders intended for later standalone extraction carry local `NOTICE` files for attribution.
