# Meaningfall

Meaningfall is a public product-family repository for repo-native product meaning, guided product creation, and dependency-ordered build verification.

## Products

| Product | Folder | Role |
| --- | --- | --- |
| ProductMD | [`products/product-md/`](products/product-md/) | `PRODUCT.md` convention for durable product meaning and behavior. Current package: v0.1.11; current spec: v0.1.10. |
| Build Flow | [`products/build-flow/`](products/build-flow/) | Guided creation workflow. Current scope: Product Brief creates or updates `PRODUCT.md`. Current package: v0.1.0. |
| Seed Loop | [`products/seed-loop/`](products/seed-loop/) | Domain-neutral grow/root/settled discipline for dependency-ordered artifacts. Current package: v0.1.0. |

## Boundaries

- ProductMD owns the `PRODUCT.md` format, specification, examples, and format validation expectations.
- Build Flow owns guided creation stages, interview behavior, handoff, and stage orchestration. It does not define ProductMD syntax.
- Seed Loop owns the neutral build-and-verify discipline. Build Flow and ProductMD may instantiate or reference it, but do not redefine it.

## Start Here

- [`products/product-md/README.md`](products/product-md/README.md) — ProductMD.
- [`products/build-flow/README.md`](products/build-flow/README.md) — Build Flow and the Product Brief skill.
- [`products/seed-loop/README.md`](products/seed-loop/README.md) — Seed Loop.

## License

Unless a product folder states otherwise, public product material in this repository is licensed under the Apache License, Version 2.0 in the repository root. Product folders that are intended to be extractable carry local `NOTICE` files for attribution.
