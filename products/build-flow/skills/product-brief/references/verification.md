# product-brief verification reference

Per-owner checks applied at the output gate — the Seed Loop `settled` check — before producing or updating `PRODUCT.md`. These are the *applied* checks; the *authority* for what is valid is the contract (`docs/spec.md`). When in doubt, the spec wins.

Load this when finishing an owner or before final output. Each owner lists what belongs, the sharpest "looks-like-but-isn't" distinctions, and shape checks.

## profile

Belongs: exact public identity facts, exact legal/formal facts, supplied or external **input** references, known-needed `TBD`.

- Future pages/URLs (`/privacy`, future site) → `map`/`actions`/body, not `references`. *Existing Instagram profile = a source; a future `/privacy` route is not a fact.*
- Audience/role/plan/platform/region that **changes behavior** → `conditions`. *"audience: parents" can be identity; `role: parent` is a condition if parents see different flows.*
- Purpose, outcomes, scope, principles, tone rationale → body. Only exact public facts (`kind`, a supplied tagline) stay in `profile.identity`.
- Legal advice/obligations ("must comply with GDPR", "ask a lawyer") → body. `profile.legal` holds exact facts only; legal **sources** → `references`.
- Contact facts → `profile.identity.contacts`; "open ticket", "book consultation" → `actions`.
- `TBD` only when the fact is known to matter; otherwise omit.

## entities

Belongs: named product meanings under direct `entities.<name>` entries. Entries may be empty objects, or compact mappings with `collection`, `views`, and `relations` when those facts preserve product meaning.

- Names what things **are**, not their states (→ `conditions`), operations (→ `actions`), map items (→ `map`), or governing logic (→ `mechanics`). *`reply` is an entity; `reply: draft/approved/sent` is a condition; `send-reply` is an action.*
- Use `collection: true` when the entity represents a series of same-shaped product things. Do not use `collection: true` in `map`.
- Do not use entity `type`, including `type: default`, `type: collection`, or `type: canvas`.
- Omitted `views` means no special view variants are recorded in frontmatter; it does not mean no representation.
- `views` names semantic representation variants of the same entity meaning. For collection entities, views always describe one collection member, not the collection index or aggregate digest; collection indexes belong in `map`, and aggregate/digest meaning belongs in body prose or composition. Prefer the starter names `in-card`, `in-section`, `in-list`, and `in-summary` when they fit; add a new name only for a distinct meaning those would blur.
- Entity `views` and map `composition` are independent axes: a view says how one entity meaning is represented; a composition role says which semantic regions exist at a map node.
- `relations` records semantic associations with other entities, not cardinality, foreign keys, or database shape. Prefer `verb: target` for directed or asymmetric relations; use bare target lists only for symmetric or self-evident associations.
- Do not nest entities to show relationships; use `relations`.
- Not fields, schema, lifecycle graphs, provider APIs, or component forms — name the entity here; explain non-obvious view, relation, and meaning in the body.
- Omit when the product has no durable domain objects (a simple landing page).
- Do not mirror the whole map into `entities`. Promote a map item only when it needs `collection`, `views`, `relations`, cross-owner references, or body explanation.
- When one product meaning needs both map structure and entity facts, use the identical name in both owners; ProductMD does not infer aliases across owners.

Shape:

```yaml
entities:
  case: {}
  article:
    collection: true
    views:
      - in-card
    relations:
      - topic
  workload-board:
    relations:
      - task
      - assignee
```

## conditions

Belongs: context/states that change product meaning (access, routing, content, obligations, available actions, generated output, review). Not generic implementation, component, loading, or visual states. The same word lands differently per product.

- Validation-like (`required`, `invalid`, `valid`) → form/validation guidance. *"invalid email format" = validation; `email_verified` is state if it gates access.*
- Feedback-like (`pending`, `success`, `failure`, `empty`) → feedback guidance. *form `success` = feedback; `application: approved` = state.*
- Resolver-outcome (`applies`, `available`, `fallback used`) → resolver/rules/body, unless the product exposes it as durable state.
- Generic runtime (`loading`, `saving`, `timeout`, `offline`) → implementation, unless the mode changes product behavior (`mode: offline` for a field app).
- Component interaction (`hover`, `selected`, `disabled`) → design system/component. *a button's `disabled` = component; `access: disabled` = state if it changes account behavior.*
- Diagnostics/review (`assumed`, `confirmed`, `needs review`) → interview/review notes; use `TBD` in frontmatter. *`human_review: required` may be state in a regulated AI workflow.*
- System item (`not found`, `forbidden`, `maintenance`) → `map`/`actions`/`mechanics`, unless it is meaningful product behavior (`access: forbidden` with product-specific recovery).
- Transition graphs → list the state **axis** only; put transitions/allowed moves in body or `actions`, not full graphs.
- Legal/privacy/consent → may be conditions when they gate access, data handling, or obligations; otherwise legal facts or `references`.
- Coverage: each recorded state value connects to described consequences somewhere in the body (an entity, place, or action it changes), or is self-evident; a value no prose touches is an orphan — explain it or remove it.

## actions

Belongs: durable product operations. Not endpoints, functions, button labels, form schemas, or component events.

- Form-like ("submit application") → list the action; the semantic form/inputs are downstream.
- Button/component events (click, toggle, hover, expand) → realization; keep only the durable operation behind the event.
- API/implementation ops (`POST /checkout`, cron, webhook) → translate only when there is product meaning (`confirm-payment`, `sync-entitlements`).
- State transitions → the states belong in `conditions`; the operation that drives them may be an action.
- Feedback/outcome words (`pending`, `success`, `blocked`) → body feedback guidance, unless there is a real operation (`retry-payment`, `complete-onboarding`).
- Coverage: primary and risky actions have feedback and recovery expectations in body prose (what the actor learns on success, failure, progress); routing feedback out of frontmatter does not mean dropping it.
- Triggered actions ("when", "after", "on") → the triggering state is recorded in `conditions`; a trigger on an unrecorded event is a missing state, not prose-only coverage.
- Long output description inside an action → the output is an entity or map item with its own sections; the action only references it.

Shape: group by durable product area, not UI placement; use operation names (`reset-password`, not "reset button"; `sync-entitlements`, not `GET /entitlements`); names are open, but examples prefer kebab-case; no descriptions, nested objects, schedules, queues, retry intervals, or form schemas in frontmatter; action order is not workflow/priority order; do not infer visibility from group name.

## map

Belongs: durable product-map structure across product, system, notification, integration, flow, and other branches. Not page sections, components, framework routes, route tables, CMS schemas, or visual/layout shapes.

- Top-level branches under `map` are durable branch classes such as `product`, `system`, `notifications`, or `integrations`. Do not use reserved top-level field names such as `profile` as map branch names.
- `product` is the main product branch. `system` is for access, recovery, provider-return, error, state-crossing, or operation-support items that are not ordinary product items.
- `spaces` is an optional grouping container for two or more large peer logical spaces. Do not create a single space in advance.
- `contains` is the standard child-item container and may contain one item.
- `props` is the canonical property container for branches, spaces, items, and groups. Do not introduce `meta`.
- ProductMD-reserved props may be written directly on a branch, space, or item when unambiguous and normalize into `props`; custom local props stay inside `props`.
- `props` is open for local product-specific properties except for ProductMD-reserved prop names. `name` or normalized `props.name` is a rare escape hatch when the YAML key cannot be the object's real name.
- `home: true` or normalized `props.home: true` marks the primary useful product entry point when one is selected.
- Collection facts use `collection: true` under `entities`; do not use quoted `"..."`, `props.open: true`, `collection: true` in `map`, or representative `sample-*` items just to show collection membership.
- `composition` or normalized `props.composition` is either inline roles (`shell`, `complement`, `overlay`) or one `uses` reference to top-level `compositions`.
- Do not mix `uses` with inline roles in the same `props.composition` value.
- Generated files prefer catalog form: named `compositions` referenced from map scopes, even for thin profiles; inline composition on user-authored files is preserved. Profiles contain role branches and may host `nav` exposure references; profiles do not contain `uses`.
- `props.composition.uses` is reference-only. It does not carry local role deltas; a local `uses` replaces inherited composition at that scope.
- `reset` or normalized `props.reset` resets selected prop groups at the current scope; `does_not_apply` suppresses one inherited named entry inside a prop group.
- Composition role branches should usually be empty objects. Do not list page contents or custom regions inside them unless explicit product pressure requires a repeated semantic part.
- Direct branch/space/item composition applies at that node's scope; `contains.props.composition` or `spaces.props.composition` applies to the child group, including group-level `uses`.
- A composition role may carry reserved `nav` for named navigation exposures: a mapping from exposure name to a top-level `navigations` entry name, or an inline projection body in mapping form (catalog references preferred in generated files). Inside `nav`, a scalar value is always a navigation name, never depth shorthand. Exposure names describe function, not layout placement; `does_not_apply` suppresses an inherited exposure.
- Top-level `navigations` is a mapping from navigation name to one shaped map projection. Default entries use `from`, `depth`, optional `override`, optional `items`, and optional `links`; omitted `from` means `current` except for `type: breadcrumbs`, where it means the nearest map/scope root; omitted `type` means `default`; scalar entry values mean `depth` only under top-level `navigations`; `override` keys address immediate children of the `from` root by bare name or deeper subjects by relative dot path; `does_not_apply` inside `override` removes a named subject from that navigation. Navigation names describe function, not placement; entries never list the scopes where they apply.
- Use navigation `items` only for curated or cross-branch links, including profile links and external URLs. `links` is a compact bucket shorthand for explicit link-heavy `items`. Scalar link targets resolve as URL, `profile.*`, then absolute map path. Do not re-list a branch's own children when `from` plus `depth` can project them.
- `type: breadcrumbs` is allowed for map-derived trails. In-page heading/anchor navigation stays in generated page files or body guidance for now.
- A machine-facing index item (such as an `llms.txt`) may have a named navigation as its content; state that in the body rather than inventing a new hosting field.
- Website navigation is evidence for product structure, but nav labels, sidebars, route implementation, and component hierarchies do not automatically become map items.

Shape: mapping, not list. `map.<branch>.contains.<item>` and `map.<branch>.spaces.<space>` are named addressable elements. Lists appear only for ordered flows, steps, or other sequence-bearing values.

## mechanics

Belongs: durable internal product-logic domains that would otherwise be lost between other owners. A mechanic affects several actions, states, or map items and is not captured by any one action or condition. A compact domain index, used only for mechanics-heavy products.

- Conditions disguised as mechanics: `review: required` → `conditions`; `human-review-routing` → `mechanics` if review routing is durable logic.
- Actions disguised as mechanics: `request-human-review` → `actions`; `escalation-policy` → `mechanics` if multiple actions/states rely on it.
- Map disguised as mechanics: `review.queue` → `map`; `assignment-policy` → `mechanics` if there is a durable rule for how work reaches the queue.
- Realization disguised as mechanics: `toolbar` → realization/body guidance; `tool-modes` → `mechanics` if mode behavior is product meaning.
- Implementation disguised as mechanics: `ranking-policy` → `mechanics`; exact scoring weights, indexes, prompt chains, service calls → out of ProductMD.

Shape: mapping from domain to compact hyphenated names; no nested workflow specs, decision tables, permission matrices, transition graphs, or implementation plans.

## body

Belongs: orientation, rationale, assumptions, boundaries, and interpretation that explain the compact YAML.

The body should not: duplicate YAML as a prose table; restate ownership, nesting, or existence already encoded by the map; hide missing frontmatter facts that belong in an owner; introduce a second product model; turn every possible future feature into current scope; become interview or generation procedure; replace a design system or visual styling layer for visual tokens, typography, or component styling; become route/component/endpoint/job/workflow/validator implementation.

## cross-cutting output checks

- YAML frontmatter parses; a body-only file stays body-only if structured facts were not selected.
- Frontmatter uses exact top-level names and the order `profile, entities, conditions, actions, map, compositions, navigations, mechanics`; no aliases.
- Backticked product-address references in body prose resolve to frontmatter addresses; code-styled YAML keys, values, syntax examples, and other literals are allowed and do not need to resolve as addresses.
- Review status (supplied / inferred / accepted / excluded / deferred) lives in the handoff, not in the file.
- No invented legal, contact, policy, or sensitive-data facts.
- A scoped update changes only the requested owner and any earlier owner the change makes necessary.
- Source material is semantically normalized, not mirrored. URL inventories, repo folders, docs sidebars, implementation routes, and component catalogs do not become ProductMD structure unless they express durable product meaning.
- ProductMD does not record component catalogs, widgets, layout mechanics, transient UI state, loading behavior, or visual styling. Keep realization pressure in body guidance, handoff notes, generated output, or design-system/implementation work as appropriate.
