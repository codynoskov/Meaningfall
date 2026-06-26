# Contributing

Meaningfall is a public product-family repository. Contributions should make its
formats, modules, and skills easier for humans and AI coding agents to read,
write, install, verify, and maintain.

## Good Contributions

- Improve a format or module spec without duplicating root repository rules.
- Improve a skill procedure without moving product truth into the skill.
- Add small, realistic, complete examples where the owning spec uses examples.
- Clarify format, module, skill, installation, verification, and agent-operation boundaries.
- Point out rules that are too vague, too heavy, or likely to fail across common
  product archetypes.
- Propose validation or verification rules after examples show repeated pressure.

## How To Contribute

Before opening a large change, start with a GitHub Issue.

Example contributions should normally update the nearest example index and keep
examples complete enough to inspect.

Spec changes should preserve existing examples unless the change intentionally revises
the convention. Keep normative material in the owning spec rather than duplicating it
across README files, references, examples, or skills.

## Repository Boundary

The public Meaningfall publication root is this folder.

Keep public contributions inside `README.md`, `SPEC.md`, `index.yaml`,
`formats/`, `modules/`, `skills/`, and root repository metadata files.

Do not add or depend on private development paths such as process memory, tickets,
drafts, archives, unrelated product folders, or local planning notes.

## ProductMD Contributions

ProductMD is a v0.1 convention. Contributions should make the `PRODUCT.md` format
easier for humans and AI coding agents to read, write, and maintain.

Good ProductMD contributions include:

- improving the `PRODUCT.md` specification;
- adding small, realistic, complete `PRODUCT.md` examples;
- clarifying the boundary between `PRODUCT.md`, `AGENTS.md`, skills, and the visual
  design layer;
- pointing out fields that are too vague, too heavy, or likely to fail across common
  product archetypes.

ProductMD example contributions should normally add:

- one folder under `formats/product-md/examples/`;
- one complete `PRODUCT.md`;
- one short entry in `formats/product-md/examples/README.md`.

## Keep Formats Small

Avoid adding a new top-level field when an existing field, Markdown section, example, or future skill can carry the meaning.

ProductMD should stay useful as a single root file. Detailed page maps, visual tokens, implementation recipes, and generation procedure belong elsewhere.

Examples should be complete `PRODUCT.md` files unless a contribution explicitly proposes a non-public working artifact. Section fragments, schema-completion examples, and one-off syntax demonstrations should not become the public example surface by default.

Interview and generation procedure belongs in the Guide skill
([`skills/guide/`](skills/guide/)), not in the ProductMD spec or
examples.

## Documentation Style

- Write documentation in English.
- Prefer ordinary Markdown.
- Use YAML only for exact ProductMD examples or syntax.
- Keep examples realistic and inspectable.
