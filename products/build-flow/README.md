# Build Flow Compatibility

Build Flow is retained as compatibility/history for the former Product Brief package
home. Product Brief is now the canonical public skill at
[`../../skills/product-brief/`](../../skills/product-brief/).

Build Flow package version stream: **frozen at v0.2.0 during the compatibility window**.

This folder keeps older public links alive. It is not the durable canonical home for
Product Brief unless a later accepted Build Flow spec, stage model, or multi-skill
contract re-establishes Build Flow as a product package.

## Boundaries

- Product Brief owns the current guided creation behavior as a public skill.
- ProductMD owns the `PRODUCT.md` format. Its single source of truth is the ProductMD spec.
- Seed Loop owns the neutral build-and-verify discipline. Product Brief instantiates it for ProductMD.
- Memory remains an accepted direction with no `products/memory/` package yet.
- Build Flow may become a product package again only after a later accepted Build Flow spec, stage model, or multi-skill governed capability exists.

## Compatibility Paths

The old Product Brief path remains live as a loader:

```text
products/build-flow/skills/product-brief/SKILL.md
```

The old reference paths remain as pointers:

```text
products/build-flow/skills/product-brief/references/product-memory-install.md
products/build-flow/skills/product-brief/references/verification.md
```

## Product Memory Install

Product Brief's install behavior is owned by the canonical skill references. The
operational install contract is
[`../../skills/product-brief/references/product-memory-install.md`](../../skills/product-brief/references/product-memory-install.md).
ProductMD format verification remains in
[`../../skills/product-brief/references/verification.md`](../../skills/product-brief/references/verification.md).

## Run Product Brief

Use the root [`../../README.md`](../../README.md) start prompt. It points to the
canonical Product Brief skill:

```text
https://github.com/codynoskov/Meaningfall/blob/main/skills/product-brief/SKILL.md
```

The old lite-mode URL under `products/build-flow/skills/product-brief/SKILL.md` remains
as a compatibility loader for previously published prompts, but new usage should start
from the root README prompt and the canonical skill URL.

## Read

- [`../../skills/product-brief/`](../../skills/product-brief/) — the Product Brief skill (interview + Seed Loop instantiation for ProductMD and product-memory install).
- [`../../skills/product-brief/references/product-memory-install.md`](../../skills/product-brief/references/product-memory-install.md) — the Product Brief install contract.
- [ProductMD](../product-md/README.md) — the `PRODUCT.md` format this skill produces.
- [Seed Loop](../seed-loop/README.md) — the neutral build-and-verify discipline the skill instantiates.
- [`CHANGELOG.md`](CHANGELOG.md) · [`NOTICE`](NOTICE) · root [`LICENSE`](../../LICENSE)
