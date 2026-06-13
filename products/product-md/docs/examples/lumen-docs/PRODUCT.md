---
profile:
  identity:
    name: Lumen Docs
    kind: developer documentation product
    audience: app developers integrating Lumen APIs
    links:
      repository: https://github.com/lumen-dev/lumen
conditions:
  context:
    language:
      - en
    platform:
      - web
  states:
    documentation:
      - current
      - archived
actions:
  support:
    - open-support-request
map:
  product:
    props:
      composition:
        uses: site-orientation
    contains:
      home:
        props:
          home: true
      guides:
        props:
          composition:
            uses: guide-reading
        contains:
          getting-started: {}
          authentication: {}
          webhooks: {}
          archive: {}
      reference:
        contains:
          endpoints: {}
          errors: {}
      support: {}
compositions:
  site-orientation:
    shell:
      nav:
        primary: site-primary
  guide-reading:
    shell:
      nav:
        primary: site-primary
        local: guide-section
navigations:
  site-primary:
    from: product
    depth: 1
  guide-section:
    from: -1
    depth: 1
    override:
      archive: does_not_apply
---

# Lumen Docs

## Overview

Lumen Docs helps app developers understand and integrate Lumen APIs through guides, reference material, and support paths.

The product is an English web documentation surface. This ProductMD covers navigation and documentation-reading structure, not API endpoint definitions, code samples, SDK behavior, or generated reference schemas.

### Boundaries

Do not encode API routes, endpoint request shapes, SDK package structure, example code, or versioning rules in ProductMD frontmatter. ProductMD preserves the documentation product surface and navigation semantics only.

Lumen Docs has no `entities`. Guides and reference pages are content reached through the product map, not things the product operates on, so they live in `map`. The one operation, `open-support-request`, already names its own object; a `support-request` entity would only repeat it. A documentation product is expected to have few entities or none.

The source repository is a public address, so it lives in `profile.identity.links`, not in `map`. The product's own home is the `props.home: true` item in `map`, not a profile field.

## Conditions

The `documentation` state distinguishes current material from archived material. Archived material can remain reachable for compatibility or migration work, but it should not be promoted as the ordinary learning path.

## Actions

`open-support-request` names the durable support operation. If generated files implement it as a form, ticket link, or contact handoff, they should reference this action without putting form fields or endpoint details in ProductMD.

The support request asks what integration task is blocked, which guide or reference context the developer used, and how support can respond. Secrets, API tokens, and production credentials should not be required for ordinary support; if troubleshooting ever needs sensitive material, that needs separate handling outside ProductMD.

A submitted support request should confirm receipt and say what happens next; the requester is usually already blocked, so a failed submission must not lose what they wrote or leave them guessing whether anyone will respond.

## Map

These notes describe what each destination is for and roughly what belongs on it, as guidance for generating the pages — not their literal content.

**home** — the documentation entry point: orients a developer to what Lumen does and routes them to getting-started, reference, or support. Short and task-routing, not marketing.

**guides** — learning and task flow. `getting-started` is the first-run path (install, authenticate, first call); `authentication` and `webhooks` are focused task guides; `archive` holds superseded guides. Concept-and-task prose with runnable snippets.

**reference** — lookup, not learning: `endpoints` and `errors` are dense, scannable surfaces a developer returns to mid-task. Structure for fast scanning, not start-to-finish reading.

**support** — a direct task destination where a developer opens a support request when guides and reference fall short; not a child of either docs branch.

## Compositions

`site-orientation` is the documentation-wide frame: project-level wayfinding through the `primary` exposure. `guide-reading` is the frame for the guides area; because a local `uses` replaces the inherited profile wholesale, it re-states the `primary` exposure alongside the guide-local `local` exposure rather than relying on inheritance.

## Navigations

`site-primary` is the project-level wayfinding across the top documentation destinations. `guide-section` is the reading navigation over the guides; its `override` keeps `archive` out of ordinary guide navigation. Archived material stays in the map and reachable by direct address — the override shapes one navigation, it does not delete the item or define route guards.

### Product Navigation Versus Local Anchor Navigation

The map records durable product items, and `navigations` records shaped views of them. Long generated guide pages may also include local heading or anchor navigation derived from page content. That local navigation is a realization detail of generated page files or body guidance, not a ProductMD navigation.
