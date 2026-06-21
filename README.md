# Meaningfall

Meaningfall is a public product-family repository for repo-native product meaning, guided product creation, and dependency-ordered build verification.

The public product packages live under [`products/`](products/). Public executable
skills live under [`skills/`](skills/) when they do not have a durable owning
product package.

## Products

| Product | Folder | Role |
| --- | --- | --- |
| ProductMD | [`products/product-md/`](products/product-md/) | `PRODUCT.md` convention for durable product meaning and behavior. Current package: v0.1.12; current spec: v0.1.11. |
| Build Flow | [`products/build-flow/`](products/build-flow/) | Compatibility/history package for the former Product Brief home. Its version stream is frozen during the compatibility window. |
| Seed Loop | [`products/seed-loop/`](products/seed-loop/) | Domain-neutral grow/root/settled discipline for dependency-ordered artifacts. Current package: v0.1.0. |

## Start With Meaningfall

To create product memory for a new product, use Product Brief. In a chat or AI client
that can read GitHub, paste:

```text
Read and follow this skill, then run Product Brief to help me create product memory for
a new product:

https://github.com/codynoskov/Meaningfall/blob/main/skills/product-brief/SKILL.md

Run the interview in English.
```

Change `English` to another language if needed. Product Brief creates `PRODUCT.md`,
`product-memory/README.md`, create-on-need supporting memory files, and default-on
approval-visible `AGENTS.md` integration.

## Boundaries

- ProductMD owns the `PRODUCT.md` format, specification, examples, and format validation expectations.
- Product Brief is the public skill for guided creation of starter product memory.
- Build Flow remains as compatibility/history for earlier Product Brief packaging. It does not define ProductMD syntax.
- Seed Loop owns the neutral build-and-verify discipline. Product Brief and ProductMD may instantiate or reference it, but do not redefine it.

## Start Here

- [`products/product-md/README.md`](products/product-md/README.md) — ProductMD.
- [`skills/product-brief/SKILL.md`](skills/product-brief/SKILL.md) — Product Brief skill.
- [`products/build-flow/README.md`](products/build-flow/README.md) — Build Flow compatibility/history.
- [`products/seed-loop/README.md`](products/seed-loop/README.md) — Seed Loop.

## License

Unless a product folder states otherwise, public product material in this repository is licensed under the Apache License, Version 2.0 in the repository root. Product folders that are intended to be extractable carry local `NOTICE` files for attribution.
