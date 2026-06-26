# Product Memory Verification

Applied checks for an installed product-memory surface. This target checks an
installed `product-memory/` against the Memory spec and the Install product-memory
reference. Authority for what is valid stays with those contracts; when in doubt,
the Memory spec wins.

Use this target when verifying or repairing an installed product-memory surface.
Use `repository-surface` for the public Meaningfall repository surface, and
`product-md-output` for a generated or updated `PRODUCT.md` body.

## When To Use

Use this target after:

- installing or updating product memory;
- migrating supporting memory toward the folder-backed records format;
- adding or editing the marked Meaningfall block in a host `AGENTS.md`.

This is a low-noise structural gate. It does not silently fix files.

## Inputs

Read:

1. the installed `PRODUCT.md`;
2. `product-memory/README.md`;
3. `product-memory/drafts/` and `product-memory/decisions/` records when present;
4. `product-memory/notes.md` and `product-memory/glossary.md` when present;
5. the host-owned `AGENTS.md` when present;
6. the Memory spec and the Install product-memory reference for the owning rules.

## Checks

### Installed Shape

- `product-memory/state.yaml` is not present.
- No default `facts.md` or `learnings.md` support surface is installed; facts and
  learnings route by role per the Memory spec.
- `notes.md` and `glossary.md`, when present, are single Markdown files without
  record front matter.
- `product-memory/archive/` exists only when there is superseded or historical
  material; it is Cold Archive, not an active record type.
- `product-memory/README.md` reads as a role and read-order map, not a
  hand-maintained list of every record.

### Folder-Backed Records

- Every record in `drafts/` and `decisions/` has required YAML front matter.
- Front matter parses wherever it is present.
- Draft `status` is one of the closed enum `open`, `paused`, `promoted`,
  `rejected`, `superseded`.
- Decision `status` is one of the closed enum `accepted`, `deprecated`,
  `superseded`.
- A `status: superseded` record identifies its replacement when that link is
  available.

A Markdown `## Status` grandfather exemption is a private lab concern; it does not
apply to this installed product-memory target.

### AGENTS.md

- The marked Meaningfall product-memory block in `AGENTS.md` contains no captured
  operating instruction. Captured operating instructions belong in the host-owned
  body of `AGENTS.md`, outside the marked block.

## Report

Report findings first, ordered by severity:

- **Blocking** — installed `state.yaml`; a default `facts.md` or `learnings.md`
  support surface; a folder-backed record missing required front matter; a `status`
  value outside its closed enum; unparseable front matter; or a captured operating
  instruction inside the marked Meaningfall block.
- **Minor** — wording drift or a missing optional supersession link.

Do not silently fix issues. Report them and let the human or an explicit edit
request drive changes.

If there are no findings, say the installed product memory is coherent for the
checked scope and name any checks intentionally not run.
