---
profile:
  identity:
    name: Field Notes Library
    kind: research publication
    audience: product teams
entities:
  articles:
    collection: true
    views:
      - in-card
      - in-section
    relations:
      - topics
  topics:
    collection: true
    relations:
      - articles
conditions:
  context:
    language:
      - en
    platform:
      - web
  states:
    publication:
      - draft
      - published
      - archived
map:
  product:
    contains:
      props:
        composition:
          shell: {}
      home:
        props:
          home: true
      articles:
        props:
          composition:
            complement: {}
      topics: {}
      about: {}
---

# Field Notes Library

## Overview

Field Notes Library is an English web publication for product teams who want reusable research notes, examples, and topic-oriented reading paths.

This ProductMD covers the public publication structure and stable article-reading semantics. It does not define a CMS schema, editorial workflow tool, authoring interface, or analytics implementation.

### Non-Goals

Do not put article fields, author schemas, tag rules, route parameters, or content-entry storage details in ProductMD frontmatter. Those belong in CMS, generated content, implementation, or later tooling.

## Entities

Field Notes Library is about **articles**, the research notes, and **topics**, the public reading paths that group them. Both are `collection: true` entities because the map records structural browsing surfaces while Entities preserves that each surface represents repeated same-shaped items. Publication status (draft/published/archived) is a condition.

## Conditions

`publication` is a product state because draft, published, and archived entries should be handled differently in public browsing and generated article surfaces. Draft entries should not be exposed publicly. Archived entries may remain referenceable, but should not be treated as current guidance without context.

### Validation And Review

Generated content should make publication state visible to editors and avoid presenting archived material as current. Empty topic results, missing articles, and not-found pages are implementation and validation coverage rather than ProductMD condition values.

## Map

These notes describe what each destination is for and roughly what belongs on it, as guidance for generating the pages — not their literal content.

**home** — the publication entry point: surfaces recent and notable articles and the main topic paths so a product team can start reading. A browsing front page, not an about page.

**articles** — the collection surface for research notes. Its `collection: true` entry in Entities marks it as a series of same-shaped article items, not a route wildcard or licence to invent map entries.

**topics** — reading paths that group articles by theme. Its `collection: true` entry in Entities marks topics as a public taxonomy, not a complete hand-written list; a topic page introduces the theme and lists its articles.

**about** — the publication's own description: who writes it, what it covers, how to read it. Secondary to the article and topic surfaces.

The default contained-item group preserves the shell role. `articles` also declares complement material for related reading and contextual notes when those are durable for this publication. Generated article pages may omit that material when none applies; do not encode that absence as a ProductMD state.
