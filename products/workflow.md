# Workflow

Status: internal project note for the Meaningfall product family.

This is the internal working note for how ProductMD, Build Flow, Seed Loop, and adjacent external conventions relate. It is **not** public documentation, **not** a ProductMD specification, and **not** a generator contract. It records decisions, boundaries, and open questions. Anything that becomes user-facing graduates into the relevant public package under this folder.

## Principles

Durable internal principles established for the Meaningfall product family. New work should hold these unless a decision explicitly revises one.

**Design**

- **Layered, not feature-oriented.** Record meaning as cross-cutting owners; a "feature" is a view across layers, not a stored unit. Lineage: SHACL/RDF, OOUX, noun-verb analysis.
- **One altitude per owner.** Each owner sits at a single level of meaning. When content is a different altitude, give it its own owner rather than swelling an existing one (`entities` is its own owner, not part of `profile`; map structure is its own owner, while semantic composition roles live inside map `props`).
- **Cascade by dependency.** Order owners so later ones reference earlier ones: `profile → entities → conditions → actions → map → compositions → navigations → mechanics`. This minimizes backward pressure; the Seed Loop `root` pass backtracks for the rest. Internal sub-part order follows the same idea where parts depend on each other; the `map` keeps its own structure logic through branches, spaces, contained items, and props. Catalogs (`compositions`, `navigations`) sit after their hosts; the host references the catalog, never the reverse.
- **Meaning, not realization.** ProductMD records durable product meaning — not form, schema, fields, components, routes, or implementation. Every owner carries a hard "what it is not" boundary.
- **Modality-neutral; the graphical surface is one projection.** Product structure uses `map`; semantic composition roles are `shell`, `complement`, and `overlay` under `props.composition`; named navigations are shaped map projections in `navigations`. Realization guidance decides how those roles and projections become web, app, CLI, voice, API, or other surfaces.
- **Catalog form by default in generated material.** Generators and published examples prefer named `compositions` and `navigations` entries referenced from the map, even for thin entries — named catalogs read better for non-technical reviewers and give body prose stable names. Inline forms stay valid user-authored syntax that consumers preserve (decision 0051).
- **Frontmatter only when compact facts are useful.** Do not mirror every body heading into YAML. Frontmatter carries reusable facts, axes, and lists; the body explains the compact YAML and is not a second product model. `##` ≈ owners; `###` = optional explanation slots.

**Authority and structure**

- **One contract; reference, never restate.** `docs/spec.md` is the single normative source. The skill, README, and examples reference it — the skill by URL plus a minimal version-pinned fallback — and never duplicate its rules.
- **Verification is the Seed Loop `settled` gate; the criteria belong to the contract.** The loop applies the checks; the spec defines what is valid.
- **Two layers: public convention vs internal note.** `product-md/` ships; this file holds internal decisions and findings. User-facing material graduates up into `product-md/`.
- **Minimalism — no structure ahead of need.** Do not add an owner, file, or folder until a real need and the thing exist together (for example, `references/` only once a file and a pointer to it both exist). No empty scaffolding.
- **Examples are exemplary; deviations live in the docs.** Examples demonstrate the canonical syntax, order, and structure in both frontmatter and body. Allowances, rare syntax, and edge cases are described in the spec, not shown in examples.

**Process**

- **Archive, don't delete.** Preserve superseded state in the lab/reference archive so it can be compared if the new structure needs checking.

## Two layers

- **Public convention** = [`products/product-md/`](product-md/) — the shipped ProductMD package.
- **Internal note** = this file (`products/workflow.md`) — decisions, workflow thinking, open questions.

Keep them separate. User-facing material does not live here; it moves into `product-md/`.

## Repository shape

```text
products/
├── README.md
├── workflow.md        (this file — internal)
├── product-md/        (public ProductMD convention)
├── build-flow/        (guided product-composition product)
└── seed-loop/         (neutral build-and-verify discipline)

products/product-md/
├── README.md + meta (CHANGELOG, CONTRIBUTING, LICENSE, NOTICE)
└── docs/              reference material: spec.md + examples/

products/build-flow/
├── README.md
└── skills/
    └── product-brief/   (the Product Brief stage)
        ├── SKILL.md
        └── references/verification.md
```

Layout principle: in `product-md/`, `docs/` is the home for reference material (contract and examples) and the package root holds the entry README plus meta files. The interview tooling no longer lives in ProductMD — it graduated into the **Build Flow** product, where `skills/` holds the Product Brief stage.

## product-brief is the Product Brief stage of Build Flow

product-brief is now owned by **Build Flow** (`products/build-flow/`) as its first stage, Product Brief. ProductMD owns the `PRODUCT.md` format; Build Flow owns guided creation. The notes below describe the skill itself; the product boundary is recorded in [`build-flow/README.md`](build-flow/README.md) and [`README.md`](README.md).

product-brief is packaged as a single `SKILL.md` (the open Agent Skills standard) under `build-flow/skills/`, not as a `tools/` folder.

- The `SKILL.md` body is `## Interview` (soft voice — how to ask, NLU/NLG) plus `## Building the file`, which instantiates the **Seed Loop** for ProductMD: grow order over the owners, the `root`/backtrack rule, the `verification.md` oracle and output gate, plus interview steering (state ledger, keep-moving). The Seed Loop discipline itself is a separate product ([`seed-loop/`](seed-loop/)), referenced, not restated.
- product-brief runs the Seed Loop as soft Markdown executed by the model, **not** code, until determinism is genuinely needed (human removed from the loop, at-scale runs, or invisible/expensive failures). Pasting code into a chat does not execute it; the model reads it as text, so it buys no determinism over clear structured Markdown. This is product-brief's executor choice over the Seed Loop's mechanism/oracle seam — the discipline stays the same whether run soft or as code.
- It references the canonical `docs/spec.md` and `docs/examples/` by URL, plus a compact version-pinned fallback inside the file. It does not duplicate the contract.
- Two run modes from one file: an installed skill in skill-aware hosts (full mode, progressive disclosure) and a paste-in prompt in plain chats (lite mode).

### Brief output contract evolves with the accepted stack

Product Brief is Build Flow's guided initialization stage, not permanently only a `PRODUCT.md` writer. Its output contract should track the currently accepted Meaningfall product stack.

Current direction:

- ProductMD supplies the canonical `PRODUCT.md` format.
- Memory supplies the installed product-memory support shape.
- Therefore a new-project Product Brief should create `PRODUCT.md`, install `product-memory/README.md`, create supporting memory files only when populated, and create or update a host-owned `AGENTS.md` product-memory block by default unless the user opts out.

Future direction:

- If an accepted surface such as Studio, Memory Lookup, Build Flow Check, or Build Flow Realize becomes available to users, review whether Product Brief should initialize, configure, or hand off to that surface.
- Do not pre-create future surfaces. Brief follows accepted user-facing capability; it does not scaffold speculative products.

Guard:

> When a new Meaningfall capability becomes user-available, check whether Product Brief's output contract, install references, verification gates, handoff, and examples need to change.

### Skill references and scripts

The skill now has a `references/` folder holding `verification.md` (per-owner gate checks), loaded on demand via a pointer in `SKILL.md`. It was created only once a real file and that pointer existed together, per the minimalism principle (a skill loads `references/` files only when `SKILL.md` points to them, so an empty folder would do nothing). A `scripts/` folder remains deferred — add it only if the loop's mechanism ever becomes deterministic code. Do not create folders preemptively.

## Closed directions

- `agent-skills/` and `structure-yaml/` are no longer pursued. Historical copies are kept in the lab/reference archive, not in this public package. Skill packaging now lives in the Build Flow product as the Product Brief stage (`build-flow/skills/product-brief/`).
- A full pre-refactor copy of `product-md/` is kept in the lab/reference archive for comparison.

## Layer boundaries

- ProductMD owns product meaning: `profile`, `entities`, `conditions`, `actions`, `map`, and `mechanics`.
- Visual identity — tokens, colors, typography, spacing, component styling — belongs to a design system or visual styling layer, not to ProductMD. The public ProductMD package keeps this boundary generic and does not name a specific visual convention.
- `DESIGN.md` (the external Google convention) is the concrete visual-layer orientation we have in mind internally for that boundary. This repository does not own DESIGN.md and does not currently generate it; ProductMD is not defined as its counterpart, and there is no committed combined design-plus-product flow.
- UI realization wrappers (header, footer, main, aside, body, group, sidebar, responsive transforms, component choice) are intentionally out of scope for ProductMD `map` and `props.composition`; later realization guidance can map semantic roles to concrete formats.

## mechanics shape

`mechanics` is a compact internal-product-logic domain index only:

```yaml
mechanics:
  editor:
    - selection-model
    - tool-modes
  assistant:
    - intent-routing
    - escalation-policy
```

Not a decision-table DSL, not transitions inside `conditions`, not implementation code, not realization mechanics, not a replacement for `actions`. Detailed behavior stays in body prose or, only under proven future pressure, a separate later tool.

## entities lineage

`entities` uses an established term in its broad sense — the domain "things" of the product. Lineage: the Entity-Relationship model (Chen), Domain-Driven Design's Entity (Evans), Object-Oriented UX's "objects" (Prytherch), classic noun-verb analysis (nouns map to objects, verbs to operations), and RDF/SHACL classes. DDD's narrower Entity-vs-Value-Object distinction is intentionally not adopted; we use the broad ER/everyday sense.

Deliberate divergences from OOUX's ORCA (Objects, Relationships, CTAs, Attributes):

- Objects map to `entities`, CTAs map to `actions`, and the object-before-action ordering is mirrored in the cascade.
- Relationships are kept in body prose, not as structured YAML.
- Attributes (fields, schema, content types) are intentionally excluded — they are downstream, not product meaning.

Authoring nuance (also stated in the spec): a person-type can be both an `entities` object (a managed record) and a `conditions` role (the current user's behavior-changing role).

## map and composition: findings

Current conceptual findings after the 2026-06-05 product-map reset.

- `map` replaces the old separate `sitemap`, top-level `composition`, `articles`, `navigation`, and `asides` owners as the single product-map surface.
- Top-level `map` branches such as `product`, `system`, `notifications`, and `integrations` share one shape: `props`, optional `spaces`, and `contains`.
- `spaces` is only for two or more large peer logical spaces. `items` is the standard child container and may contain one item.
- `props` is the only property container. Do not add `meta`.
- `props` is open for local product-specific properties except ProductMD-reserved prop names. Currently reserved: `name`, `home`, `reset`, and `composition`.
- Collection facts live under `entities.<name>.collection: true`, not in `map` props; do not use `props.open: true`, `collection: true` in `map`, or representative `sample-*` items only to show collection membership.
- `props.composition` is intentionally small and modality-neutral: `shell`, `complement`, `overlay`. Content is the item itself and body guidance, not a composition role.
- `props.reset` resets selected prop groups at the current scope, and `does_not_apply` suppresses one inherited named entry inside a prop group.
- Composition roles mark generalized semantic structure, not UI wrappers, custom page contents, components, or layout landmarks.
- A later realization document can explain how map items and composition roles translate into web, app, CLI, voice, API, or other concrete formats.

## Legacy reuse

Legacy Meaningfall material may hold useful prior decisions, vocabulary pressure, or lessons; check it before inventing a new approach. It does not constrain names or structure for the current ProductMD line.

## Open questions and deferred work

- A later whole-product generator is unresolved and is **not** part of the current Product Brief stage. Product Brief's current accepted scope is product-memory initialization around `PRODUCT.md`; a whole-product generator, if it happens, would be a later Build Flow stage, deliberately designed when there is concrete pressure — not a current commitment.
- Whether and when Build Flow might add visual-direction generation (or DesignMD, component, stack, or prototype stages) is open and deferred, not a current commitment.
- Content/contract questions still open: possible `scope`/`expression` owners, and whether repeated real use needs richer `props.composition` substructure beyond empty role branches.
- Escape-hatch gap, deferred (2026-06-11): no named convention distinguishes a deliberate local extension (a custom field or body section a project keeps on purpose) from accidental drift — consumers report both forever. Today it routes through project-specific interpretation prose (spec "A project may use the Markdown body…"). Revisit only when a real validator makes the permanent-report noise material.

## Not now

Do not finalize: a generator product, a formal address grammar beyond what `map` already implies, a component or pattern catalog, formal decision tables, or a format-specific realization document before the new map shape is exercised.
