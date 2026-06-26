# AGENTS.md

Meaningfall is a public product-family repository. Public formats live under
`formats/`; public modules live under `modules/`; public executable skills live
under `skills/`.

Voice/input alias: when the human says or dictates "meaningful" as a project name,
interpret it as "Meaningfall".

This file is public agent guidance. It is operational guidance, not product truth.
For public surface placement, ownership, specification hierarchy, and
contract conflicts, follow root `SPEC.md`.

## Startup

For public Meaningfall work, read only what the task needs:

1. `README.md`
2. `SPEC.md`
3. the nearest format, module, or skill README/spec/`SKILL.md`

## Layer Boundary

- `SPEC.md`, `formats/`, `modules/`, and `skills/` define public Meaningfall
  contracts, formats, modules, and skills.
- An installed user workspace contains `PRODUCT.md`, `product-memory/`, and
  optional host-owned `AGENTS.md` guidance. It is not represented by a live
  installed workspace folder inside the public repository tree.
- Public Meaningfall files must be understandable from public files alone.

## Hard Rules

- Documentation is written in English.
- Current public format material belongs in `formats/`.
- Current public module material belongs in `modules/`.
- Public distributed Meaningfall skills belong in root `skills/`; this is not an
  installed user-workspace `skills/` folder.
- Root `SPEC.md` owns repository-level public surface and contract hierarchy rules.
- Do not create installed-workspace folders under the public repository tree.
- Keep edits to the smallest coherent file set.
- Use ordinary Markdown; editor-specific syntax and private workspace rules are not
  active here.

## Layout

- `README.md` — public repository overview.
- `SPEC.md` — repository-level public surface and contract hierarchy spec.
- `index.yaml` — public machine-readable repository map.
- `formats/product-md/` — ProductMD format.
- `formats/principles-md/` — Principles-MD format.
- `modules/memory/` — Memory module.
- `modules/seed-loop/` — Seed Loop module.
- `skills/guide/` — Guide public skill.
- `skills/install/` — Install public skill.
- `skills/verify/` — Verify public skill.
- `skills/git-hygiene/` — Git Hygiene public skill.
