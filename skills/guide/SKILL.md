---
name: guide
description: Guide a user through creating, updating, or maintaining Meaningfall product memory around PRODUCT.md / ProductMD from a rough product idea, notes, source material, or a scoped update request. Use when a user wants to create, draft, revise, or maintain PRODUCT.md / ProductMD product context, or initialize Meaningfall product memory for a new product.
---

# Guide

Guide turns a rough product idea, notes, source material, or a scoped update request into editable product memory centered on `PRODUCT.md` — the ProductMD convention for durable product meaning. `PRODUCT.md` is product input, not generated output: it records known, chosen, supplied, or intentionally open product meaning.

You run two layers together:

- **Interview** — how you talk to the user: soft, adaptive, in ordinary product language.
- **Seed Loop** — how you build and verify the file: `grow` the owners in order, `root` each back to its seed, and repeat until `settled`. This skill is the Seed Loop *instantiated* for ProductMD; the discipline itself (grow/root/settled, propagation, the mechanism/oracle seam) lives in the Seed Loop spec and is not restated here. In this repository: [`modules/seed-loop/spec.md`](../../modules/seed-loop/spec.md).

The ProductMD format itself is defined by the ProductMD contract, not by this file. Read references on demand:

- Contract (single source of truth): <https://github.com/codynoskov/Meaningfall/blob/main/formats/product-md/spec.md>
- Complete examples: <https://github.com/codynoskov/Meaningfall/tree/main/formats/product-md/examples>
- Memory governance: <https://github.com/codynoskov/Meaningfall/blob/main/modules/memory/spec.md>
- Verify skill: `../verify/SKILL.md`
- Install skill: `../install/SKILL.md`

Do not restate format rules from memory. When you need owner definitions, routing rules, `map` shape, or `props.composition` rules, consult the ProductMD contract. If you cannot fetch it, use the compact fallback at the end of this file.

## Interview

### Opening

- Begin with the user's product. Treat ProductMD documentation, prompts, and repository links as reference material unless the user explicitly says they are the product.
- Run the interview in the user's language; write the final `PRODUCT.md` in English. Use natural phrasing — avoid literal translations that sound awkward, rude, or overly technical.
- If no product idea has been given yet, open low-pressure: Guide helps turn a short initial description into a useful `PRODUCT.md`; you will ask a few product questions; short answers are fine; exact facts can stay open; anything captured can change later. Do **not** mention frontmatter, schemas, field names, or the owner cascade in the opening.
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

ProductMD's consistency check is the Seed Loop oracle for this domain. When
finishing an owner, and before final output, use the Verify skill with target
`product-md-output`. The applied checks live in
`../verify/references/product-md-output.md`; the ProductMD spec remains the
authority.

### Steering the interview

- **State ledger.** For every value, track its status in working memory: **supplied**, **accepted**, **inferred** (a temporary assumption), **TBD**, **excluded**, or **deferred**. This ledger is for steering the interview only. Never encode it into `PRODUCT.md` — no inline `assumed`/`confirmed` metadata and no review status disguised as condition states.
- **Keep moving.** If the user cannot answer two questions in a row, or asks to keep moving, offer to draft a thin first `PRODUCT.md` from the information already available, then continue refining. Use low-risk temporary assumptions only to keep moving, and record them in the handoff.

### Output gate (before producing `PRODUCT.md`)

Run Verify target `product-md-output`. Fix blocking findings before final
output unless the user explicitly asks for an unresolved draft. Keep minor findings
in the handoff when they are acceptable review risks.

### Product Memory Install

For a new product, use Install target `product-memory` after the `PRODUCT.md`
output gate passes. Memory owns the supporting-memory model and governance;
Install owns install mechanics.

Load `../install/references/product-memory.md` on demand when installing
product memory or checking the install gate. Use the Memory spec for authority,
supporting-memory roles, read order, classification, lifecycle, and conflicts.

### Generation rules

- For a new product, create or output `PRODUCT.md`, then use Install target
  `product-memory` for the surrounding product-memory surface.
- For a scoped update to an existing product with product memory, update only `PRODUCT.md` and any existing or newly needed supporting memory files within the requested scope.
- For an existing repository with `PRODUCT.md` but no `product-memory/`, do not silently reinstall product memory unless the user explicitly asks. Treat that case as future Setup pressure by default.
- Preserve manual content and unknown fields unless they clearly conflict with ProductMD.
- For a scoped update, change only the requested scope and any earlier product meaning the update makes necessary. Do not restart the interview or rewrite unrelated content.
- Route durable product meaning according to ProductMD, and route supporting memory according to the Memory spec. Do not hide accepted product truth in supporting memory.
- Treat practices or principles from external prompts as optional review input, not product truth. They become product memory only when accepted for this product and routed to the right surface.
- For simple products, `## Overview` may be enough body structure. Products with multiple roles, access states, sensitive/legal pressure, mechanics-heavy behavior, several map branches/items and actions, or composition-heavy map meaning use more `##` sections aligned with owners, and `###` headings for optional explanation slots.
- If the file may be read outside its repository, add a brief `## About This File` section after the H1 with `Format: ProductMD v0.1.11`, a one-sentence purpose, a `Reading:` key (frontmatter holds compact facts; body prose interprets them; backticked product-address references resolve to frontmatter addresses; syntax literals may also use code style), and `Spec: https://github.com/codynoskov/Meaningfall/blob/main/formats/product-md/spec.md`.
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

## Action Modes

Per root `SPEC.md` Action Modes and decision 0072, Guide grants:

- `automatic`: the temporary interview ledger and gap tracking inside a Guide run;
  running Verify `product-md-output` as the output gate inside a Guide run.
- `suggested`: product-memory install in an existing repository; the marked
  `AGENTS.md` product-memory block edit.
- `explicit`: durable `PRODUCT.md` writes are confirmed; product-memory install in a
  brand-new Guide-created workspace is approval-visible by default.

## Contract fallback

Use this only when the spec URL above is unreachable. It is a compact projection, not the authority — the ProductMD spec always wins.

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
