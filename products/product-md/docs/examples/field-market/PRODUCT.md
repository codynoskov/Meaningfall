---
profile:
  identity:
    name: Field Market
    kind: maker marketplace with public shopping and seller admin
    audience: shoppers, makers, and marketplace staff
    contacts:
      support: support@fieldmarket.example
      seller: makers@fieldmarket.example
  legal:
    entity:
      name: Field Market Cooperative Ltd
      jurisdiction: United Kingdom
  references:
    marketplace_policy:
      source: TBD
      kind: policy
    refund_policy:
      source: TBD
      kind: policy
entities:
  shopper: {}
  makers:
    collection: true
    views:
      - in-card
  products:
    collection: true
    views:
      - in-card
    relations:
      made-by: makers
  listings:
    collection: true
    relations:
      offers: products
  orders:
    collection: true
    relations:
      includes: products
      placed-by: shopper
  payments:
    collection: true
    relations:
      settles: orders
conditions:
  context:
    language:
      - en
    platform:
      - web
    participant:
      - shopper
      - seller
      - staff
  states:
    account:
      - anonymous
      - shopper
      - seller
      - staff
    listing:
      - draft
      - submitted
      - live
      - paused
      - rejected
    order:
      - cart
      - placed
      - fulfilled
      - refunded
    payment:
      - not-started
      - authorized
      - declined
      - refunded
actions:
  cart:
    - add-to-cart
    - checkout
  listing:
    - submit-listing
    - approve-listing
    - reject-listing
    - pause-listing
  order:
    - fulfill-order
    - refund-order
  integration:
    - confirm-payment
    - reconcile-refund
map:
  product:
    props:
      composition:
        shell: {}
        complement: {}
    spaces:
      props:
        composition:
          shell: {}
      public:
        contains:
          home:
            props:
              home: true
          shop:
            contains:
              makers: {}
              products:
                props:
                  composition:
                    complement: {}
      seller:
        contains:
          listings: {}
          orders: {}
          payouts: {}
      admin:
        contains:
          listing-review: {}
          orders: {}
          refunds: {}
          settings: {}
      legal:
        contains:
          privacy: {}
          terms: {}
          refunds: {}
  system:
    contains:
      signin: {}
      checkout: {}
      order-confirmation: {}
      payment-result: {}
---

# Field Market

## Overview

Field Market is a two-sided maker marketplace with public shopping, seller administration, staff review, and commerce recovery.

This ProductMD covers the public shop, seller and admin surfaces, listing review, order handling, and payment-sensitive actions. It does not define product schemas, payment-provider endpoints, payout calculations, tax rules, shipping rules, or component design.

## Profile

The references are intentionally incomplete. `marketplace_policy` and `refund_policy` are known-needed input sources because listings, payments, refunds, and seller behavior need policy review before launch. Agents should not infer policy text or refund obligations from the marketplace category.

### Sensitive Review

Marketplace policy, refund language, seller eligibility, prohibited listings, disputes, and payment disclosures require human review before public launch.

## Entities

Field Market is organized around a few entity meanings: **shopper**, **makers**, **products**, **listings**, **orders**, and **payments**. Makers, products, listings, orders, and payments are `collection: true` entities because the marketplace works with repeated same-shaped records. Product views and relations preserve only the product-level associations needed here: products appear as reusable shopping units and are made by makers; listings are seller-managed offers for products; orders connect shoppers to purchased products.

Payments earn an entity here because the marketplace must preserve payment and refund records across checkout, provider return, order support, and staff recovery. That differs from a simple booking site where payment can be recorded as booking-related state only. Listing, order, and payment states live in Conditions; operations on them live in Actions.

## Conditions

Participant context changes what people can see and do: shoppers browse and buy, sellers manage listings and orders, and staff review marketplace quality and support disputes.

Listing state prevents generated seller and admin flows from treating submitted, rejected, paused, or live items as the same thing. Order and payment states are product-semantic because they change confirmation, support, refund, and recovery behavior.

## Actions

`add-to-cart` and `checkout` are visible shopper actions, but ProductMD does not define cart fields, checkout steps, or payment provider mechanics.

Checkout asks for enough buyer, delivery, and payment intent to place an order and route provider-backed payment. Contact and payment-sensitive material should be handled with clear visibility and lifetime boundaries; ProductMD records why the product needs the information, not field names or payment-provider payloads.

Listing actions are review-sensitive. `approve-listing` and `reject-listing` should be staff/admin actions with enough generated review context to avoid accidental publication.

`confirm-payment` is externally triggered by a payment result. `reconcile-refund` may follow staff action or provider callback. Generated integration code may reference these actions, but ProductMD does not define webhook endpoints, queues, retries, or settlement rules.

### Feedback And Recovery

Checkout should tell shoppers whether an order is not yet placed, placed, blocked by payment, or waiting on provider confirmation. Listing review should tell sellers whether a listing is live, rejected with an actionable reason, paused, or still waiting for staff. Refund and order-support feedback should preserve the order and payment record so recovery does not imply a new purchase or erase dispute context.

## Map

The shop contains maker and product structural surfaces. Their collection facts live in Entities because makers and products are supplied by marketplace data or generated content, not by hand-written map enumeration.

### Product And Legal Items

Seller and admin branches are separate because seller self-service and staff review have different authority. Legal items exist because commerce, marketplace policy, and refunds create real product pressure.

### System Items

The `system` branch is separate from `map.product`. Sign-in, checkout, order confirmation, and payment result items live there because they support access, transaction, recovery, or provider-return crossings rather than ordinary marketplace browsing.

## Map Composition

The product branch has shell and complement roles for marketplace-wide orientation, account/access context, and policy/trust context.

`spaces` is used because public, seller, admin, and legal are peer product spaces. The shared space-level shell role applies to those spaces without creating one-off composition entities.

The product collection has a complement role because product detail items need purchase context, seller trust, stock, delivery, or related action pressure. The details belong in body prose or generated product files, not inside `props.composition`.

Seller and admin spaces have operational items. Their navigation and controls are realization choices derived from those spaces, not separate ProductMD `navigation` entries.
