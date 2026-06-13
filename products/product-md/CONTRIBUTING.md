# Contributing

ProductMD is a v0.1 convention. Contributions should make the format easier for humans and AI coding agents to read, write, and maintain.

## Good Contributions

- Improve the `PRODUCT.md` specification.
- Add small, realistic, complete `PRODUCT.md` examples.
- Clarify the boundary between `PRODUCT.md`, `AGENTS.md`, skills, and the visual design layer.
- Point out fields that are too vague, too heavy, or likely to fail across common product archetypes.
- Propose validation rules after examples show repeated pressure.

## How To Contribute

Before opening a large change, start with a GitHub Issue.

Example contributions should normally add:

- one folder under `docs/examples/`
- one complete `PRODUCT.md`
- one short entry in `docs/examples/README.md`

Spec changes should preserve the existing examples unless the change intentionally revises the convention. Keep normative material in the spec rather than duplicating it across files.

## Keep The Format Small

Avoid adding a new top-level field when an existing field, Markdown section, example, or future skill can carry the meaning.

ProductMD should stay useful as a single root file. Detailed page maps, visual tokens, implementation recipes, and generation procedure belong elsewhere.

Examples should be complete `PRODUCT.md` files unless a contribution explicitly proposes a non-public working artifact. Section fragments, schema-completion examples, and one-off syntax demonstrations should not become the public example surface by default.

Interview and generation procedure belongs in the Build Flow product ([`../build-flow/skills/product-brief/`](../build-flow/skills/product-brief/)), not in the ProductMD spec or examples.

## Publication Boundary

The standalone ProductMD publication root is this folder.

Keep public contributions inside:

- `README.md`
- `CONTRIBUTING.md`
- `docs/`

The interview skill that creates a `PRODUCT.md` is a separate product, Build Flow, and is contributed under `../build-flow/`, not here.

Do not add or depend on private development paths such as process memory, tickets, drafts, archives, unrelated product folders, or local planning notes.

## Documentation Style

- Write documentation in English.
- Prefer ordinary Markdown.
- Use YAML only for exact ProductMD examples or syntax.
- Keep examples realistic and inspectable.
