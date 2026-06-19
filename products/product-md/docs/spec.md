# PRODUCT.md Specification

Status: v0.1.11 specification.

`PRODUCT.md` is a self-contained, plain-text representation of durable product meaning. It describes what a product is, who or what it serves, which things it is about, which context changes behavior, which product-map branches, spaces, items, semantic composition roles, reusable composition profiles, and named navigations matter, which operations matter, which internal product-logic domains must not be lost, and which supplied or external references should guide future work.

`PRODUCT.md` is product input, not generated output. It records known, chosen, supplied, or intentionally open product meaning so humans, agents, and tools can generate, review, implement, and maintain product work without inventing context.

A `PRODUCT.md` file may contain two parts: optional YAML frontmatter and a Markdown body. The YAML frontmatter contains compact machine-readable product facts and selected semantic axes. The Markdown body contains human-readable orientation, rationale, assumptions, boundaries, review notes, and interpretation guidance. Frontmatter provides the compact source; prose explains how to apply it.

References in `PRODUCT.md` are input sources. `profile.references` may include supplied documents, external standards, policies, laws, UX guidance, platform rules, brand notes, source documents, or examples the user wants agents to consult. A generated product page, future policy surface, route, implementation file, or planned output is not a reference.

A project may use the Markdown body to explain project-specific interpretation, boundaries, assumptions, or reference usage for its own ProductMD file. It should not redefine ProductMD top-level fields, encode agent procedure, or treat generated output as existing source.

## File Name

The canonical file name is:

```text
PRODUCT.md
```

Use uppercase to match root-level convention files such as `README.md` and `AGENTS.md`.

## File Shape

A `PRODUCT.md` file may contain:

1. Optional YAML frontmatter for compact, machine-readable product facts.
2. Markdown body content for orientation, rationale, assumptions, boundaries, and interpretation guidance.

Both parts are optional. A body-only `PRODUCT.md` is valid when product guidance is still prose-only or when structured facts have not been selected yet.

```md
---
profile:
  identity:
    name: ExampleProduct
    kind: product

entities:
  document: {}

conditions:
  context:
    platform:
      - web
  states:
    account:
      - anonymous
      - authenticated

actions:
  account:
    - signin

map:
  product:
    contains:
      props:
        composition:
          uses: reading
      home:
        home: true

compositions:
  reading:
    shell:
      nav:
        local: local-section
    complement:
      related: {}

navigations:
  local-section:
    from: -1
    depth: 1

mechanics:
  editor:
    - selection-model
---

# ExampleProduct

## Overview

ExampleProduct helps...
```

## Authoring Model

### Cascade

When frontmatter is present, top-level fields appear in this order:

```text
profile -> entities -> conditions -> actions -> map -> compositions -> navigations -> mechanics
```

Earlier fields establish context for later fields. If a later field needs a missing audience, market, state, permission, lifecycle, destination, legal fact, action, or product-logic domain, update the earlier owner first or explain the unresolved pressure in the body.

Owner references normally point backward: `map` reads the already-defined `entities`, `conditions`, and `actions`. The forward references are catalog references: `props.composition.uses` names a profile defined just after `map` in `compositions`, and navigation exposures inside composition roles name entries in `navigations`. Read `compositions` and `navigations` as referenced catalogs, like `entities`, placed after their hosts only because their entries are anchored from map and composition scopes — not as later processing stages. The host always references the catalog; a catalog entry never lists the places where it applies.

Use the exact top-level names `profile`, `entities`, `conditions`, `actions`, `map`, `compositions`, `navigations`, and `mechanics`. ProductMD v0.1 does not define aliases.

All fields are optional. Include exact facts, selected semantic axes, and known-needed `TBD` placeholders. Omit fields that do not help yet.

Use `TBD` only when a fact or axis is known to matter but the exact value has not been supplied. Do not fill a file with placeholders.

The body is captured alongside the cascade. It is not an additional frontmatter field.

Owner roles:

- `profile` — product identity, audience, legal/formal context, and input references.
- `entities` — named product meanings that need semantic facts.
- `conditions` — behavior-changing states and context.
- `actions` — durable product operations.
- `map` — durable product-map items and containment.
- `compositions` — reusable composition profiles referenced from map scopes.
- `navigations` — named, shaped projections of the map referenced from composition roles.
- `mechanics` — compact internal product-logic domains.
- body — explanation, boundaries, rationale, and do-not-infer guidance.

`entities` and `map` are related but not interchangeable: entities name meanings; map preserves structural containment and reachability. `actions` and `mechanics` have a similar split: actions name operations; mechanics preserves internal logic domains that govern or connect operations, states, and structure without becoming workflow or implementation detail.

Generators and published examples should prefer catalog form: named `compositions` and `navigations` entries referenced from the map, even when an entry is thin. Named catalogs read better for non-technical reviewers and give body prose stable names to explain. Inline composition and inline navigation projections remain valid authored syntax; consumers preserve them on user-authored files.

### Contribution Placement

ProductMD is open to user additions, but an addition becomes final ProductMD content only after it has a clear owner. Treat free-form user input as source material first, then classify it against the cascade.

When a user adds a sentence, paragraph, heading, or frontmatter field, split mixed material into atomic claims before placing it. A single paragraph may contain an identity fact, a state, a map item, an operation, a risk boundary, and implementation detail; those do not share one owner merely because they arrived together.

Use this placement guide:

| Addition type | Primary owner |
| --- | --- |
| Product name, category, audience, provider, public link, legal/formal fact, supplied source | `profile` |
| Named product meaning, collection fact, semantic view, durable relation | `entities` |
| Behavior-changing context, role, permission, market, platform, lifecycle, access, status, or state | `conditions` |
| Operation that creates, changes, sends, approves, resolves, recovers, or otherwise has product effect | `actions` |
| Durable product item, system crossing, notification surface, integration touchpoint, branch, space, containment, or reachability | `map` |
| Reusable semantic composition roles shared across map scopes | `compositions` |
| Deliberately exposed map projection, breadcrumb, local navigation, directory, related-resource set, or curated link set | `navigations` |
| Cross-cutting internal product logic such as ranking, assignment, pricing, permission resolution, routing, scheduling, policy handling, or game rules | `mechanics` |
| Rationale, assumptions, boundaries, non-goals, feedback and recovery meaning, review notes, interpretation, or do-not-infer guidance | body |
| Implementation detail, component choice, generated route, file path, API endpoint, style token, task procedure, or volatile release plan | outside ProductMD unless it has become durable product meaning |

If the addition fits several owners, split it and write each part where it belongs. If the right owner is unclear, keep the material in body prose as a review note until it can be placed; do not invent a new top-level frontmatter key as a parking lot.

Placement follows the cascade. If a later owner needs an earlier missing fact, update or propose the earlier owner first. For example, adding an action that depends on an unrecorded role should prompt a `conditions` update; adding a map item that represents a repeated object may prompt an `entities` update; adding a navigation exposure may prompt a `navigations` entry and the `map` or `compositions` host that references it.

Before adding new material, check whether the meaning is already covered. If it is fully covered, do not duplicate it. If it is partly covered, merge the sharper detail into the existing owner or body paragraph. If it conflicts with existing meaning, preserve the conflict as an open review issue in body prose until a human decision resolves it.

Tools may present likely destinations to the user instead of asking them to know ProductMD vocabulary. Offer only plausible destinations plus a free-form body option. A good prompt says, in effect: this looks like an entity, condition, action, map item, mechanic, or body note; choose the intended meaning, or keep it as prose for later review.

### Frontmatter

Frontmatter stores compact structure that humans, agents, and tools can read directly.

Use frontmatter for exact product facts and selected semantic axes, not for explanation. Do not put rationale, prose instructions, TODO notes, legal advice, review notes, generated-output URLs, future pages, future actions, implementation recipes, or "should" statements in frontmatter.

Frontmatter is not a complete inventory of the realized application. Runtime details, component states, framework behavior, route implementation, validation mechanics, generated UI coverage, and adapter behavior belong outside ProductMD unless they become durable product meaning.

Examples and illustrative snippets should write frontmatter lists in block form (one `-` item per line) across `conditions.context`, `conditions.states`, `actions`, ordered flow-like values, and `mechanics`. `entities` and the main product map use mappings at the top level for entity names and map items; `views` and short-form `relations` are the common entity-level list exceptions. Inline form (`key: [item, item]`) is valid YAML and consumers should preserve it on user-authored files, but published examples and generators should default to block lists for readability.

### Body

The Markdown body carries durable product guidance that is too explanatory, broad, or procedural for compact frontmatter.

Use the body for:

- non-obvious frontmatter values and product-specific meanings
- assumptions, boundaries, and non-goals
- review-sensitive placeholders and source dependencies
- product principles and expression direction
- feedback, validation, recovery, and confirmation expectations
- product mechanics that need prose because the compact domain index is not enough
- downstream coverage that should not become frontmatter
- project-specific interpretation of this ProductMD file

The body should enrich frontmatter, not translate it line by line.

Body prose should not restate ownership, nesting, or existence already encoded by the frontmatter map. Use body prose for meaning that frontmatter cannot express compactly: purpose, contained meaning, shared rules, condition-sensitive behavior, exceptions, references to other ProductMD facts, and do-not-infer guidance.

Restatement to avoid: "home contains docs." Enrichment to keep: "`docs` is the task reference surface, not a marketing library."

Write a body section only where it adds non-obvious meaning. If an owner is trivial or self-evident from its frontmatter — a single-value context, an obvious destination — omit its body section rather than narrating it. Do not add a section to explain an owner the file deliberately leaves out; absence needs no prose. Every body paragraph should carry interpretation, a rule, a boundary, or do-not-infer guidance that the frontmatter cannot, not a restatement of what the frontmatter already shows.

The complement also holds: do not silently leave a frontmatter element undescribed. Every element present should be covered in the body — at least its purpose — unless its name alone already says everything, which is common for leaf destinations and obvious facts. A nested destination or sub-element may be covered within its parent's description, but it should be identifiable there, not buried in a clause or dropped.

For map-heavy material, body prose has a semantic distinction role: it helps humans and agents choose correctly between nearby branches, spaces, items, and composition roles. Write the descriptive aspects as ordinary prose, without bold labels. Do not print `**Purpose:**`-style label prefixes; they make body prose harder to read.

The one accepted bold signpost construction is the `Important:` note, set entirely in bold — the marker and the sentence together: `**Important: voiding does not delete an invoice; it stays reachable for audit.**` Use it only for an exceptional, situational note that must not be missed — a rule whose violation causes irreversible, legal, or trust harm and that a reader or renderer would plausibly get wrong without the mark. Place it at the end of the element's description. Most descriptions have no `Important:` note; if a file grows many of them, they are no longer exceptional and should be rewritten as ordinary prose. This does not forbid bold product names, entity names, or list labels when emphasis makes prose easier to scan; it forbids using bold labels as a shadow template for descriptive aspects.

When describing a modeled element, prioritize its meaning in this order: **name**, **purpose**, **contents**, **behavior**, **feedback**, **notes**. The name is the element's frontmatter address and is not repeated in prose. `purpose` is why the element exists; `contents` is what a page or element is made of — its sections, parts, and sub-collections; `behavior` is how it works or applies; `feedback` is how the product answers the actor — acknowledgment, the meaning of validation outcomes, progress, errors and recovery, and empty results, at meaning level, never as components; `notes` are caveats, exceptions, or do-not-infer guidance. Feedback applies to elements an actor operates; a purely informational element has none, and that needs no prose. This is a priority order, not a required template: a self-evident element needs no description, and many need only a purpose. When you do explain, lead with purpose. Cover these as aspects of ordinary prose in this order, without label prefixes, and do not fill them in mechanically.

Parallel meanings escalate through three forms, and the same ladder serves any enumerable aspect — contents, inputs, condition variants. Plain prose carries simple or interwoven meaning, where shared rules bind the elements more than parallelism separates them. A generalizing phrase with a colon carries several parallel elements whose names speak for themselves — every post carries a durable frame: author, publication date, and topic tags — and the phrase also names the group, giving later prose a stable concept to reference. A list carries several parallel meanings when each needs its own clause: one line per item in the form name — meaning, a lead-in phrase before the list, and shared rules as prose after it. The thresholds: parallelism moves prose to a colon; needing a dash of explanation after each name moves the colon to a list. Groups compose two levels without nesting: a group is a list item, its members an inline enumeration inside it. Escalate under pressure of real meaning, never by template — a two-item list and a one-item list are signs of mechanical filling.

An element's aspects may vary under recorded `conditions`, and this variance is often the meaning that matters most. Say it where it lives: a small variance is a clause inside the affected aspect — editable while the invoice is `draft`; a large variance describes the element per condition value, baseline first, as a list when several variants each carry their own meaning. Describe variance only against conditions the frontmatter records — needing an unrecorded condition is a signal to add it to `conditions`, not to describe it unrecorded. The complement also applies: a recorded state that no prose connects to any element either gets its consequences explained or does not belong in frontmatter.

Describe `contents` in prose only where frontmatter does not already model it. Do not translate a `map` tree into prose — that is restatement. Use `contents` for an item's own makeup when frontmatter intentionally leaves it out. If `notes` keeps absorbing the same kind of meaning, the vocabulary is missing a field for it; surface that as a review signal rather than overloading `notes`.

The aspects are calibrated for map material; owner sections refine them for their own elements, and the refinement wins. Action prose has its own aspect set — actor authority, trigger mode, inputs, state effects, confirmation, recovery, feedback (see `actions`). Mechanics prose explains domain meaning and preservation duties (see `mechanics`); condition prose explains what each value changes and what moves it (see `conditions`); entity prose explains meaning, views, and relations (see `entities`). Two aspects mislead outside map material: an entity's `contents` is meaning-level member shape and relations, never fields or schemas; a composition or navigation entry's `contents` is already modeled by its frontmatter shape and needs no prose translation. Where an aspect cannot apply, its absence needs no prose and no placeholder.

Every `PRODUCT.md` should make these basics clear in frontmatter, body, or both:

- product identity or working name
- what the product is and who or what it serves
- primary language and primary surface when they matter
- what good use or a good outcome means
- current scope and important boundaries
- expression or copy direction when product language matters

Portable or standalone ProductMD files may include a short `## About This File` section immediately after the H1:

```md
## About This File

Format: ProductMD v0.1.11
Purpose: This file records product input for this project: durable meaning, selected structure, assumptions, boundaries, and references that should guide future work.
Reading: Frontmatter holds compact product facts; body prose interprets them and never restates them. Backticked product-address references in prose resolve to frontmatter addresses; syntax literals may also use code style.
Spec: https://github.com/codynoskov/Meaningfall/blob/main/products/product-md/docs/spec.md
```

Use this section when a `PRODUCT.md` file may be shared outside its repository or read without nearby ProductMD documentation. Keep it brief: state the format, the purpose of this file, the reading key, and the specification link. Do not use it to restate the full specification, redefine top-level fields, or add project-specific schema.

`## Overview` is enough for a simple product. Larger, sensitive, multi-role, transactional, operational, map-heavy, composition-heavy, or mechanics-heavy products may use deeper sections such as `## Profile`, `## Entities`, `## Conditions`, `## Actions`, `## Map`, `## Compositions`, `## Navigations`, or `## Mechanics`.

Prefer `##` headings for major semantic owners. Except for `## Overview` and meta context such as `## About This File`, a `##` body section should usually correspond to a frontmatter owner when that owner has useful compact facts. Use `###` headings for optional explanation slots inside a major owner, such as `### References`, `### Feedback And Recovery`, `### Sensitive Review`, `### Boundaries`, or `### Non-Goals`.

Product-specific body sections are allowed when they carry durable interpretation that is clearer as prose than as compact facts. Prefer putting them under the nearest owner as `###` sections. A custom `##` body section is acceptable for cross-owner interpretation, but it does not create a new ProductMD owner and should not become a catch-all for material that belongs in `profile`, `entities`, `conditions`, `actions`, `map`, `compositions`, `navigations`, or `mechanics`.

Free-form user notes may be kept in the body while they are being reviewed. Use a clear prose heading such as `## Review Notes`, `## Appendix`, or an owner-local `### Review Notes` when the material is not yet normalized. A finished ProductMD file should not leave durable product facts only in a parking-lot section; normalize them into the cascade or keep them as explicit body interpretation.

Do not create frontmatter only to mirror a heading. Create compact frontmatter when the product meaning can be represented as reusable facts, lists, semantic axes, or named domains. Keep overview framing, rationale, interpretation, and narrative explanation in the Markdown body.

### Open Mappings

Field-owned mappings are open. Product-specific names, map branch names, space names, item keys, local prop names, state values, action names, mechanics domain names, and source names may use the style that fits the product, as long as their meaning is clear or explained in the body.

Top-level keys are not open. Use only the v0.1 top-level names listed in the cascade.

Prefer short lowercase keys for recurring ideas such as `name`, `kind`, `audience`, `contacts`, `entity`, and `references`. Use `snake_case` when a multiword key is needed for clarity. Treat recurring keys as conventions, not a schema.

Do not rename a clear product-specific key only to match a common example. If a local name is more accurate, keep it and explain non-obvious meaning in the body.

### Mapping And Lists

Use mappings for named, addressable product structure: map branches, spaces, and items. Use lists only when order is part of the product meaning and repeated entries may be valid, such as flows, ordered steps, ordered policies, ordered fallback attempts, or ranked options.

The main product map therefore uses named mappings:

```yaml
map:
  product:
    contains:
      home: {}
      docs: {}
```

Do not use lists for ordinary child items:

```yaml
map:
  product:
    contains:
      - home
      - docs
```

## Frontmatter Fields

### `profile`

Optional. When frontmatter is present and product identity is known, `profile.identity.name` is strongly recommended.

`profile` contains compact public identity, legal context, and input references.

```yaml
profile:
  identity:
    name: Acme
    kind: research workspace
    audience: small teams
  legal:
    entity:
      legal_name: TBD
      jurisdiction: Denmark
  references:
    wcag_2_2:
      source: https://www.w3.org/TR/WCAG22/
      kind: accessibility
    product_brief:
      source: /provided-files/product-brief.md
      kind: supplied-document
```

`profile.identity` contains exact public identity facts: name, kind, audience, supplied tagline, public category, provider, place, dates, contacts, social channels, and other public addresses such as a source repository, community channel, status page, or app-store listing. Group public addresses under a key such as `links` or `social`.

These public addresses are identity facts, not product map items. A repository, social account, or community link belongs in `profile.identity`, not in `map`; `map` records the product's own structural items and non-product branches such as system, notifications, or integrations. The product's own home or primary entry point is recorded in `map.product` with `home: true` or normalized `props.home: true`, not as a `homepage` field in `profile`. A repository or external source belongs in `profile.references` only when it is a supplied input the product is generated from.

`profile.legal` contains exact legal, formal, regulatory, rights, or policy facts needed to operate, describe, or generate the product responsibly. It should contain simple facts, not legal advice, compliance instructions, or source lists.

`profile.references` contains supplied or external input sources that should guide future work.

References may include privacy policies, GDPR or other legal/regulatory sources, accessibility guidance, ecommerce UX rules, platform policies, marketplace rules, app-store rules, organization policies, local regulatory sources, AI review policies, brand notes, source documents, and user-provided examples or inspiration.

A reference influences generation as input. A generated product page, future policy surface, route, implementation file, or planned output is not a reference.

A privacy policy belongs in references only when it already exists as a supplied or external source; a future privacy item belongs in `map`, body guidance, handoff notes, or generated output.

Reference values may be simple URLs, supplied file paths, or `TBD`. Use an expanded object with `source` and optional `kind` when the reference category is useful for readers or tools.

Examples: [`fieldnote`](examples/fieldnote/PRODUCT.md), [`carebridge`](examples/carebridge/PRODUCT.md).

### `entities`

Optional.

`entities` records named product meanings that need semantic facts beyond product-map containment. It is not a complete data schema and it is not a duplicate of the map.

```yaml
entities:
  case: {}
  reply: {}
  customer: {}
```

`entities` is a direct mapping from entity name to an empty object or compact entity facts. Do not add a second-level wrapper such as `items`, `objects`, `canvases`, or `embeds`.

```yaml
entities:
  case: {}
  article:
    collection: true
    views:
      - in-list
    relations:
      assigned-to: agent
```

Do not add `embeds`, `media`, `figures`, `sections`, `flows`, `forms`, `components`, `tables`, or `pages` as peer entity groups or fixed entity types. Those words may appear as product-specific entity names when the product meaning itself requires them, but ProductMD does not define them as schema categories.

`entities` records what named product meanings are. `map` records durable product items and containment. A map item is broader than an entity: it may be a destination, system crossing, notification surface, integration touchpoint, flow support item, or structural item that needs no separate semantic facts. An entity is narrower: it earns a frontmatter entry only when the named meaning needs facts that `map`, `actions`, `conditions`, or ordinary body prose would otherwise lose.

The same authored name may appear in both owners when one product meaning needs both structural presence and entity-level facts. Their meaning is read as a union across owners: structural presence in `map`, entity facts in `entities`. When one product meaning needs both, it must use the identical name in both owners; a name mismatch breaks the connection instead of creating an implicit alias.

An entity may use these optional fields:

- `collection` — `true` when the entity represents a series of same-shaped product things.
- `views` — semantic representation variants of the same entity meaning.
- `relations` — durable semantic associations with other entities.

ProductMD v0.1 does not define a fixed `type` field for entities. Do not write `type: default`, `type: collection`, or `type: canvas`. If repeated use later proves a product-specific type system is needed, it should be added deliberately; for now, `collection`, `views`, `relations`, and body explanation cover the accepted semantic pressure without creating a component taxonomy.

```yaml
entities:
  pricing-plan: {}

  article:
    collection: true
    views:
      - in-card
      - in-section
    relations:
      tagged-with: topic
      written-by: author

  workload-board:
    relations:
      - incident
      - customer
      - review
```

The collection index, archive, or browsing surface belongs in `map`; the collection fact itself belongs in `entities.<name>.collection`. This means a product with durable collection surfaces will usually have corresponding `entities` entries even when it otherwise has few entities.

`collection: true` belongs in `entities`, not in `map`. Do not add representative `sample-*` map items only to show that a collection has members.

`views` lists semantic representation variants of the same entity meaning. A view is not a component, layout, route, content outline, or usage index. Entity `views` and map `composition` are independent axes: a view says how one entity meaning is represented; a composition role says which semantic regions exist at a map node.

Use this preferred starter set when it fits:

- `in-card` — compact bounded preview meaning.
- `in-section` — embedded thematic section meaning.
- `in-list` — repeated scanning or queue meaning.
- `in-summary` — recap or status meaning.

This is not a closed vocabulary. Keep the set of view names as small as possible. Reuse these names when they fit the entity-meaning variant. Do not invent near-synonyms such as `card`, `as-card`, `preview-card`, and `tile` for the same meaning. Add a new view name only when it expresses a genuinely different product meaning that the starter set would blur.

Omitting `views` means no special view variants are recorded in frontmatter. It does not mean the entity has no visual or product representation. If an entity has no representation at all, or only appears as part of another entity and never as a complete map item, omit `views` unless there is still a meaningful variant to name and explain the boundary in the body.

For collection entities, views always describe one collection member's semantic representations:

```yaml
entities:
  invoice:
    collection: true
    views:
      - in-list
      - in-summary
```

This says that `invoice` is one collection entity with two recorded semantic view variants for one invoice. It does not create multiple entities and it does not require a full-page/default view token. The collection index or browsing surface belongs in `map`; aggregate or digest meaning for the collection as a whole belongs in body prose or a composition role on the index map item, not in `views`.

`views` and short-form `relations` use YAML lists for compact unordered sets; list order does not imply priority or workflow.

`relations` records durable semantic associations between entities. Use it for cross-links, ownership-like associations, many-to-many associations, and connections whose shape is more complex than containment:

```yaml
entities:
  product:
    collection: true
    relations:
      made-by: maker
      sold-in: shop
      compatible-with:
        - accessory
        - service
```

Do not nest entities to show that they are connected. `map.contains` records structural containment; `entities.<name>.relations` records semantic association. Prefer mapping form (`verb: target`) for directed or asymmetric relations because it preserves relation meaning. Use a bare list of target names only for symmetric or self-evident associations. Do not require inverse relations, and avoid database-shaped terms such as `one-to-many`, `join-table`, or `foreign-key` unless product behavior itself depends on that distinction.

Entity keys should be unique across the product unless the body explicitly disambiguates an unusual collision.

Do not duplicate a map item in `entities` if the map node already records the useful structural fact, it has no `collection`, `views`, `relations`, cross-owner references, or entity-level meaning, and it would only repeat the map name.

If a map item needs `collection`, `views`, or `relations`, write those facts in `entities`, not in `map`:

```yaml
map:
  product:
    contains:
      articles: {}

entities:
  articles:
    collection: true
    views:
      - in-card
      - in-section
    relations:
      - topics
      - authors
```

`entities` names product meanings, not their states, operations, map containment, or governing logic. The states a thing moves through belong in `conditions`; operations on it belong in `actions`; the place it is reached belongs in `map`; the logic that governs it belongs in `mechanics`. A `reply` is an entity; `reply: draft, approved, sent` is a condition; `send-reply` is an action.

List an entity when one of these is true:

- it needs `collection`, `views`, or `relations`
- it is referenced by `conditions`, `actions`, or `mechanics`
- it has product meaning that no single statement about it already carries
- it needs body explanation to prevent misinterpretation
- it exists as product meaning without a durable map item

A noun fully carried by a single statement does not earn an entity. A thin documentation, marketing, or content product may therefore have few entities or none even when it has many map items.

Because later owners can reveal earlier missing meaning, authors and tools should run an entity promotion pass after drafting `map` and `mechanics`: if a map item turns out to need semantic facts, add it to `entities`; if an entity only repeats a map item and has no separate semantic pressure, remove it.

A person-type may appear in two owners at once: as a domain object the product manages (a `customer` entity) and as the current user's behavior-changing role (`account: anonymous, customer, staff` in `conditions`). List it in `entities` when the product stores or is about that object; record the role in `conditions`.

Fields, schemas, lifecycle graphs, provider APIs, and concrete component forms do not belong in `entities` frontmatter. Explain non-obvious entity meaning, shared view vocabulary, relation meaning, rare no-representation entities, and do-not-infer guidance in the body.

When an entity changes strongly under recorded conditions, escalate deliberately. Lifecycle variance stays one entity, described per state value in its body section, baseline first: a `draft` invoice is the accountant's working object, a `sent` one is a frozen legal document, a `paid` one is an audit record. Durable actor-facing variants crystallize as named `views`, with body prose connecting conditions to views; there is no `when` field. And when supposed variants stop sharing operations, lifecycle, and relations, they are two entities joined by a relation, not one entity with variants — the test is whether the variants share identity and history continuously.

Examples: [`case-brief`](examples/case-brief/PRODUCT.md), [`field-market`](examples/field-market/PRODUCT.md).

### `conditions`

Optional.

`conditions` records behavior-changing context and product states.

```yaml
conditions:
  context:
    language:
      - en
    platform:
      - web
  states:
    account:
      - anonymous
      - authenticated
    access:
      - public
      - gated
      - forbidden
    booking:
      search:
        - idle
        - searching
        - no-results
        - results
      reservation:
        - none
        - held
        - confirmed
        - cancelled
```

Use `conditions` for facts that affect behavior, availability, routing, content selection, defaults, obligations, data handling, available actions, generated output, or review pressure.

`conditions.context` names broad product context axes such as language, platform, market, audience mode, deployment surface, or plan family.

`conditions.states` names behavior-changing product states. State groups may be flat lists or simple nested axes. For flat state lists, the first item is the ordinary resting or baseline state when one exists. State lists are not transition graphs.

State groups may mix two kinds of axes: session or user axes that vary per user (an `account` role), and instance-configuration axes that gate behavior for everyone until an operator changes them (a delivery channel, a connected provider, an initialized instance). Both are valid `conditions.states`. Name them so the kind is clear, and explain in the body which action families an instance axis gates; application products repeatedly need both kinds.

Do not turn every product value into a condition. Loading, empty, generic error, hover, pressed, selected, or not-found states are realization coverage, not ProductMD conditions, unless the product itself treats them as meaningful behavior states.

A condition must change what the product does with the same content — available actions, access, routing, content selection, defaults, obligations, or review pressure. The mere existence of different content is not a condition: separate versions, editions, or pages are `map` items and content, not states. A single-value context axis (one language, one platform) is a scope fact rather than a behavior-changing state. Release or version status is volatile and stays out of `PRODUCT.md`; a version-like track such as `current`/`archived` is a condition only when it uses stable category names and carries a behavioral rule, such as keeping archived material reachable but not presenting it as current.

Transition logic, precedence rules, impossible combinations, and state interactions belong in the body unless a later ProductMD version accepts more structure.

Examples: [`signal-lantern`](examples/signal-lantern/PRODUCT.md), [`harbor-hotel`](examples/harbor-hotel/PRODUCT.md), [`carebridge`](examples/carebridge/PRODUCT.md).

### `actions`

Optional.

`actions` records durable product operations, grouped by product area when useful.

```yaml
actions:
  account:
    - signin
    - signup
    - signout
  billing:
    - checkout
    - cancel-plan
```

Actions name operations that matter to the product model. They may be visible user actions, staff/admin actions, automatic actions, scheduled actions, state-triggered actions, or external-service-triggered actions.

ProductMD frontmatter should list action names only. It should not define form schemas, input fields, API endpoints, validation details, state-transition graphs, queues, retry policy, component events, or implementation recipes.

If an action requires a form, job, page, integration handler, or generated product entity, that downstream entity may reference the ProductMD action name. ProductMD should not reference concrete generated file paths.

Actions are related to `conditions` and `map`, but they are not the same thing. Conditions name behavior-changing states. Map names durable product, system, notification, integration, and other product-map items. Actions name operations that may change states, require items, run from items, or happen without an item.

An action must be an operation the product performs or that produces an effect within it — something is created, sent, changed, approved, or moved to a new state. A link that only takes a user to another item is navigation or map structure, not an action. Instructions describing what a user does in their own environment, such as an install command, are content, not actions. An operation that happens entirely in an external system is that system's operation, not this product's, though an external service may still trigger an action when its effect lands in the product. A thin documentation, marketing, or content product may have few actions or none.

Use the body to explain non-obvious action meaning, actor authority, trigger mode, inputs, state effects, confirmation, recovery, feedback, audit, human review, and external dependencies.

Inputs are part of an action's meaning when the product asks something of a person. Describe them at meaning level: what is asked, why the product needs it, what is required versus optional, and what is sensitive. A way to reach the guest is product meaning; an email field is realization. Do not list input fields, formats, controls, or validation rules. When many inputs are asked, group them by meaning and name each group by what it means, never by step or screen: groups are durable, and realization decides whether they render as one form, a stepper, or phases of a conversation. State an ordering rule only when the order is itself product meaning, such as asking for sensitive input only after its purpose is explained. When an element asks for many inputs, its feedback coverage includes validation: what the product checks and why, and what the actor learns and can do when a check fails. Keep validation at meaning level — a stay cannot end before it starts is product meaning; format and field mechanics are realization. Outputs need no separate vocabulary: name the entity the action creates or changes and the state it moves, using recorded `entities` and `conditions` addresses. An output's weight decides its home. Ephemeral results — a confirmation, a recalculated value — are the action's feedback, one sentence of its prose. An output that outlives the action's moment or can be acted on is an entity: its views, states, operations, and explanation live in its own sections, and the action only references it. An output surface that presents derived results is a map item. A long output description inside an action is a sign that an entity or map item is missing.

A trigger is the initiation fact of an action, not a separate owner. When prose names a trigger, prefer recorded vocabulary: a state-triggered action fires on a transition into a state recorded in `conditions` — if the triggering state is missing there, record it rather than describing an unrecorded event. A schedule is stated in prose. Recurring trigger policy that connects several actions — batching, quiet hours, deduplication — is a `mechanics` domain, not per-action prose.

Examples: [`field-market`](examples/field-market/PRODUCT.md), [`ops-console`](examples/ops-console/PRODUCT.md), [`case-brief`](examples/case-brief/PRODUCT.md), [`carebridge`](examples/carebridge/PRODUCT.md).

### `map`

Optional.

`map` records the durable product map: product items, system items, notification surfaces, integration touchpoints, flows, and other structural branches that agents should preserve when generating or editing product work. It is not limited to websites or pages.

```yaml
map:
  product:
    contains:
      props:
        composition:
          shell: {}
          complement: {}
      home:
        home: true
      research:
        props:
          composition:
            uses: reading
        contains:
          previews: {}
          articles: {}
  system:
    contains:
      signin: {}
      checkout: {}
```

`map` is a mapping of top-level branches. The common branch is `product`; other branches such as `system`, `notifications`, and `integrations` use the same rules. Add another top-level branch only when it names a durable structural class that should sit beside the product branch rather than inside it.

The main structure uses mappings, not lists. A mapping means named, addressable elements. A list means ordered or repeated material where sequence is part of the meaning.

#### Branches, Spaces, Items, Props

Top-level branch names under `map` are structural branches. Branches may contain:

- `props` — exact properties of the branch.
- `spaces` — optional grouped spaces for large logical product areas.
- `contains` — child items directly inside the branch.

`spaces` is an optional grouping container. Use it only when a branch or item contains two or more peer spaces. Do not create a single space in advance only because the product may grow later.

`contains` is the standard child-item container. It may contain one item or many items. Use `contains` for ordinary child structure.

An item is the main named element of the product tree. An item may contain:

- `props`
- `contains`
- `spaces`

`props` is the canonical normalized container for properties of a branch, space, item, or item group. Do not introduce `meta` in ProductMD v0.1.

`props` is open for local product-specific properties unless a prop name is reserved by ProductMD. ProductMD v0.1 reserves:

- `name` — a rare escape hatch when the YAML key cannot be the object's real name, for example when the object is literally named `props`, `items`, or `spaces`, or when a supplied name is not suitable as a YAML key. In ordinary structure, the YAML key is the object's name. The direct `name` shorthand also normalizes to `props.name`.
- `home` — marks the selected primary useful entry item.
- `reset` — resets selected prop groups at the current scope.
- `composition` — a prop group, not a local prop.

Local props belong only to the branch, space, item, or group where they are written. They do not pass to child items.

For authoring compactness, ProductMD-reserved props may also be written directly on a branch, space, or item when the meaning is unambiguous. Consumers normalize direct reserved props into `props`. Product-specific custom props must stay inside `props`.

These two forms are equivalent:

```yaml
home:
  home: true
```

```yaml
home:
  props:
    home: true
```

The shorthand applies only to ProductMD-reserved props. Direct keys on a branch, space, or item must be structural containers (`props`, `contains`, `spaces`) or ProductMD-reserved props that normalize into `props`. Do not write custom local props directly on a branch, space, or item. Group-level properties under `contains` or `spaces` continue to use the reserved `props` entry so they cannot be confused with child names.

Composition written directly on a branch, space, or item declares roles or a reusable profile available at that node's own scope. `contains.props.composition` or `spaces.props.composition` declares roles or a reusable profile shared by that child group. Use the group form when a set of siblings shares the same composition and repeating it on every child would add noise.

#### Item Groups

`contains` may carry group-level properties using a reserved `props` entry:

```yaml
map:
  product:
    contains:
      props:
        composition:
          shell: {}
      home: {}
      docs: {}
```

This says that the child items in that group share the listed group-level prop groups. The `props` entry is not an item. If the product has an actual child named `props`, give it a different YAML key and put the real name in `props.name`.

`spaces` may use the same pattern when properties apply to the group of spaces.

#### Composition

`composition` is a prop group under `props`. It records semantic composition roles or a reusable composition profile available at that branch, space, item, or item group.

At one scope, `props.composition` is either inline roles:

```yaml
props:
  composition:
    shell: {}
    complement: {}
    overlay: {}
```

or one reusable profile reference:

```yaml
props:
  composition:
    uses: community-assisted-reading
```

Do not mix `uses` with inline `shell`, `complement`, or `overlay` branches in the same `props.composition` value.

Use empty objects for the role branches by default. Do not list page contents, UI regions, components, widgets, layout wrappers, or arbitrary custom parts inside inline `composition` unless a product has explicit pressure to preserve a repeated semantic part that would otherwise be lost. The reserved `nav` key described below is a navigation exposure shape, not an arbitrary custom part.

The three roles mean:

- `shell` — stable orientation or operating context for the current scope.
- `complement` — semantic material that complements content with context, trust, comparison, policy, recovery, related material, or next-step support.
- `overlay` — temporary, interruptive, or cross-cutting semantic material tied to the scope.

Content is the item itself and its body guidance. Do not add a `content` composition role to say that an item has content.

Inline composition is applied by mapping merge. Omitted local role keys keep any broader inline role that applies to the current scope. A narrower value for the same role wins in its local scope. Use `does_not_apply` as the explicit negative override for one inherited inline role:

```yaml
props:
  composition:
    complement: does_not_apply
    overlay: {}
```

`does_not_apply` does not mean hidden, disabled, unavailable, deleted from source, or removed from a broader scope. In the composition cascade it suppresses a single inherited named entry at the level where it appears, such as a composition role or a nav exposure. Separately, inside a navigation's `override`, `<subject>: does_not_apply` excludes that subject from that one projection — a refinement of the projection, with no inheritance involved.

Use `props.reset` to reset a prop group at the current scope before applying local values:

```yaml
props:
  reset:
    composition: true
  composition:
    overlay: {}
```

`props.reset.all: true` resets all ProductMD prop groups at the current scope. In ProductMD v0.1 that means `composition`. `reset` works at the prop-group level only; it does not work inside `composition`.

`uses` references a named top-level `compositions.<name>` profile. It is reference-only:
it does not accept local role overrides, local deltas, `reset`, or `does_not_apply` inside
the same composition value. If a scope needs a profile variant, define another named
profile or use inline composition at that scope.

`uses` participates in the same scope and group placement as inline composition. It is
valid directly on a branch, space, or item and in group-level locations such as
`contains.props.composition.uses` and `spaces.props.composition.uses`.

Composition cascade behaves as follows:

- Inline composition keeps the role-level merge behavior described above.
- A local `uses` value replaces inherited composition at that scope; it does not merge with inherited inline roles or inherited profile roles.
- A local inline composition written under an inherited `uses` profile also replaces that inherited profile for the local scope; it is not a partial override of the profile.
- A child with no local composition inherits the nearest applicable composition, whether inline or profile-backed.
- `props.reset.composition: true` and `props.reset.all: true` reset inherited composition before any local inline composition or local `uses` is applied.

User-authored files may keep simple or group-level composition inline; a thin
`shell: {}` does not require a named profile, and consumers preserve the authored
choice. Generators and published examples prefer catalog form even for thin profiles,
per the authoring model.

#### Navigation Hosting

A composition role may carry one reserved structured key, `nav`, for named navigation exposures. An exposure attaches a navigation defined in top-level `navigations` to the current scope; the navigation itself — what is projected, from where, how deep — is defined in the `navigations` catalog, not inside composition.

Use `nav` only when the product deliberately exposes a shaped view that the map itself and the composition role do not already make clear. The composition role carries meaning:

- `shell.nav` — stable orientation or wayfinding for the scope.
- `complement.nav` — supporting, related, next-step, policy, recovery, trust, or resource links.
- `overlay.nav` — cross-cutting or interruptive navigation available over the current surface.

`nav` is a mapping from exposure name to navigation name:

```yaml
map:
  product:
    composition:
      shell:
        nav:
          primary: site-primary
          directory: site-directory
```

The exposure name (`primary`, `directory`) is the local role of the navigation at this place; the navigation name (`site-primary`, `site-directory`) is the reusable shaped view defined in `navigations`. The same navigation may serve different exposures at different scopes, and a child may re-point an inherited exposure name to a different navigation.

Exposure names describe function, not placement. Prefer names such as `primary`, `directory`, `local`, `related`, `resources`, or `location`. Do not use layout names such as `header`, `footer`, `sidebar`, `top`, `bottom`, `left`, or `right` as navigation exposure identity.

An exposure value may also be an inline projection body using the `navigations` entry shape, in mapping form only. Inside `nav`, a scalar exposure value is always a navigation name (or `does_not_apply`); the scalar depth shorthand accepted under top-level `navigations` does not apply here, so `local: all` references a navigation named `all`, never depth. Inline projections are valid authored syntax, but catalog references are the preferred authored and generated form: they keep the navigation grammar in one place and give body prose a name to explain.

Navigation exposure inheritance follows the surrounding composition cascade. Omitted exposure names inherit. New exposure names add. A same-named exposure reference replaces the inherited reference. Use `does_not_apply` to suppress an inherited exposure:

```yaml
nav:
  directory: does_not_apply
```

`props.reset.composition: true` and `props.reset.all: true` reset inherited navigation exposures because `nav` lives inside `composition`. `reset` works only at the prop-group level; it does not reach into `navigations` catalog entries, which are definitions, not scope state.

In-page heading or anchor navigation is not ProductMD map navigation. Keep it in generated page files or body guidance unless repeated product pressure proves it needs a future accepted shape.

#### Product Branch

The `product` branch records the main product structure. It may have direct `contains` for simple products:

```yaml
map:
  product:
    contains:
      props:
        composition:
          shell: {}
      home:
        home: true
      docs: {}
```

Use `spaces` only when there are two or more large peer spaces:

```yaml
map:
  product:
    spaces:
      public:
        contains:
          home:
            home: true
          shop: {}
      seller:
        contains:
          listings: {}
          orders: {}
```

Do not use `spaces` to create a single wrapper around items. If there is only one candidate space, model its children directly as `contains` until another peer space exists.

#### System And Other Branches

The `system` branch records durable access, recovery, provider-return, error, state-crossing, or operation-support items that should not appear as ordinary product items.

```yaml
map:
  system:
    contains:
      signin: {}
      payment-result: {}
      forbidden: {}
```

Use other branches such as `notifications` or `integrations` when the product has durable structures that are not ordinary product items and not system crossings. These branches use the same `props`, `spaces`, and `contains` rules.

#### Collections And Entities

`map` records structural presence. It does not record whether an item is a collection.

Use `entities.<name>.collection: true` when a map item represents a series of same-shaped items:

```yaml
map:
  product:
    contains:
      articles: {}

entities:
  articles:
    collection: true
```

Do not add representative `sample-*` items only to show that the collection has members. The collection item's purpose, member shape, views, relations, and boundaries belong in `entities` or in the body when they are not self-evident.

#### Body Guidance

`map` is not a route table, CMS model, page-template schema, navigation policy, content outline, component structure, form schema, transition graph, or implementation recipe.

The frontmatter `map` stays a compact skeleton of product structure and composition roles. The Markdown body is the place to describe each non-obvious branch, space, item, or group: purpose, contained meaning, condition-sensitive behavior, exceptions, external links, source-of-truth relationships, and do-not-infer guidance. Keep page or item contents in body prose or downstream source files, not as custom composition inventories.

Examples: [`field-notes-library`](examples/field-notes-library/PRODUCT.md), [`lumen-docs`](examples/lumen-docs/PRODUCT.md), [`field-market`](examples/field-market/PRODUCT.md).

### `compositions`

Optional.

`compositions` is a catalog of named reusable composition profiles. Use it when the same
rich composition applies at several map scopes and inline composition would duplicate the
same structure or push machine-visible meaning into body prose. Generators and published
examples also use it for thin profiles, purely for readability, per the authoring model.

Although `compositions` is defined after `map`, it is referenced from `map` by name
through `props.composition.uses`, like `entities`. Read it as a catalog, not as a stage
that runs after `map`.

Each entry under `compositions.<name>` is shaped like an inline `props.composition` block,
but it contains only role branches:

```yaml
compositions:
  community-assisted-reading:
    shell:
      nav:
        reading: local-section
    complement:
      ai-assistance: {}
      community-questions: {}
      page-feedback: {}
```

Profiles may contain:

- `shell`
- `complement`
- `overlay`
- role-hosted `nav` exposures referencing `navigations` entries

Profiles may not contain `uses`. Profile-to-profile composition is not part of ProductMD
v0.1. A profile referencing a `navigations` entry is a host-to-catalog reference, not
profile-to-profile composition.

Apply a profile from `map` with `props.composition.uses`:

```yaml
map:
  product:
    contains:
      docs:
        contains:
          props:
            composition:
              uses: community-assisted-reading
          guides: {}
          reference: {}
      handbook:
        contains:
          engineering:
            contains:
              props:
                composition:
                  uses: community-assisted-reading
              developing-locally: {}
```

Profile names should describe semantic function, not layout placement. Prefer names such
as `community-assisted-reading`, `checkout-support`, `review-work`, or
`related-resources`. Do not use visual or placement names such as `sidebar`, `header`,
`panel`, `right-rail`, or `card-grid`.

`compositions` is not a component registry, layout catalog, page-template system,
navigation owner, second map, or content inventory. It names reusable semantic
composition, not how that composition is visually realized. The navigations it exposes
are defined in `navigations`.

### `navigations`

Optional.

`navigations` is a catalog of named, shaped projections of the product map. Each entry is one durable navigation — a view of the map that the product deliberately exposes. A navigation is not a route table, a second map, a menu component, a layout region, or a navigation policy.

Like `compositions`, `navigations` is a referenced catalog: composition roles (inline or in profiles) attach entries by name through `nav` exposures. A navigation entry never lists the places where it applies.

```yaml
navigations:
  site-primary:
    from: product
    depth: 1
  site-directory:
    from: product
    depth: all
    override:
      admin: does_not_apply
  local-section:
    from: -1
    depth: 1
  location:
    type: breadcrumbs
```

Omitted `type` means `default`. A default navigation projects the map:

- Omitted `from` means `current`. `current` is the map point where the referencing exposure is resolved, not the point where the navigation is defined.
- `from` may be `current`, a relative integer such as `-1`, or an explicit map path.
- `depth` is a non-negative integer or `all`.
- Structural containers such as `contains`, `spaces`, and `props` are not depth steps.
- A `from` path does not cross top-level map branches. A product navigation does not automatically include `system` items; link to those explicitly when needed.

Because `from` resolves at the referencing scope, reusable navigations should prefer relative or self-anchored values: omitted `from`, `from: current`, or relative values such as `from: -1`. Absolute map paths are valid only when the navigation is intentionally root-specific or branch-specific, such as a product-wide `site-primary`. Treat absolute paths as a reuse smell by default.

Scalar depth shorthand is valid only under top-level `navigations`, where it is unambiguous:

```yaml
navigations:
  local-section: 1
  site-directory: all
```

This normalizes to:

```yaml
navigations:
  local-section:
    depth: 1
  site-directory:
    depth: all
```

This shorthand never applies inside `nav` exposures, where a scalar value is always a navigation name.

Inside a navigation, use `items` only for explicit curated links, including cross-branch map links, profile addresses, or external URLs. Navigation `items` and `links` hold link entries only. Prefer `from` plus `depth` over hand-listing a branch's own children.

```yaml
navigations:
  resources:
    items:
      docs: product.docs
      repository: profile.identity.links.repository
      status: https://status.example.com
```

When a navigation is mainly a list of explicit links, `links` is an exact compact alias for `items`:

```yaml
navigations:
  resources:
    links:
      docs: product.docs
      repository: profile.identity.links.repository
      status: https://status.example.com
```

This normalizes to the `items` form above. Use `links` only for explicit links; use `from` plus `depth` for map projection.

A scalar link item is shorthand for `target`. Use expanded form only when the link needs another accepted property:

```yaml
navigations:
  resources:
    items:
      status:
        target: https://status.example.com
        label: System status
```

Resolve scalar link targets in this order: external URL with a scheme, `profile.*` path, then map path. Map-path link targets are absolute from the map root, such as `product.docs`, not relative to the current scope. The `profile.*` prefix is reserved for profile addresses; do not use `profile` as a top-level map branch name.

`override` refines named subjects inside one navigation. It does not mutate the source map and does not affect other navigations. Scalar override values mean `depth`, and `does_not_apply` means the named branch does not apply in that navigation.

Override keys address the projection's own subjects: an immediate child of the navigation's `from` root by bare name, or a deeper subject by a relative dot path from that root, such as `guides.archive`. A bare name never reaches past the immediate children, so repeated item names elsewhere in the map stay unambiguous.

```yaml
navigations:
  site-directory:
    from: product
    depth: all
    override:
      admin: does_not_apply
      guides: 1
```

`type: breadcrumbs` is a map-derived trail toward the current map point. Omitted `from` means the nearest applicable map root or scope root. `depth` is valid but uncommon; when present, it limits how far the trail may extend from `from` toward current.

```yaml
navigations:
  location:
    type: breadcrumbs
    from: product.docs
```

Navigation names describe function, not placement: `site-primary`, `site-directory`, `local-section`, `related-resources`. Do not use layout names such as `header`, `footer`, or `sidebar` as navigation identity.

A navigation is usually surfaced through a composition role, but a map item may also be a navigation surface itself: a machine-facing index such as an `llms.txt` or sitemap file is a map item whose content is a named navigation. State that relationship in the body ("the content of this item is the `site-directory` navigation"); no other hosting mechanism is defined.

Condition-dependent navigation stays in the body: record the axes in `conditions`, name the navigations here, and explain in prose which conditions select which navigation. ProductMD v0.1 does not define a condition field on navigation entries.

Examples: [`lumen-docs`](examples/lumen-docs/PRODUCT.md).

### `mechanics`

Optional.

`mechanics` records internal product-logic domains that agents should preserve when generating, reviewing, or changing product work.

```yaml
mechanics:
  editor:
    - selection-model
    - tool-modes
    - object-lifecycle
  assistant:
    - intent-routing
    - escalation-policy
```

Mechanics is a compact domain index. It names product-logic areas that must not be lost, such as selection models, tool modes, scoring and ranking, matching, scheduling, pricing, permissions, assignment, escalation, AI routing, review policy, or game rules. A mechanic is durable internal logic that affects several actions, states, or map items and is not captured by any one action or condition.

Mechanics should not encode the full behavior. It is not a decision-table DSL, transition graph, implementation model, realization mechanics, workflow engine, route guard matrix, permission table, prompt chain, queue definition, or replacement for `actions`.

Use the body to explain non-obvious mechanics: what a domain means, why it matters, which conditions or actions affect it, what downstream work must preserve, and which details are intentionally outside ProductMD.

Examples: [`ops-console`](examples/ops-console/PRODUCT.md), [`case-brief`](examples/case-brief/PRODUCT.md).

## Consumer Behavior

Consumers include AI coding agents, interview tools, generators, validators, diff/explain tools, and any other software or workflow that reads or updates `PRODUCT.md`.

Consumers should preserve user-authored source. Unknown fields and unknown body sections may be reported for review, but they should not be deleted or rewritten just because they are not part of v0.1.

Consumers should treat manual edits as meaningful unless they clearly break YAML syntax or conflict with accepted ProductMD rules.

When content appears to belong somewhere else, consumers should warn, ask, or propose a scoped update. They should not silently normalize field names, move content, or invent missing facts.

When accepting a user addition, consumers should classify it before writing it into the final shape. They should split mixed additions, suggest the nearest valid ProductMD owner, check whether the meaning is already covered, and explain any proposed move or merge in ProductMD terms. The user should be able to choose a likely owner or keep the addition as body prose for later review.

Consumers should check sequence pressure. A proposed edit to `map`, `compositions`, `navigations`, or `mechanics` may reveal missing `profile`, `entities`, `conditions`, or `actions` facts. In that case the consumer should propose the earlier-owner update explicitly instead of hiding the new fact in the later owner.

When required or known-needed facts are missing, consumers should ask for the value or preserve an explicit `TBD`. They should not infer legal facts, contact details, routes, states, obligations, or source references from generic product-category assumptions.

Consumers should preserve rare syntax when it is justified by product pressure. Do not simplify `spaces`, non-product `map` branches, group-level `props`, nested state axes, `entities` entries with `collection`, `views`, or `relations`, reusable `compositions`, `props.composition.uses`, named `navigations` and their exposure references, inline navigation projections, reset rules, negative overrides, or mechanics domains only because a smaller example does not use them. If the syntax appears unjustified, report it for review instead of deleting it.

Consumers should update narrowly. A request to revise actions or mechanics should not rewrite profile, conditions, map, or body prose unless the change creates direct pressure on those owners. When a later section reveals a missing earlier fact, propose the earlier owner update explicitly.

Consumers should preserve body guidance as product source. They should not collapse body explanations into frontmatter or delete rationale, assumptions, boundaries, recovery guidance, or review notes because the same topic has a compact YAML value. If body prose duplicates frontmatter without adding interpretation, consumers may propose shortening it, but they should preserve any meaning that frontmatter cannot carry.

## Relationship To Other Files

### Visual Design

A design system or visual styling layer owns visual identity: tokens, colors, typography, spacing, component style, and design rationale.

`PRODUCT.md` may say that paid users see content while unpaid users see an upgrade call to action. It should not say what color the call to action is.

### Realization

A presentation or realization layer owns how product meaning becomes a running interface: component catalogs, widgets, layout mechanics, transient UI state, loading behavior, and format-specific mappings.

`PRODUCT.md` records durable product meaning, selected semantic axes, product-map structure, and semantic composition roles — not the components or widgets that realize them. `props.composition` may say that `shell`, `complement`, or `overlay` is a meaningful role at a scope; it should not say which component, landmark, command surface, or message template realizes that role.

Realization reads `PRODUCT.md` in two modes. As generation input it is the source: views, pages, flows, and other output are derived from its meaning. As a conformance contract it binds every realized render, fixed or generated: a render conforms when map reachability is preserved, when the meanings recorded for a place are present or reachable there, when mechanics invariants hold, and when nothing contradicts recorded boundaries or do-not-infer guidance. A fixed interface satisfies the contract once at design time; an individualized or generated render must satisfy it on every render. Conformance checks derive from the file itself; ProductMD v0.1 defines no separate conformance schema.

### `AGENTS.md`

`AGENTS.md` owns repository operation: commands, conventions, restrictions, and agent instructions.

`PRODUCT.md` should describe the product, not how an agent should edit files.

### Skills And Tools

Skills and tools own reusable procedure: how to generate, revise, validate, review, interview, or check ProductMD files.

`PRODUCT.md` should describe product meaning, not task procedure.

## Non-Goals

ProductMD v0.1 is not:

- a runtime
- a CMS
- a resolver
- an ontology language
- a design token format
- a replacement for code
- a complete route model or page-template system
- a legal compliance format
- a universal workflow engine
- a decision-table language

## Validation Guidance

A basic checker may verify that:

- optional YAML frontmatter parses as YAML when present
- known v0.1 top-level fields follow the order `profile`, `entities`, `conditions`, `actions`, `map`, `compositions`, `navigations`, `mechanics`
- `profile.identity.name` exists when frontmatter is present and product identity is known
- `entities`, when present, is a direct mapping from entity name to an empty object or compact facts; do not require a second-level `items` group
- entity entries are empty objects or compact mappings with the accepted fields `collection`, `views`, and `relations`
- `collection: true` appears only under `entities.<name>`, not in `map`
- entity entries do not use `type`, including `type: default`, `type: collection`, or `type: canvas`
- omitted `views` means no special view variants are recorded in frontmatter; it does not mean no representation
- collection entity `views` describe one member, not the collection index or aggregate digest
- `relations` records semantic associations, not database joins, foreign keys, or nested containment
- directed or asymmetric `relations` prefer mapping form (`verb: target`); bare target lists are for symmetric or self-evident associations
- a product meaning that appears in both `map` and `entities` uses the identical authored name in both owners
- `conditions.context` and `conditions.states` use mappings to compact value lists or simple nested mappings
- `map` is a mapping whose top-level branches may include `product`, `system`, `notifications`, `integrations`, or other durable branch names, except reserved top-level field names such as `profile`
- `map` branches, spaces, items, and item groups use `props` as the canonical property container rather than `meta`
- direct branch, space, or item properties are limited to ProductMD-reserved props that normalize into `props`
- `map` child structure uses mappings under `contains` and `spaces`, not lists
- `spaces` is used only when there are two or more peer spaces
- `contains` may contain one item or many items
- `props` is open for local product-specific properties except for ProductMD-reserved prop names
- `composition` or normalized `props.composition` uses either the accepted inline branches `shell`, `complement`, and `overlay`, or a single `uses` reference
- `props.composition.uses`, when present, names an entry under top-level `compositions`
- `uses` is not mixed with inline `shell`, `complement`, or `overlay` branches in the same `props.composition` value
- ordinary composition branches are empty objects unless explicit product pressure requires a preserved semantic subpart or the reserved `nav` key
- `compositions`, when present, is a mapping from profile name to inline composition roles; profiles do not contain `uses`
- `compositions` entries use functional semantic names rather than layout or placement names
- group-level `contains.props.composition.uses` and `spaces.props.composition.uses` are valid when sibling groups share a reusable profile
- `nav` exposure names use functional names rather than layout names
- `nav` exposure values reference entries under top-level `navigations` by name or carry an inline projection body in mapping form; a scalar exposure value is always a navigation name, never depth shorthand; catalog references are the preferred generated form
- scalar depth shorthand for navigation entries is valid only under top-level `navigations`
- `navigations`, when present, is a mapping from navigation name to one map projection, breadcrumbs trail, or curated link set
- navigation names use functional names rather than layout names
- navigation entries project or curate product navigation; they do not duplicate the map, define UI realization, or list the scopes where they apply
- the primary entry point, when selected, is marked with `home: true` or normalized `props.home: true`
- collection facts use `collection: true` under `entities`, not `collection: true` in `map`; do not add representative `sample-*` map items only to show collection membership
- `props.reset` resets selected prop groups at the current scope
- `does_not_apply` is the explicit negative override for one inherited named entry inside a prop group
- `actions` lists action names rather than form schemas, endpoints, or implementation recipes
- `mechanics` maps product-logic domains to compact domain-name lists rather than workflow graphs, implementation models, or policy tables
- long-form rationale, edge cases, assumptions, and product rules stay in the Markdown body

Review tooling may also report semantic placement issues:

- a user addition that mixes several owner roles and should be split
- an addition whose meaning is already covered elsewhere
- a body paragraph that restates frontmatter without adding interpretation
- a custom body section that has become a parking lot for facts that belong in the cascade
- a later-owner addition that needs an earlier `profile`, `entities`, `conditions`, or `actions` fact
- an entity-like noun hidden only in `map`, when it needs `collection`, `views`, `relations`, conditions, actions, mechanics, or body explanation
- a condition described in body prose but missing from `conditions`
- an operation described in body prose but missing from `actions`
- a navigation or composition concept described repeatedly in body prose that should become a named catalog entry
- implementation or realization detail that should move outside ProductMD

Strict validation and additional tooling are deferred until repeated use shows a clear need. ProductMD v0.1 should remain useful as a readable file convention without requiring a CLI, package, build step, or validator.

## Extension Policy

Product-specific names are open inside field-owned mappings such as entity names, condition groups, map branch names, spaces, items, local props, action groups, and mechanics domains.

Body headings are open as prose organization, but they are not schema owners. Prefer owner-aligned `##` headings and owner-local `###` headings; preserve unusual user-authored headings when they carry meaning, and review them when they duplicate or bypass the cascade.

Top-level ProductMD keys should remain small and deliberate. Adding a new top-level key is a format design decision, not a one-off example choice. A new top-level key is justified only when repeated real ProductMD files need a durable owner that cannot be represented as profile facts, entities, conditions, actions, map structure, compositions, navigations, mechanics, or body guidance.

Do not use unknown top-level keys, custom composition roles, layout-based navigation names, or direct custom map props as extension mechanisms. Use open field-owned names, functional navigation names, `props` for local product-specific properties, body prose for interpretation, and review notes for unresolved material.

## Examples

Complete examples live in [`examples/`](examples/).
