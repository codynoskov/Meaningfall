---
profile:
  identity:
    name: Ops Console
    kind: internal operations console
    audience: support, compliance, and operations staff
entities:
  incidents:
    collection: true
    views:
      - in-list
      - in-summary
    relations:
      affects: customers
      reviewed-through: reviews
  customers:
    collection: true
    views:
      - in-summary
  reviews:
    collection: true
    views:
      - in-list
      - in-summary
  workload-board:
    relations:
      brings-together:
        - incidents
        - customers
        - reviews
conditions:
  context:
    language:
      - en
    platform:
      - web
    surface:
      - internal
  states:
    session:
      - active
      - expiring
      - expired
    incident:
      - quiet
      - active
      - resolved
    review:
      - none
      - pending
      - escalated
actions:
  account:
    - signin
    - signout
  incident:
    - publish-update
    - resolve-incident
  review:
    - approve-review
    - escalate-review
  system:
    - expire-session
    - archive-resolved-incident
map:
  product:
    props:
      composition:
        shell: {}
        overlay: {}
    contains:
      dashboard:
        props:
          home: true
          composition:
            shell: {}
            complement: {}
            overlay: {}
        contains:
          incidents: {}
          customers: {}
          reviews: {}
          workload-board: {}
  system:
    contains:
      signin: {}
      session-expired: {}
      forbidden: {}
mechanics:
  operations:
    - incident-priority
    - review-assignment
    - escalation-policy
  access:
    - session-expiration
    - permission-resolution
---

# Ops Console

## Overview

Ops Console is an internal web console for support, compliance, and operations staff handling incidents, customer context, and review queues.

This ProductMD covers durable console structure, operational state pressure, semantic overlays, and staff/system actions. It does not define permission matrices, queue infrastructure, backend jobs, route guards, or component interaction details.

### Non-Goals

Do not encode incident workflows, review assignment, RBAC, event buses, endpoints, or component behavior in ProductMD frontmatter.

## Entities

Ops Console is built around repeated work objects staff handle: **incidents**, **customers**, and **reviews**. They are `collection: true` entities because the console works with repeated operational records. `in-list` and `in-summary` preserve scanning and status meanings without specifying table, card, or dashboard components. Their states (incident quiet/active/resolved, review pending/escalated) live in Conditions; the logic that prioritizes and assigns them lives in Mechanics.

`workload-board` is an entity because it preserves the relationship surface where active incidents, customer context, and pending reviews are understood together. ProductMD does not decide whether that surface is realized as a board, grid, graph, chart, or custom component.

## Conditions

Session, incident, and review states are product-semantic because they affect staff access, operational status, review urgency, and recovery. They are not a complete runtime model. Generic loading, failed requests, empty queues, disabled controls, and websocket reconnect states remain implementation coverage unless they become product-level behavior.

## Actions

`publish-update`, `resolve-incident`, `approve-review`, and `escalate-review` are staff actions. Generated pages should preserve audit and confirmation pressure for high-risk operations.

Staff actions ask for operational meaning rather than UI fields: incident updates need public-facing status content, resolution needs a reason staff can stand behind, and review escalation needs enough context for the next accountable person. Sensitive customer context should remain visible only to authorized staff and should not leak into public incident language.

`expire-session` is state-triggered by session state. It should not be exposed as an ordinary button. `archive-resolved-incident` may be automatic after an incident is no longer active, but ProductMD does not define schedule, queue, or retention mechanics.

### Feedback And Recovery

Staff feedback should distinguish an operation that is pending from one that has taken effect, and a blocked operation should say what blocks it — permission, review state, or an expired session — because staff act on incidents under time pressure. Destructive or access-changing operations should confirm consequences before they run.

## Map

`dashboard` has `props.home: true` because the dashboard is the home item and also owns core console items. Incidents, customers, reviews, and workload-board are contained console work areas reached through the dashboard, not summary widgets for sibling items that live elsewhere.

### System Items

The `system` branch is separate from `map.product`. System items are restricted to access and recovery surfaces. They should not appear in ordinary console navigation.

## Map Composition

The console is operational, not browsing-led. The product branch has shell and overlay roles because operational context and interruption/recovery surfaces must remain stable across console work. The dashboard item has shell, complement, and overlay roles because incidents, customers, and reviews are working items that need surrounding context.

The overlay role is justified because several overlay-like product meanings are durable console-wide surfaces rather than incidental component details:

- `session-timeout` is a focused decision dialog for an expiring session.
- `destructive-action-confirmation` is a focused confirmation dialog for high-risk staff operations.
- customer context because staff often need supporting context without leaving the current work.
- review-note preview because it is anchored to local review material and should stay lightweight.
- operation feedback for action outcomes.
- support escalation because it can remain available across console surfaces.

Triggers, stacking, timing, permission checks, retry behavior, exact overlay types, and action logic belong to generated files, implementation, realization guidance, or later tooling, not to ProductMD `props.composition`.

## Mechanics

Ops Console is mechanics-heavy because staff work depends on internal product logic that is broader than individual actions or items. `incident-priority`, `review-assignment`, and `escalation-policy` preserve the operational domains that decide which work needs attention and who should handle it. `session-expiration` and `permission-resolution` preserve access logic that affects recovery and staff authority.

These mechanics names are not permission matrices, queue rules, event buses, or backend jobs. Detailed routing, RBAC, retention, and scheduling remain outside ProductMD unless a generated file or later tool gives them a concrete home.
