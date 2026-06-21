# Changelog

## Unreleased

- Moves Product Brief's canonical public home to `skills/product-brief/`.
- Keeps `products/build-flow/skills/product-brief/SKILL.md` as a compatibility loader for published links.
- Keeps old Product Brief reference paths as compatibility pointers.
- Freezes the Build Flow package version stream during the compatibility window.
- Extends the Product Brief product-memory install contract to `install-contract v1.1`.
- Adds `product-memory/facts.md` and `product-memory/learnings.md` as create-on-need supporting files.
- Defines the product-design-native memory model for notes, facts, drafts, decisions, learnings, and archive, including draft acceptance versus integration, returned drafts, decision cancellation, rationale versus learning, and archive rules for draft iteration logs.

## v0.2.0 - 2026-06-19

Product Brief now installs the current accepted starter product-memory surface for new products:

- Creates `PRODUCT.md` as canonical product truth.
- Creates `product-memory/README.md` as the supporting memory role map and read order.
- Creates `product-memory/notes.md`, `decisions.md`, `drafts.md`, and `glossary.md` only when populated.
- Keeps `product-memory/archive/` lazy and `product-memory/state.yaml` deferred.
- Creates or updates a host-owned `AGENTS.md` product-memory block by default unless the user opts out.
- Adds `skills/product-brief/references/product-memory-install.md` as install-contract v1.
- Keeps `skills/product-brief/references/verification.md` focused on ProductMD format and placement checks.

## v0.1.0 - 2026-06-13

Initial Build Flow package:

- Established Build Flow as the guided product-composition product under the Meaningfall umbrella.
- Moved the Product Brief stage into `products/build-flow/skills/product-brief/`.
- Defined the initial scope: Product Brief creates or updates `PRODUCT.md`.
- Kept DesignMD, component generation, visual reference generation, stack analysis, prototype generation, and test-data planning out of current scope.
- Documented that Product Brief verification checks are stage-local and derived from the ProductMD spec, not a second ProductMD format authority.
