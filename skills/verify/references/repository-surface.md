# Repository Surface Verification

Applied checks for the public Meaningfall repository surface. This target checks
that public routing is coherent with root `SPEC.md`, root `README.md`, and
`index.yaml`.

Authority stays with the owning contracts. `index.yaml` is routing metadata, not
narrative authority, and this reference does not define product meaning.

This target applies to a public Meaningfall repository surface. It does not
install `index.yaml`, `state.yaml`, or any other machine-readable state file into
an installed user workspace. `product-memory/state.yaml` remains intentionally
absent from installed product memory.

## When To Use

Use this target after changes to:

- public paths, folders, or repository layout;
- root `README.md`, root `SPEC.md`, or `index.yaml`;
- format, module, or root skill entrypoints;
- public routing language that could point readers or agents to the wrong
  surface.

Do not use this target as a broad documentation-quality audit. It is a
low-noise structural gate.

## Inputs

Read:

1. root `SPEC.md`;
2. root `README.md`;
3. `index.yaml`;
4. the public files and folders named by those surfaces when needed.

Do not read private `process/` material to decide whether the public repository
is coherent. Private drafts or decisions may explain why a change happened, but
the public surface must stand on public files.

## Checks

### Repository Map

- `index.yaml` parses as YAML.
- Paths listed in `index.yaml` exist relative to the public repository root.
- `index.yaml` entries point only to public repository surfaces.
- `index.yaml` does not point into private workspace paths such as `process/`.

### Public Entrypoints

- Root `README.md` links to existing public surfaces.
- Root `README.md` names the current primary public formats, modules, and skills
  without pointing to removed canonical paths.
- Root `SPEC.md` names existing current public surfaces in its ownership map.

### Current Surface Set

- Current public formats named by `README.md`, `SPEC.md`, or `index.yaml` exist.
- Current public modules named by `README.md`, `SPEC.md`, or `index.yaml` exist.
- Current root skills named by `README.md`, `SPEC.md`, or `index.yaml` exist.
- Listed skill target references exist.

### Boundary Checks

- Public paths do not route to private `process/` material.
- `Meaningfall/` does not contain a live installed-workspace `product-memory/`
  surface.
- `Meaningfall/` does not contain a local installed-workspace `skills/` surface
  separate from the public root skills.
- Compatibility or historical paths, if present, are visibly marked as
  compatibility or history rather than current canonical homes.

## Dependency-Ordered Review

When a public surface change affects several files, check from the owning
contract outward, then root back:

1. Identify the owning contract or procedure for the changed surface.
2. Check downstream routes, maps, and entrypoints against that owner.
3. If a downstream file needs a rule the owner does not provide, report the
   owner gap instead of normalizing the downstream file around an implicit rule.
4. When containment is uncertain, run the full repository-surface gate.

This is an application of Meaningfall's dependency-ordered review discipline,
not a new Seed Loop contract.

## Report

Report findings first, ordered by severity:

- **Blocking** — broken listed path, stale canonical route, private-surface leak,
  missing current public surface, or public routing that contradicts root
  `SPEC.md`.
- **Minor** — wording drift, redundant routing, or compatibility wording that is
  clear enough but likely to become stale.

If there are no findings, say the repository surface is coherent for the checked
scope and name any checks intentionally not run.
