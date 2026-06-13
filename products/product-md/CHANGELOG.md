# Changelog

## Unreleased

No changes yet.

## v0.1.11 - 2026-06-13

Packaging: `product-brief` moved out of the ProductMD package into the standalone **Build Flow** product.

- Moved the `product-brief` skill from `skills/product-brief/` to the Build Flow product at `../build-flow/skills/product-brief/`. ProductMD now owns the `PRODUCT.md` format only; guided creation (interview and generation procedure) is owned by Build Flow, whose first stage, Product Brief, creates or updates a `PRODUCT.md`. The README and CONTRIBUTING publication boundary were updated to point at Build Flow.
- The ProductMD contract (`docs/spec.md`) is unchanged by this move; the skill still references the spec by URL.

Tooling: the generation harness was extracted into a neutral Seed Loop discipline.

- Extracted the generation harness from `product-brief` into a separate, neutral, domain-agnostic **Seed Loop** discipline (grow the owners in order, root each back to its seed, repeat until settled). `product-brief`'s `## Harness` section is now `## Building the file`, which instantiates the Seed Loop for ProductMD — cascade/grow order, the `references/verification.md` oracle and output gate, and interview steering — and references the discipline instead of restating it.
- The ProductMD contract (`docs/spec.md`) is unchanged by this move. `references/verification.md` now names the Seed Loop `settled` gate rather than "the harness output gate".

## v0.1.10 - 2026-06-11

Body guidance refinement:

- Added the enumeration ladder as a general body-prose rule: plain prose for simple or interwoven meaning, a generalizing phrase with a colon for parallel self-evident elements (the phrase also names the group), a list when each element needs its own clause (name — meaning, lead-in before, shared rules after); parallelism moves prose to a colon, per-name explanation moves the colon to a list; groups compose two levels without nesting.
- Added the entity variance ladder: lifecycle variance stays one entity described per state value (baseline first); durable actor-facing variants crystallize as named `views` with prose connecting conditions to views (no `when` field); variants that stop sharing operations, lifecycle, and relations are two entities joined by a relation — the test is continuous shared identity and history.
- Removed optional bold labels from body prose: descriptive aspects (`purpose`, `contents`, `behavior`, `notes`) are written as ordinary prose without `**Purpose:**`-style prefixes, and the situational signposts `**Use when:**`, `**Shared rule:**`, and `**Do not infer:**` are dropped.
- Added the `Important:` note as the one accepted bold signpost construction, set entirely in bold (marker and sentence together): an exceptional note at the end of an element's description, reserved for rules whose violation causes irreversible, legal, or trust harm and that a reader would plausibly get wrong; many such notes in one file signal they should be rewritten as ordinary prose. Bold product names, entity names, and list labels remain allowed when they aid scanning.
- Added the two realization reading modes: `PRODUCT.md` as generation input and as a conformance contract binding every realized render, fixed or generated; conformance checks derive from the file itself.
- Clarified triggers as initiation facts of actions: state-triggered actions fire on transitions into states recorded in `conditions`, schedules stay in prose, and recurring trigger policy connecting several actions is a `mechanics` domain.
- Added a `Reading:` line to the `## About This File` template: frontmatter holds compact facts, body prose interprets without restating, backticked product-address references in prose resolve to frontmatter addresses, and syntax literals may also use code style.
- Named inputs in the actions body guidance: described at meaning level (what is asked, why, required versus optional, sensitivity), never as input fields, controls, or validation; outputs are named through recorded `entities` and `conditions` addresses. Many inputs are grouped by meaning — groups are durable, step or screen splits are realization; ordering rules only when order is itself product meaning. Output weight routes its home: ephemeral results are action feedback, durable or actionable outputs are entities with their own sections, derived result surfaces are map items. For input-heavy elements, feedback coverage includes validation meaning — what is checked, why, and what the actor learns and can do on failure — never format or field mechanics.
- Added condition-variance placement rules for body prose: small variance is a clause inside the affected aspect, large variance describes the element per condition value (baseline first, list form when variants carry their own meaning); variance is described only against recorded `conditions`, and a recorded state no prose connects to anything is an orphan signal. The product-brief skill now asks what each recorded role and state changes and gates output on state-consequence coverage.
- Bridged the generic descriptive aspects to owner-specific refinements: aspects are calibrated for map material, and the owner sections' own prose sets (actions, mechanics, conditions, entities) win for their elements; flagged the two misleading aspects (entity `contents` is never fields or schemas; composition and navigation `contents` is already modeled by frontmatter shape); an inapplicable aspect needs no prose or placeholder.
- Extended skill enforcement to the remaining body rules: the interview asks about collected and sensitive inputs; the output gate checks two-way frontmatter-body coverage, product-address reference resolution, and meaning-level input coverage; verification checks trigger-state recording and output-weight promotion.
- Promoted `feedback` to a named descriptive aspect (name, purpose, contents, behavior, feedback, notes): how the product answers the actor — acknowledgment, validation outcomes, progress, errors and recovery, empty results — at meaning level, never as components. The product-brief skill now asks about feedback for primary and risky operations and gates output on its body coverage. Examples audited for feedback and meaning-level input coverage: `case-brief`, `field-market`, `harbor-hotel`, `lumen-docs`, `ops-console`, `carebridge`, and `signal-lantern`; `signal-lantern` also gained the `Reading:` line.

## v0.1.9 - 2026-06-10

Named navigations separated from composition:

- Added optional top-level `navigations` after `compositions` and before `mechanics`: a catalog of named, shaped map projections (default projection, breadcrumbs, or curated `items`/`links`).
- Moved the navigation grammar (`from`, `depth`, `type`, `items`/`links`, `override`, breadcrumbs) out of the composition section into the `navigations` owner; composition roles return to role markers plus thin hosting.
- Redefined role-hosted `nav` as a mapping from exposure name to navigation name; the exposure name is the local role at that place, the navigation name is the reusable shaped view.
- Kept the host-to-catalog reference direction: composition roles and profiles reference navigations by name; a navigation entry never lists the scopes where it applies.
- Kept inline projection bodies inside `nav` valid, with catalog references as the preferred authored and generated form.
- Accepted map items as navigation surfaces for machine-facing indexes (such as an `llms.txt`): the item's content is a named navigation, stated in the body.
- Kept condition-dependent navigation in body prose referencing `conditions` axes and navigation names; no condition field on navigation entries.
- Added an authoring preference: generators and published examples default to catalog form for `compositions` and `navigations`, even for thin entries; inline remains valid user-authored syntax.
- Disambiguated scalar values after independent audit: inside `nav`, a scalar exposure value is always a navigation name; the scalar depth shorthand is valid only under top-level `navigations`; inline projection bodies inside `nav` use mapping form.
- Defined `override` subject addressing: immediate children of the navigation's `from` root by bare name, deeper subjects by relative dot path.
- Split `does_not_apply` wording: cascade suppression of inherited roles/exposures versus projection refinement inside a navigation's `override`.
- Added conditions guidance distinguishing session/user state axes from instance-configuration axes that gate action families.
- Demonstrated navigations in the `lumen-docs` example, including `override` to keep archived material out of ordinary guide navigation.

## v0.1.8 - 2026-06-09

Reusable composition profiles:

- Added optional top-level `compositions` after `map` and before `mechanics`.
- Added `props.composition.uses` for applying a named composition profile from a map scope.
- Kept inline `props.composition` as the default and preferred shape for simple products.
- Required a single `props.composition` value to be either inline roles (`shell`, `complement`, `overlay`) or one `uses` reference, not both.
- Defined `uses` as reference-only: no local role deltas, `reset`, or `does_not_apply` inside the same composition value.
- Accepted group-level usage such as `contains.props.composition.uses` and `spaces.props.composition.uses`.
- Defined cascade behavior: local `uses` replaces inherited composition at that scope; it does not merge with inherited inline roles or inherited profile roles.
- Kept `map` as the accepted product-map owner and kept old separate top-level owners `sitemap`, singular `composition`, `articles`, `navigation`, and `asides` superseded.

## v0.1.7 - 2026-06-09

Entities and map containment clarification:

- Replaced `entities.items` with direct `entities.<name>` entries.
- Removed fixed entity `type` values. ProductMD no longer uses `type: collection`, `type: canvas`, or implicit `type: default`.
- Restored `collection: true` as the collection marker, but only under `entities.<name>`, not in `map`.
- Clarified that `views` are semantic representation variants of an entity meaning. Omitted `views` means no special view variants are recorded in frontmatter, not "no representation."
- Kept `relations` as the structured home for semantic associations between entities; entity nesting is not used for relationships.
- Replaced structural `map.*.items` containers with `contains`, while keeping "item" as the general term for a durable product-map node and keeping `nav.items` for explicit curated link entries.
- Clarified that a map item is broader than an entity; do not mirror the whole map into `entities`. Promote a map item to `entities` only when it needs collection facts, views, relations, cross-owner references, or body explanation.
- Documented the current owner cascade as `profile -> entities -> conditions -> actions -> map -> mechanics`, with general backtracking when later owners reveal missing earlier meaning.

## v0.1.6 - 2026-06-08

Entities model cleanup:

- Replaced the old flat-list `entities` shape with `entities.items`.
- Added narrow item `type` values: omitted type means default, `type: collection` marks a same-shaped series, and `type: canvas` marks a durable data, relationship, spatial, graph, or freeform working-surface meaning.
- Moved collection marking out of `map`: `collection: true` and normalized `props.collection: true` are no longer the current way to mark collections.
- Added item `views` for additional non-baseline semantic representations of the same item meaning. `self-contained` is the implicit baseline and should not be listed.
- Added item `relations` for durable semantic associations between items, avoiding nested collections for non-containment relationships.
- Kept `map` focused on structural presence; `type`, `views`, and `relations` live in `entities`.
- Rejected `embeds`, `media`, `figures`, `sections`, `flows`, `forms`, `components`, `tables`, and `pages` as peer entity groups or item types for now.
- Updated the specification, README, product-brief skill verification, reconstruction harness, and examples to use the new entities model.

## v0.1.5 - 2026-06-05

Product map reset:

- Replaced the separate `sitemap`, top-level `composition`, `articles`, `navigation`, and `asides` owners with a unified `map` owner.
- Set the v0.1.5 frontmatter cascade to `profile`, `entities`, `conditions`, `actions`, `map`, `mechanics`.
- Added top-level `map` branches such as `product`, `system`, `notifications`, and `integrations`, all using the same branch shape.
- Standardized map structure around mappings: `spaces` for two or more large peer logical spaces, `items` for named child items, and `props` as the canonical property container.
- Added compact shorthand for ProductMD-reserved props on branches, spaces, and items; for example `collection: true` normalizes to `props.collection: true`, while custom local props stay inside `props`.
- Kept `props` open for local product-specific properties, with ProductMD reserving only selected prop names such as `name`, `home`, `collection`, `reset`, and `composition`.
- Added `props.composition` with the accepted semantic roles `shell`, `complement`, and `overlay`; content is the item itself and body guidance, not a composition role.
- Added reserved `nav` exposures inside composition roles, preserving the useful `from`, `depth`, and `override` navigation logic without restoring a top-level `navigation` owner or layout areas.
- Added `links` as a compact bucket shorthand for explicit link-heavy navigation exposures.
- Replaced list-based product trees with mapping-based `items`; lists are now reserved for ordered or repeatable sequence-bearing values.
- Replaced open collection marker `"..."` with `collection: true` or normalized `props.collection: true` on collection items.
- Added `props.reset` and `does_not_apply` for prop-group reset and negative override behavior.
- Updated the README, specification, product-brief skill verification, reference-test prompts, and complete examples to use the new `map` model.

## v0.1.4 - 2026-06-03

Clarifications (no new owners or breaking changes):

- Body descriptive vocabulary: a described element is covered in the priority order name -> purpose -> contents -> behavior -> notes — aspects to cover in prose, not required labels. Added `contents` (a page or element's makeup) as the home for page-structure and generation hints; an overloaded `notes` signals a missing aspect to route to review.
- Body sections are written only where they add non-obvious meaning; trivial or self-evident owners get no section, and a deliberately omitted owner is not explained.
- `entities`: list a noun only when it is irreducible to a single statement — a thing nothing operates on but that exists or relates (an actor, a related object), or one shared by several statements needing one canonical name. A noun carried by a single destination or a single action does not earn an entity; thin content/doc sites may have few or none.
- `conditions`: a condition must change what the product does with the same content. Different versions, editions, or pages are `sitemap` destinations, not states; a single-value context axis is scope; release/version status stays out.
- `actions`: an action produces an effect within the product. A link is navigation, an install command is content, and an operation performed entirely in an external system is not the product's.
- `profile.identity`: public addresses (repository, social, community, status, store) are identity facts grouped under `links`, not `sitemap` destinations; the product's own home is `home: true` in `sitemap`, not a profile field.
- `sitemap`: top-level entries are the product's primary destinations; subordinate areas nest under their hub, and external links live in `profile.identity` or a page's body. `"..."` is the final entry of its list, and an open collection still has a modeled item type (its index structure in the body, item-page shape in `articles`/`composition`). The Markdown body is the place for per-destination purpose and contents as page-generation guidance.
- `composition`: a destination-scoped variant is keyed by its full sitemap address (root-qualified, e.g. `acme.docs`), so it is clear where the composition changes; the product-wide set uses the root key, while generic or page-type sets (`page`, `article-detail`) and the `all`/`base` modifiers keep descriptive names.
- Examples: `lumen-docs` and `field-notes-library` updated to demonstrate the entity, links, and per-destination sitemap-body guidance; `field-market` and `lumen-docs` composition keys aligned to full sitemap addresses.

## v0.1.3 - 2026-06-02

Composition addressed entities:

- Added optional address-keyed companion owners after `composition`: `articles`, `navigation`, and `asides`.
- Documented concrete article addresses with stable appearance names such as `in-section` and `in-card`; `main.article` implies `self-contained`.
- Simplified navigation metadata into address-keyed `navigation` entries with compact `from`, `depth`, and `hide` keys, replacing inline `nav` exposure and general `override` in the basic syntax.
- Added `asides` for concrete aside addresses and semantic cases such as `empty` or `with-related-articles`, while keeping aside ownership encoded by the address.
- Strengthened body guidance: prose should distinguish nearby semantic options and explain non-obvious meaning without translating frontmatter line by line.
- Updated the cascade to `profile`, `entities`, `conditions`, `actions`, `sitemap`, `composition`, `articles`, `navigation`, `asides`, `mechanics`.
- Replaced sitemap child `system` groups with the reserved `system_<product-root>` peer key in the spec, and migrated examples and navigation to match.

Clarifications:

- Added a `Relationship To Other Files` -> `Realization` note: ProductMD records durable meaning, selected semantic axes, and stable semantic regions — not components, widgets, layout mechanics, transient UI state, or loading behavior.

## v0.1.2 - 2026-06-01

Composition discipline:

- Removed layout wrappers (`body`, `content`, `group`, `sidebar`) from the closed `composition` vocabulary.
- Reclassified utility values (`brand`, `breadcrumbs`, `controls`, `search`, `status`, `toolbar`, `filters`) as predefined templates — open, recommended, not closed.
- Added a naming grammar with the `kind_qualifier` rule for same-kind siblings and disallowed qualifier categories (location, role, sitemap context, page identity, content type).
- Documented nested composition sets: a set key such as `page` may nest inside another set as an inner shell within persistent surrounding regions.
- Tightened overlay vocabulary: `dialog` is the only fixed scoped kind; `drawer`, `popover`, `toast`, and `floating` are overlay templates.
- Added an excluded UI/component vocabulary list, a recursion note for the `article`/`section`/`aside` trio, and a deferred roadmap of future fixed elements (`figure`).

Owners and cascade:

- Added an optional `entities` owner for the product's durable domain nouns (a flat list, or grouped by domain at scale). Relationships and states stay in the body and `conditions`.
- Added an optional `mechanics` owner for compact internal product-logic domains, with mechanics-heavy examples.
- Set the frontmatter cascade to `profile`, `entities`, `conditions`, `actions`, `sitemap`, `composition`, `mechanics` — `actions` precedes `sitemap` and `composition`, so operations are defined before the destinations and regions that host them.
- Clarified that `home: true` marks the product's primary useful entry point, not an about/company page by default.

Tooling and packaging:

- Repackaged `product-brief` as an Agent Skill at `skills/product-brief/SKILL.md` — a soft `## Interview` voice plus an explicit `## Harness` — replacing the prior prompt, tool spec, and templates. It references `docs/spec.md` and `docs/examples/` instead of restating format rules, with per-owner checks in `skills/product-brief/references/verification.md`.
- Consolidated reference material under `docs/` (moved `examples/` to `docs/examples/`), and dissolved the standalone discovery checklists — distilling their verification into the skill while keeping field vocabulary in the spec.
- Rewrote the README as a front door with two ways to run `product-brief` (installed skill or paste-in prompt).

Other:

- Promoted block-list YAML form as the published example style; converted examples and snippets from inline `[a, b, c]` to block lists.
- Generalized visual-scope boundaries to "a design system or visual styling layer"; the public package names no specific external visual convention.
- Flattened the example suite into a single set of named-product folders under `docs/examples/`.
- Folded an earlier separate-composition-format exploration into ProductMD `composition` rather than shipping it separately; its discipline lessons are integrated here.

## v0.1 - 2026-05-25

First public release of ProductMD.

- Defines `PRODUCT.md` as a single plain Markdown file with optional YAML frontmatter.
- Establishes the v0.1 frontmatter cascade: `profile`, `conditions`, `sitemap`, `composition`, `actions`.
- Documents Markdown body guidance for orientation, assumptions, boundaries, interpretation, feedback, validation, and recovery expectations.
- Includes complete examples for body-only, minimal, content, documentation, booking, marketplace, operations, AI-review, and regulated intake situations.
- Includes non-normative discovery checklists for authors, agents, and interview tools.
- Includes `product-brief`, a prompt/procedure workflow for creating or updating ProductMD files with an LLM.
- Uses Apache License 2.0 for the public package.
