# Meaningfall

Meaningfall is a product-family workspace for repo-native product meaning, guided
product creation, product memory, scoped principles, and dependency-ordered build
verification.

Read [`SPEC.md`](SPEC.md) for repository-level public surface rules, ownership,
format/module placement, and contract hierarchy.

## Start

To create or update product memory for a product, use Guide. In a chat or AI
client that can read GitHub, paste:

```text
Read and follow this skill, then run Guide to help me create or update product memory
for a product:

https://github.com/codynoskov/Meaningfall/blob/main/skills/guide/SKILL.md

Run the interview in English.
```

Change `English` to another language if needed. Exact product-memory install
behavior is defined by the [Install skill](skills/install/).

## Entrypoints

- [`SPEC.md`](SPEC.md) — repository-level public contract.
- [`formats/product-md/`](formats/product-md/) — ProductMD.
- [`formats/principles-md/`](formats/principles-md/) — Principles-MD.
- [`modules/memory/`](modules/memory/) — Memory.
- [`modules/seed-loop/`](modules/seed-loop/) — Seed Loop.
- [`skills/guide/`](skills/guide/) — Guide skill.
- [`skills/install/`](skills/install/) — Install skill.
- [`skills/verify/`](skills/verify/) — Verify skill.
- [`skills/git-hygiene/`](skills/git-hygiene/) — Git Hygiene skill.
- [`CHANGELOG.md`](CHANGELOG.md) — repository release history.
- [`CONTRIBUTING.md`](CONTRIBUTING.md) — repository contribution guidance.
- [`index.yaml`](index.yaml) — machine-readable repository map.

## License

Public product material in this repository is licensed under the Apache License,
Version 2.0 in the repository root. See [`LICENSE`](LICENSE) and [`NOTICE`](NOTICE).
