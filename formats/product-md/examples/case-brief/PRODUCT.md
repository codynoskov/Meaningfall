---
profile:
  identity:
    name: Case Brief
    kind: AI-assisted support writing product
    audience: support teams
    contacts:
      support: support@casebrief.example
  references:
    ai_review_policy:
      source: TBD
      kind: policy
entities:
  cases:
    collection: true
    views:
      - in-list
    relations:
      belongs-to: customer
      handled-by: agent
      answered-with: reply
  reply: {}
  customer: {}
  agent: {}
conditions:
  context:
    language:
      - en
    platform:
      - web
  states:
    case:
      - open
      - waiting-on-customer
      - resolved
    draft:
      - none
      - generated
      - edited
      - approved
      - rejected
    review:
      - not-required
      - required
      - complete
actions:
  ai:
    - generate-draft
    - regenerate-draft
    - request-human-review
  support:
    - edit-draft
    - approve-draft
    - reject-draft
    - send-reply
map:
  product:
    contains:
      props:
        composition:
          shell: {}
      dashboard:
        props:
          home: true
      cases: {}
      review:
        contains:
          queue: {}
          policy: {}
  system:
    contains:
      signin: {}
      review-required: {}
mechanics:
  ai-assistance:
    - draft-generation
    - human-review-routing
    - sensitive-case-escalation
---

# Case Brief

## Overview

Case Brief helps support teams draft customer replies with AI while preserving human review for sensitive, risky, or policy-dependent cases.

This ProductMD covers case-level drafting, review pressure, AI action identity, and support reply operations. It does not define prompt templates, model settings, safety classifiers, message schemas, or provider APIs.

### Non-Goals

Do not encode prompt chains, model parameters, safety classifier logic, queue workers, or API endpoints in ProductMD frontmatter.

## Profile

`ai_review_policy` is a known-needed input source because this product can draft customer-facing text. It is marked `TBD` because the exact policy source has not been supplied. Agents should not infer final review requirements or safety claims from the product category.

## Entities

Case Brief is built around four nouns: **cases** (customer support threads), the **reply** drafted for a case, the **customer** the case belongs to, and the **agent** who edits and sends. `cases` is a `collection: true` entity because support cases are repeated work items, and its `in-list` view preserves the queue/scanning meaning without describing a concrete list component. Draft and review status are states of the reply (see Conditions), not separate entities; `send-reply` is the operation that delivers it (see Actions).

## Conditions

Case, draft, and review states are product-semantic. They change whether AI generation is useful, whether a support person can send a reply, and whether human review is required before generated text reaches a customer.

`review: required` is not an authoring diagnostic. It is a real product state for this workflow because it blocks direct sending until review is complete.

## Actions

### AI Actions

`generate-draft` and `regenerate-draft` are AI actions. They may be visible controls, but ProductMD records the durable operation rather than button behavior or model invocation details.

Draft generation reads case context, source material, and the support person's requested reply direction. Those inputs matter because the product is producing customer-facing language; generated files should keep sensitive account, billing, legal, and safety-adjacent material visible as review pressure without turning ProductMD into a prompt or message schema.

`request-human-review` is required when generated content touches sensitive account, billing, legal, or safety-adjacent material. Generated product files should preserve this action as review pressure rather than publishing generated output directly.

### Support Actions

`approve-draft` and `send-reply` are separate actions. Approval means the draft is acceptable for use; sending is the customer-contact operation.

`reject-draft` asks why a generated draft cannot be used so the case keeps review memory without requiring ProductMD to define review form fields.

### Feedback And Recovery

AI generation should tell the agent whether a draft is still being produced, cannot be produced, needs policy review, or is unsafe to send as-is. A failed generation should not erase the current case context or existing edited draft, and review-required feedback should explain who can unblock the reply.

### Sensitive Review

Generated replies that include policy interpretation, refunds, account suspension, privacy requests, safety matters, legal-sensitive material, or medical/financial claims should require human review unless a supplied review policy says otherwise.

## Map

The `cases` item is the structural surface for case work. Its collection type lives in Entities because support cases are repeated work items supplied by the support system or generated product data, not hand-written map entries. Each case needs case-writing work, policy context, source material, and human-review pressure when sensitive.

### System Items

The `system` branch is separate from `map.product`. The `review-required` system item exists because the product needs a recoverable path when a draft cannot be sent directly.

## Map Composition

The default item group has a shell role. The `cases` collection adds a complement role because case-writing work needs supporting case facts, policy context, or source material. The complement role is not a generic side panel; it belongs to case-writing work.

## Mechanics

The AI assistance mechanics are product-level domains, not prompt-chain or model-provider details. `draft-generation` names the durable drafting logic; `human-review-routing` names the policy-dependent routing between direct support editing and required review; `sensitive-case-escalation` preserves the fact that some cases require stronger handling even when the exact review policy source is still `TBD`.

Generated work should preserve these mechanics as product pressure without turning ProductMD into a safety classifier, prompt spec, queue definition, or policy table.
