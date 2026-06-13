---
profile:
  identity:
    name: Harbor Hotel
    kind: boutique hotel website with booking flow
    audience: leisure travelers and event guests
    contacts:
      reservations: reservations@harborhotel.example
entities:
  rooms:
    collection: true
    views:
      - in-card
    relations:
      - booking
  booking: {}
  guest: {}
conditions:
  context:
    language:
      - en
    platform:
      - web
  states:
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
    payment:
      - not-started
      - authorized
      - declined
      - refunded
actions:
  booking:
    - search-availability
    - hold-room
    - confirm-booking
    - cancel-booking
  payment:
    - authorize-payment
    - request-refund
map:
  product:
    contains:
      props:
        composition:
          shell: {}
      home:
        props:
          home: true
      rooms: {}
      dining: {}
      events: {}
      booking:
        props:
          composition:
            shell: {}
        contains:
          search: {}
          confirmation: {}
      legal:
        contains:
          terms: {}
          privacy: {}
---

# Harbor Hotel

## Overview

Harbor Hotel is a boutique hotel website with a booking flow for leisure travelers and event guests.

This ProductMD covers the public website, booking items, booking state pressure, and the embedded booking surface. It does not define room inventory schemas, provider APIs, payment endpoint details, or visual design.

### Non-Goals

Do not model provider API details, room schemas, tax calculation, settlement, or cancellation policy text in ProductMD frontmatter.

## Entities

Harbor Hotel is about a few nouns: **rooms** a guest can book, the **booking** itself (its search and reservation status live in Conditions), and the **guest**. `rooms` is a `collection: true` entity because the public rooms surface represents repeated bookable room options. Payment is recorded as booking-related state, not a separate entity here.

## Conditions

Booking state is nested because search and reservation have different meanings. A visitor can search without holding a reservation, and a held reservation should not be presented as confirmed.

Payment state is recorded only at product-behavior level. `authorized` means the product can continue toward booking confirmation. It is not a settlement ledger, receipt schema, or refund-policy definition.

## Actions

`search-availability`, `hold-room`, `confirm-booking`, and `cancel-booking` are durable booking operations. Generated product files may implement semantic forms and provider calls for them, but ProductMD should not define fields, calendars, inventory rules, or endpoint contracts.

Booking asks for stay intent: dates, party needs, selected room or offer, a way to reach the guest, and payment readiness when confirmation requires it. Payment details are provider-sensitive and should not become ProductMD fields; the product meaning is that a booking cannot be confirmed until the reservation and payment states support it.

`authorize-payment` may be provider-backed. It should not mark a reservation as confirmed until the booking state supports that interpretation. `request-refund` is included because cancellation and payment state create recovery pressure; refund policy copy still requires legal and operational review.

### Feedback And Recovery

Booking feedback should distinguish no availability, temporary provider failure, declined payment, held reservation, confirmed reservation, and cancelled reservation. Failed provider or payment paths should preserve enough context for safe retry without promising that a room is held when it is not.

## Map

Rooms, dining, and events are ordinary public items. Booking has its own item group because search and confirmation are transactional surfaces, not sections of the home page.

Terms and privacy are included because booking and payment create legal-sensitive public surfaces. Their exact copy and obligations still need current source review.

The ordinary site items have a shell role. Booking has its own shell role because the booking surface needs stable operating context across search, held reservation, confirmation, cancellation, provider recovery, and legal-sensitive copy.

The booking engine is an autonomous surface owned by an internal subproject or external provider. ProductMD records that ownership boundary in body guidance rather than as an `embed` entity type. The host product owns surrounding context and booking status; the embedded surface owns its internal form steps, errors, provider messages, and payment handoff. If this kind of ownership boundary keeps recurring across examples, it is a signal to revisit whether ProductMD needs a dedicated embed form later.
