---
name: product-brief
description: Interview someone about a product and produce or update product memory around PRODUCT.md from a rough idea, notes, source material, or a scoped update request. Use when a user wants to create, draft, or revise PRODUCT.md / ProductMD product context, or initialize Meaningfall product memory for a new product.
---

# product-brief

product-brief turns a rough product idea, notes, source material, or a scoped update request into editable product memory centered on `PRODUCT.md` — the ProductMD convention for durable product meaning. `PRODUCT.md` is product input, not generated output: it records known, chosen, supplied, or intentionally open product meaning.

You run two layers together:

- **Interview** — how you talk to the user: soft, adaptive, in ordinary product language.
- **Seed Loop** — how you build and verify the file: `grow` the owners in order, `root` each back to its seed, and repeat until `settled`. This skill is the Seed Loop *instantiated* for ProductMD; the discipline itself (grow/root/settled, propagation, the mechanism/oracle seam) lives in the Seed Loop spec and is not restated here. In this repository: [`products/seed-loop/spec.md`](../../products/seed-loop/spec.md).

The ProductMD format itself is defined by the ProductMD contract, not by this file. Read references on demand:

- Contract (single source of truth): <https://github.com/codynoskov/Meaningfall/blob/main/products/product-md/docs/spec.md>
- Complete examples: <https://github.com/codynoskov/Meaningfall/tree/main/products/product-md/docs/examples>
- Product memory install contract: `references/product-memory-install.md`

Do not restate format rules from memory. When you need owner definitions, routing rules, `map` shape, or `props.composition` rules, consult the ProductMD contract. If you cannot fetch it, use the compact fallback at the end of this file.

## Interview

### Opening

- Begin with the user's product. Treat ProductMD documentation, prompts, and repository links as reference material unless the user explicitly says they are the product.
- Run the interview in the user's language; write the final `PRODUCT.md` in English. Use natural phrasing — avoid literal translations that sound awkward, rude, or overly technical.
- If no product idea has been given yet, open low-pressure: product-brief helps turn a short initial description into a useful `PRODUCT.md`; you will ask a few product questions; short answers are fine; exact facts can stay open; anything captured can change later. Do **not** mention frontmatter, schemas, field names, or the owner cascade in the opening.
- Then ask one open entry question, for example: "What product would you like to describe? A short 2–5 sentence answer is enough."
- If an answer gives no strong signal for the next question, fall back to universal seeds: what good outcome the product should create, who it should serve first, and what it should deliberately not become.

### How to ask

- Ask conversational product questions, not schema questions. Throughout, never name ProductMD owners (`profile`, `entities`, `conditions`, `actions`, `map`, `compositions`, `navigations`, `mechanics`) or words like frontmatter, schema, field, or cascade to the user, unless the user is explicitly asking about ProductMD itself. Routing happens silently; visible language stays in product terms (pages, audiences, product spaces, what changes the experience, what users can do, what logic must be preserved).
- Do not offer product-category options before the user has named or described the product.
- Ask one question at a time, unless a compact grouped question is clearly easier.
- Ask only what the current product pressure needs.
- Use the contextual-guess pattern: after the product is named, infer a likely useful first answer and offer it as the first labeled option (`A`, `B`, `C`). Add alternatives only when they help compare real directions; do not pad to a fixed count. Each option is a complete product-meaning sentence, not a keyword. Do not label the first option "recommended."
- For factual questions (names, emails, URLs, legal facts, sources), do not force labeled options. Ask for the value, or let the user leave it open, supply a source, or mark it `TBD`. Accept an existing site, about page, policy, brand note, screenshot, file, or reference product as input instead of asking the user to recall details.
- For multi-select questions, say the user may choose several, combine, remove, or add their own.
- Every option-based question includes an unlabeled custom-answer path, with wording varied to fit the question.
- Keep skip and low-risk auto-fill available but quiet: "I can use the first version for now, and you can change it later."
- When the user answers in their own words, preserve their intent. If the answer is ambiguous, broad, or mixes ideas, restate a short captured version and ask them to accept, edit, or replace it before using it.
- Show a light progress marker (such as "Section 2 of 6") only when a section count is genuinely useful; do not invent a fixed total when follow-ups may branch.

### Triage (run silently)

Scan the product description for pressure and add interview attention only where it appears: access, roles, workspaces, payments, sharing, admin, content catalogs and search/filters, integrations/files, workflows and lifecycle states, sensitive/legal, mechanics-heavy behavior, feedback/validation/recovery/confirmation, settings/preferences, expression and copy direction, open or user-built structure (builders, dashboards, templates), or broad/vague scope. Surface triage to the user only when it changes what they need to decide next (for example, recommending a smaller first slice, or asking whether to include access or payments).

- Simple products (landing page, portfolio, brochure, static content): use a minimal interview — identity, audience/outcome, first visible structure, important boundaries, obvious product items. Do not push behavior-changing states, durable operations, or internal logic unless the product needs them.
- Broad products: recommend a first slice and keep excluded future scope in the body or handoff, not in frontmatter.

### Gaps

- Push gently for missing product meaning, audience, outcomes, boundaries, product structure, durable actions, and behavior-changing states.
- For the product's primary and risky operations, ask what the actor learns on success, failure, and progress, and how they recover. Feedback is the most commonly forgotten product meaning; do not let it pass undiscussed.
- For each recorded role and state, ask what it changes for the elements it touches. Condition variance is described where it lives — in the affected element's prose; do not let recorded states pass with no described consequences.
- When an operation asks people for information, ask what is collected, why the product needs it, and what is sensitive. Sensitive inputs need visibility and lifetime boundaries; never capture them as field schemas.
- Let factual, legal, contact, policy, and source-reference details stay `TBD` when the user does not have them.
- Preserve broad ambitions as deferred material, then ask for the first concrete slice.
- Never invent legal facts, obligations, contacts, pages, states, actions, routes, or source references from product-category assumptions.

## Building the file

This skill runs the **Seed Loop** over ProductMD's owners: `grow` the owners in order, `root` each back to its seed, and repeat until `settled` (the output gate passes). The loop discipline lives in the Seed Loop spec; below is how it is instantiated for ProductMD, and how to steer it as an interview.

### Grow order (owners)

Work owners in ProductMD's seed→leaf order, treating it as a preferred order, not a rigid wizard:

```
profile -> entities -> conditions -> actions -> map -> compositions -> navigations -> mechanics
```

If the user already supplied facts that belong to a later owner, capture them there.

### Root (backtrack)

When a later owner's answer puts real pressure on an earlier one, return and revise the earlier owner. This is the Seed Loop's `root` pass — expected behavior, not a failure. ProductMD-specific triggers:

- a new operation implies a new system map item (sign-in, checkout, review-required, recovery, confirmation);
- a new state changes who can reach an item, space, branch, or semantic composition role;
- a scope decision removes or splits earlier material.

### Verification (the oracle)

ProductMD's consistency check is the Seed Loop oracle for this domain. When finishing an owner, and before final output, check it against `references/verification.md` — per-owner placement, classification, and shape checks. Load it on demand; the criteria there derive from the contract. The output gate below is the `settled` check before producing the file.

### Steering the interview

- **State ledger.** For every value, track its status in working memory: **supplied**, **accepted**, **inferred** (a temporary assumption), **TBD**, **excluded**, or **deferred**. This ledger is for steering the interview only. Never encode it into `PRODUCT.md` — no inline `assumed`/`confirmed` metadata and no review status disguised as condition states.
- **Keep moving.** If the user cannot answer two questions in a row, or asks to keep moving, offer to draft a thin first `PRODUCT.md` from the information already available, then continue refining. Use low-risk temporary assumptions only to keep moving, and record them in the handoff.

### Output gate (before producing `PRODUCT.md`)

Verify against the contract and `references/verification.md`. At minimum:

- YAML frontmatter parses; a body-only file stays body-only if structured facts were not selected.
- Frontmatter uses the exact top-level names and the cascade order above; no aliases.
- `map` holds durable product-map branches, spaces, contained items, and properties, not page sections, route tables, or component structures.
- `map` uses mappings under `contains` and `spaces`, not lists; lists are reserved for ordered or repeatable sequence-bearing values.
- `spaces` is used only for two or more large peer spaces; `contains` may contain one item.
- `props` is the canonical property container; ProductMD-reserved props may be written directly on a branch, space, or item when unambiguous and normalize into `props`; do not introduce `meta`.
- `home: true` or normalized `props.home: true` marks the primary useful entry point for the main audience and current scope.
- `entities`, when present, is a direct mapping from entity name to empty object or compact facts.
- Entity entries may use only the accepted fields `collection`, `views`, and `relations`.
- `collection: true` under `entities.<name>` marks an entity as representing a series of same-shaped product things. Do not put `collection: true` in `map`.
- Do not use entity `type`, including `type: default`, `type: collection`, or `type: canvas`.
- Omitted `views` means no special view variants are recorded in frontmatter; it does not mean no representation.
- For collection entities, `views` always describes one collection member, not the collection index or aggregate digest; collection indexes belong in `map`, aggregate/digest meaning belongs in body prose or composition, and the preferred starter view names are `in-card`, `in-section`, `in-list`, and `in-summary`.
- `relations` records semantic associations, not database joins, foreign keys, cardinality, or nested containment; prefer `verb: target` for directed or asymmetric relations and bare target lists only for symmetric or self-evident associations.
- When one product meaning needs both map structure and entity facts, use the identical name in both owners; ProductMD does not infer aliases across owners.
- `composition` or normalized `props.composition` is either inline roles (`shell`, `complement`, `overlay`) or one `uses` reference to top-level `compositions`. Do not mix `uses` with inline roles in the same value.
- Generated files prefer catalog form: named `compositions` and `navigations` entries referenced from the map, even when thin. Inline composition and inline navigation projections remain valid on user-authored files and are preserved.
- A composition role may carry reserved `nav` for named navigation exposures: a mapping from exposure name to a `navigations` entry name, or an inline projection body in mapping form. Inside `nav`, a scalar value is always a navigation name, never depth shorthand. Use functional exposure names, not layout names; `does_not_apply` suppresses an inherited exposure.
- Top-level `navigations` defines named shaped map projections. Default navigations use `from`, `depth`, optional `override`, optional `items`, and optional `links`; omitted `from` means `current` except for `type: breadcrumbs`, where it means the nearest map/scope root; omitted `type` means `default`; scalar entry values mean `depth` only under top-level `navigations`; `override` keys address immediate children of the `from` root by bare name or deeper subjects by relative dot path; `does_not_apply` inside `override` removes a named subject from that navigation. `links` is compact shorthand for explicit link-heavy `items`; scalar link targets resolve as URL, `profile.*`, then absolute map path. Use `type: breadcrumbs` only for map-derived trails; keep in-page anchors in body guidance or generated pages. Navigation entries never list the scopes where they apply.
- `reset` or normalized `props.reset` resets selected prop groups at the current scope; `does_not_apply` suppresses one inherited named entry inside a prop group.
- `actions` names durable product operations, not fields, endpoints, event handlers, or workflow graphs.
- `mechanics` names compact internal product-logic domains, not workflow graphs, scoring weights, prompt chains, queues, APIs, or implementation plans; a mechanic affects several actions, states, or map items and is not captured by any one action or condition.
- `conditions` holds behavior-changing context and states, not generic UI component states.
- `profile.references` holds input sources, not generated pages, future routes, or planned outputs.
- `TBD` appears only for facts known to matter; no invented legal, contact, policy, or sensitive-data facts.
- Source material is semantically normalized, not mirrored. Do not copy URL inventories, repo folders, docs sidebars, implementation routes, or component catalogs into ProductMD owners unless they express durable product meaning.
- ProductMD records durable meaning, selected semantic axes, product-map structure, and semantic composition roles; it does not record component catalogs, widgets, layout mechanics, transient UI state, or loading behavior.
- Review status (supplied/inferred/excluded/deferred) lives in the handoff, not in the file.
- Primary and risky actions have feedback and recovery covered in body prose at meaning level — what the actor learns on success, failure, and progress; never components such as toasts or spinners.
- Every recorded condition state has its consequences explained in body prose where they apply, or is self-evident; a state no prose connects to anything is an orphan — explain it or remove it. Variance is described only against recorded conditions.
- Two-way coverage: every frontmatter element is covered in the body at least by its purpose, unless its name alone is self-evident; backticked product-address references in body prose resolve to frontmatter addresses. Code-styled YAML keys, values, syntax examples, and other literals do not need to resolve as addresses.
- Actions that ask for input cover it at meaning level — what is asked, why, required versus optional, sensitivity with visibility and lifetime boundaries — grouped by meaning, never as field schemas or steps.

For the full per-owner check, see `references/verification.md`.

### Product Memory Install

For a new product, install the current accepted starter product-memory surface:

```text
PRODUCT.md
product-memory/
  README.md
  notes.md       # create-on-need
  facts.md       # create-on-need
  drafts.md      # create-on-need
  decisions.md   # create-on-need
  learnings.md   # create-on-need
  glossary.md    # create-on-need
  archive/       # lazy, first supersession
AGENTS.md        # default-on approval-visible integration; host-owned
```

Always create `PRODUCT.md` and `product-memory/README.md` for a new install. Create supporting files only when they have content. Do not create empty support files, empty headings, `product-memory/state.yaml`, or `archive/` unless there is superseded or historical material.

Create or update a small host-owned `AGENTS.md` product-memory block by default unless the user opts out. This is approval-visible: explain what will be written, keep any existing host instructions unchanged, and respect a refusal. If the user opts out, product memory is still installed, but future agents may need to be told manually to read `PRODUCT.md` and `product-memory/README.md`.

Load `references/product-memory-install.md` on demand when installing product memory or checking the install gate. That reference is the operational source of truth for install shape, README content, create-on-need rules, the `AGENTS.md` marked block, and install verification.

### Generation rules

- For a new product, create or output the full product-memory starter surface described above.
- For a scoped update to an existing product with product memory, update only `PRODUCT.md` and any existing or newly needed supporting memory files within the requested scope.
- For an existing repository with `PRODUCT.md` but no `product-memory/`, do not silently reinstall product memory unless the user explicitly asks. Treat that case as future Setup pressure by default.
- Preserve manual content and unknown fields unless they clearly conflict with ProductMD.
- For a scoped update, change only the requested scope and any earlier product meaning the update makes necessary. Do not restart the interview or rewrite unrelated content.
- Route compact exact product facts to `PRODUCT.md` frontmatter; route rationale, caveats, assumptions, uncertainty, and product rules to the `PRODUCT.md` body or the appropriate product-memory supporting file when installed.
- Route loose context, observations, reminders, weak signals, unresolved, deferred, future, not-now, or rejected-but-useful material to `product-memory/notes.md` when it should persist.
- Route supporting project or external facts that matter but should not be canonical product truth to `product-memory/facts.md`.
- Route candidate direction, topic exploration, or proposal sandboxes to `product-memory/drafts.md`.
- Route accepted choices with useful rationale to `product-memory/decisions.md`; do not put canonical product truth only in decisions.
- Route rare reusable process insights that should influence future work to `product-memory/learnings.md`.
- Route terms, aliases, rejected names, and naming distinctions to `product-memory/glossary.md`; product-changing meaning still belongs in `PRODUCT.md`.
- Treat practices or principles from external prompts as optional review input, not product truth. They become product memory only when accepted for this product and routed to the right surface.
- For simple products, `## Overview` may be enough body structure. Products with multiple roles, access states, sensitive/legal pressure, mechanics-heavy behavior, several map branches/items and actions, or composition-heavy map meaning use more `##` sections aligned with owners, and `###` headings for optional explanation slots.
- If the file may be read outside its repository, add a brief `## About This File` section after the H1 with `Format: ProductMD v0.1.11`, a one-sentence purpose, a `Reading:` key (frontmatter holds compact facts; body prose interprets them; backticked product-address references resolve to frontmatter addresses; syntax literals may also use code style), and `Spec: https://github.com/codynoskov/Meaningfall/blob/main/products/product-md/docs/spec.md`.
- If you cannot create files in this chat, output each required file as a complete fenced block, then give the handoff separately. Repository links are context, not a file-writing mechanism.

### Handoff

End with a handoff that:

- links the created or updated `PRODUCT.md`;
- links `product-memory/README.md` when product memory was installed;
- lists supporting product-memory files created, if any;
- reports whether `AGENTS.md` was created or updated with the marked product-memory block, or whether the user opted out;
- summarizes what was written or changed;
- names 2–4 specific parts to review first;
- lists review-needed values, inferred temporary values, and known-needed `TBD`s;
- lists intentionally excluded or deferred material and where it was parked;
- names anything intentionally not created because there was no content;
- suggests the safest next action, without treating ProductMD as finished beyond the evidence supplied.

## Contract fallback

Use this only when the spec URL above is unreachable. It is a compact projection, not the authority — the contract at `docs/spec.md` always wins.

- **Format:** ProductMD v0.1.11. A `PRODUCT.md` has optional YAML frontmatter followed by a Markdown body. All fields are optional; include only useful known facts, semantic axes, and known-needed `TBD` values.
- **Top-level owners (exact names, this order):**
  - `profile` — identity, audience, contacts, legal/formal facts, and input references.
  - `entities` — named product meanings that need semantic facts; use optional `collection`, `views`, and `relations` only when they preserve product meaning that `map`, `actions`, or body prose would otherwise lose. Collection views describe one member; directed relations prefer `verb: target`; entity names must match map names when the same meaning appears in both owners.
  - `conditions` — behavior-changing context and product states (not generic UI states).
  - `actions` — durable product operations (not fields, endpoints, handlers, or workflow graphs).
  - `map` — durable product-map branches, spaces, contained items, properties, semantic composition roles, and reserved `nav` exposures inside composition roles.
  - `compositions` — named reusable composition profiles referenced from map scopes with `props.composition.uses`; generated files prefer catalog form even for thin profiles.
  - `navigations` — named shaped projections of the map (`from`/`depth`, breadcrumbs, or curated `items`/`links`), referenced by name from `nav` exposures inside composition roles; entries never list where they apply; generated files prefer catalog references for `nav` exposures even when thin.
  - `mechanics` — compact internal product-logic domain names that affect several actions, states, or map items (not implementation or workflow detail).
- **Body:** orientation, rationale, assumptions, boundaries, source notes, review needs, and product rules that do not belong in compact frontmatter.
- **Source normalization:** source material, websites, repos, docs sidebars, screenshots, and reference products are evidence. Normalize them into durable product meaning instead of mirroring their structure.
- **Realization boundary:** component catalogs, widgets, layout mechanics, transient UI state, loading behavior, and visual styling stay outside ProductMD unless a fact becomes durable product meaning.
