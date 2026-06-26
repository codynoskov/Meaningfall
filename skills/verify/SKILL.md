---
name: verify
description: Verify Meaningfall artifacts against their owning contracts and report findings. Use when a user asks to verify, review, audit, check, validate, or run an output gate for PRODUCT.md/ProductMD output, product memory installation, format/module boundaries, skill boundaries, or other Meaningfall public surfaces.
---

# Verify

Verify checks Meaningfall artifacts against the contracts that own them. It
owns the review process, not the underlying format or module specs.

Supported target:

- **product-md-output** — verify a created or updated `PRODUCT.md` as Meaningfall
  output.
- **repository-surface** — verify the public Meaningfall repository surface,
  routing map, and primary public entrypoints.
- **product-memory** — verify an installed product-memory surface: installed shape,
  folder-backed record format, and `AGENTS.md` block hygiene.

Future targets may be added here as Meaningfall gains more verification surfaces.

## Workflow

1. Identify the verification target. If the user does not name one, infer the
   narrowest target from the artifact.
2. Read the target reference before reviewing.
3. Read the owning format or module contracts named by the target reference.
4. Check the artifact against the target reference and owning specs.
5. Report findings first, ordered by severity, with file/line references when
   possible.
6. Separate blocking findings from minor wording or drift risks.
7. Do not silently fix issues unless the user asks for edits.

## Targets

### product-md-output

Use `references/product-md-output.md` when checking a generated or updated
`PRODUCT.md`.

This target applies:

- ProductMD for format and product-meaning ownership;
- Memory when supporting product memory or handoff routing is involved;
- Seed Loop's settled gate when the artifact was produced by a grow/root process.

### repository-surface

Use `references/repository-surface.md` when checking the public Meaningfall
repository surface after routing, ownership, path, or public-entrypoint changes.

This target applies:

- root `SPEC.md` for public surface roles and repository-level boundaries;
- root `README.md` for public entrypoint routing;
- `index.yaml` as the machine-readable repository map.

### product-memory

Use `references/product-memory.md` when checking an installed product-memory
surface, not the public repository surface and not a generated `PRODUCT.md` body.

This target applies:

- Memory for product-memory governance and the records format;
- the Install product-memory reference for installed shape and `AGENTS.md`
  integration mechanics.

## Action Modes

Per root `SPEC.md` Action Modes and decision 0072, Verify grants:

- `automatic`: running checks inside an accepted workflow; reporting findings.
- `suggested`: proposing fixes.
- `explicit`: applying fixes. Verify never edits files silently.
