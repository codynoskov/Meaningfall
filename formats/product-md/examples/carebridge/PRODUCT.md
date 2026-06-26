---
profile:
  identity:
    name: CareBridge
    kind: client intake and care coordination portal
    audience: small counseling clinics
  legal:
    entity:
      legal_name: TBD
      jurisdiction: TBD
  references:
    clinic_privacy_policy:
      source: TBD
      kind: policy
    wcag_2_2:
      source: https://www.w3.org/TR/WCAG22/
      kind: accessibility
entities:
  client: {}
  clinician: {}
  intake: {}
  documents:
    collection: true
    relations:
      - client
  messages:
    collection: true
    relations:
      - client
conditions:
  context:
    language:
      - en
    market:
      - us
    platform:
      - web
  states:
    account:
      - anonymous
      - client
      - clinician
      - admin
    intake:
      - not-started
      - in-progress
      - submitted
      - needs-review
      - accepted
      - withdrawn
    consent:
      - not-requested
      - pending
      - granted
      - withdrawn
    access:
      - public
      - gated
      - forbidden
actions:
  account:
    - signin
    - signout
  intake:
    - start-intake
    - submit-intake
    - withdraw-intake
  consent:
    - provide-consent
    - withdraw-consent
  clinician:
    - review-intake
    - request-more-information
    - accept-intake
map:
  product:
    spaces:
      props:
        composition:
          shell: {}
      public:
        contains:
          home:
            props:
              home: true
          services: {}
          privacy: {}
          accessibility: {}
      client:
        contains:
          intake:
            props:
              composition:
                complement: {}
          documents: {}
          messages: {}
      clinician:
        props:
          composition:
            shell: {}
        contains:
          review-queue: {}
          client-record: {}
      admin:
        contains:
          staff: {}
          audit: {}
  system:
    contains:
      signin: {}
      consent: {}
      forbidden: {}
      intake-withdrawn: {}
---

# CareBridge

## Overview

CareBridge helps small counseling clinics collect client intake information, consent, and follow-up materials in a calmer, more reviewable way than scattered email or paper forms.

It is an English web portal for clients, clinicians, and clinic administrators in an initial US-market context. This ProductMD describes public information, client intake, consent handling, clinician review, and basic admin responsibility.

### Product Intent

#### Outcomes

CareBridge should reduce intake confusion for clients and reduce review burden for clinic staff. Clients should understand the next required step, and clinicians should be able to tell which intakes are ready for review.

#### Scope

This ProductMD version covers the product structure needed for intake and review. Scheduling, billing, telehealth sessions, insurance claims, emergency support, and clinical treatment notes are intentionally outside this version.

#### Product Principles

CareBridge should make status and next steps clear without making clinical, legal, eligibility, or emergency-support promises.

### Expression And Copy

Use calm, plain, non-clinical language. Do not imply diagnosis, emergency support, treatment approval, or guaranteed service access.

## Profile

### Identity

`client intake and care coordination portal` should be read as an operations product for clinics, not as a clinical decision system. Later generated surfaces should preserve the difference between collecting information, coordinating review, and making care decisions.

### Legal

The legal facts are intentionally incomplete. `TBD` values matter because this product handles sensitive information, but agents must not infer the legal entity, jurisdiction, or final consent obligations from the product category.

### References

`clinic_privacy_policy` is a known-needed input source, not a future generated privacy page. `wcag_2_2` is a chosen accessibility reference for generated work. Neither reference is a compliance claim by itself.

### Sensitive Or Legal Review

Privacy policy, retention periods, emergency disclaimers, consent copy, accessibility statement, and clinic-specific legal owner are review-required before launch.

## Entities

CareBridge is built around a few nouns: the **client** and the **clinician** (the people the portal serves), the **intake** (the central record a client submits and a clinician reviews), and the **documents** and **messages** attached to a client. `documents` and `messages` are `collection: true` entities because clients may have repeated attached records. `client` and `clinician` also appear in `conditions` as account roles; intake and consent *status* are states (see Conditions), not separate entities.

## Conditions

### Context

English web in the US market is the first supported context. If another market or language is added later, references, consent language, privacy handling, and generated copy should be reviewed together.

### States

The `account`, `intake`, `consent`, and `access` states are product-semantic because they change what people can see, submit, review, or recover.

The first value in each state list is the ordinary baseline when such a baseline exists. These lists are not transition graphs. Allowed transitions and edge cases belong in body guidance, generated workflow files, implementation, or later accepted structured syntax.

#### intake

`intake` describes the client intake lifecycle. `submitted` means the clinic has received material for review; it does not mean the client has been accepted for care. `needs-review` is clinician-facing pressure for review queues and status copy.

#### consent

`consent` affects whether intake can proceed and what recovery guidance the client needs. `withdrawn` should not silently erase the client record or imply legal effect without confirmed policy source.

### Coverage

Loading, generic form error, empty inbox, upload progress, network failure, and not-found states are still expected downstream coverage. They are not ProductMD conditions unless they change intake workflow, access, consent, or review obligations.

## Actions

### Intake Actions

#### start-intake

`start-intake` begins the client-facing intake process. It may require account or consent state, but ProductMD does not define a form schema or route guard here.

#### submit-intake

`submit-intake` sends client-provided intake material for clinic review. On receipt, the product should confirm review intake, not acceptance for care. If submission fails, the product should preserve entered work when possible and offer a safe retry path.

Intake asks for enough client context, presenting concern, consent, and attached material for a clinician to decide what should happen next. Health, identity, contact, and document information are sensitive; generated work should explain why each group is needed and avoid exposing it outside the client and authorized clinic review surfaces.

#### withdraw-intake

`withdraw-intake` should require confirmation because it changes client workflow state. The generated product should explain what access or review state changes, but exact legal effect depends on confirmed policy material.

### Consent Actions

#### provide-consent

`provide-consent` allows intake to continue when consent is required. Generated forms may implement the exact consent capture, but the legal copy and policy source need review.

#### withdraw-consent

`withdraw-consent` changes available actions and recovery guidance. It should not imply data deletion unless a confirmed policy source says so.

### Clinician Actions

#### request-more-information

`request-more-information` returns the intake to the client with recoverable next steps. The response should be specific enough for the client to act without exposing internal review notes.

#### accept-intake

`accept-intake` marks the intake as accepted for the product workflow. It should not imply clinical diagnosis, treatment approval, insurance approval, or emergency support.

### Validation Guidance

Generated intake forms should handle missing required values, invalid contact details, incomplete consent, and document upload failures. Keep validation close to generated forms and inputs; ProductMD records the cross-product expectation only.

### Recovery And Confirmation

State-changing, sensitive, or abandonment-prone flows should preserve work when possible and explain consequences before discarding progress.

## Map

### Public And Role Areas

The map keeps public, client, clinician, and admin spaces separate because those spaces have different authority and review responsibilities. The space names are durable product structure, not route implementation.

#### client

The client branch owns intake, documents, and messages. It should not expose clinician review tools or admin audit surfaces.

#### clinician

The clinician branch owns review queues and client-record review. It does not imply full clinical documentation or treatment-note functionality in this ProductMD version.

### System Items

The `system` branch is separate from `map.product`. System items support access, consent, and recovery state changes. They do not define route guards or a workflow graph.

#### forbidden

`forbidden` exists because gated or restricted access needs a recoverable item. The item should explain what happened and what the person can do next without exposing protected information.

#### intake-withdrawn

`intake-withdrawn` preserves recovery pressure after a client withdraws intake. It should not be treated as an ordinary product item or marketing item.

## Map Composition

### Product Spaces

The public, client, clinician, and admin spaces share a shell role. Their content is the item itself and body guidance; detailed page sections belong in generated page content unless they create durable product-map pressure.

### Client And Clinician

The client intake item has a complement role for review-sensitive guidance, consent context, and recovery cues. Clinician has an additional shell role because review work needs persistent operational context across review queues and client-record review.

#### clinician

Current intake and review state should remain visible during clinician review work. This is durable operational status, not generic success, failure, loading, or validation feedback.
