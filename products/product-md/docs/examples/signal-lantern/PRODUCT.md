---
profile:
  identity:
    name: Signal Lantern
    kind: incident communication product
    audience: small operations teams
entities:
  incident: {}
  updates:
    collection: true
    views:
      - in-summary
    relations:
      - incident
conditions:
  context:
    language:
      - en
    platform:
      - web
  states:
    visitor:
      - anonymous
    incident:
      - quiet
      - active
      - resolved
actions:
  public:
    - request-demo
  operations:
    - publish-update
map:
  product:
    contains:
      props:
        composition:
          shell: {}
      home:
        props:
          home: true
      incident-status:
        props:
          composition:
            complement: {}
  system:
    contains:
      request-demo: {}
      publish-update: {}
---

# Signal Lantern

## About This File

Format: ProductMD v0.1.11
Purpose: This file records product input for this project: durable meaning, selected structure, assumptions, boundaries, and references that should guide future work.
Reading: Frontmatter holds compact product facts; body prose interprets them and never restates them. Backticked product-address references in prose resolve to frontmatter addresses; syntax literals may also use code style.
Spec: https://github.com/codynoskov/Meaningfall/blob/main/products/product-md/docs/spec.md

## Overview

Signal Lantern helps small operations teams communicate incident status clearly during urgent service interruptions.

It is an English web product for anonymous public visitors and small operations teams. This ProductMD describes a first public incident-communication surface, not a full monitoring system, automated alerting product, or operations console.

### Expression And Copy

Public status language should be clear and action-oriented. The product should avoid implying that an incident is resolved until an operator has confirmed the resolution.

## Profile

Signal Lantern should stay centered on urgent public communication. Product language should favor clarity, current status, and operational trust over broad marketing claims.

The profile is intentionally compact. Missing provider, contact, and legal facts should not be silently filled from generic SaaS assumptions.

## Entities

Signal Lantern is about the **incident** and the **updates** published about it. `updates` is a `collection: true` entity because public incident communication depends on repeated status updates; `in-summary` preserves the recap meaning without defining a concrete component. The incident's quiet/active/resolved status is a condition; `publish-update` is the operation that adds an update.

## Conditions

English web is the only supported context for the first version.

Anonymous visitors can read public incident status. Quiet is the ordinary baseline incident state. Active and resolved incident states matter because public status language must distinguish ongoing disruption from confirmed recovery.

Loading, empty, error, and not-found coverage is still expected during implementation, but those are realization checks rather than ProductMD conditions for this product.

## Actions

Demo requests are handled manually unless a product owner confirms automated scheduling. Incident publishing is part of the product direction, but the minimal landing page may only describe it.

A demo request asks how to contact the visitor and what incident-communication problem they want help with. It should not ask for production incident details, secrets, or customer data at this stage.

A demo request should confirm receipt and promise human follow-up; a failed request must not silently drop the visitor's message. A published update should be immediately visible on the public status surface, because trust depends on knowing the status is current.

## Map

### Product Items

The first public surface is a landing page with an incident-status destination.

### System Items

Request demo and publish update are system items because they support product actions rather than ordinary browsing. They are not children of the product branch and should not appear as ordinary public navigation.

The incident-status item has a complement role for incident context or related updates.
