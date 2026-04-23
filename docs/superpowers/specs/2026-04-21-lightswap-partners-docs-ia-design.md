# LightSwap Partners Docs IA Design

Date: 2026-04-21

## Summary

Restructure the Mintlify documentation site from an API-centered site into a broader **LightSwap partners** documentation hub.

The site should stay intentionally small and conservative:

- one tab only
- sidebar-driven navigation
- no top navigation menu
- public partner-facing language
- current live content only, plus one visible `Widget (coming soon)` page

The goal is to make the docs useful for both business-oriented partner readers and developers, while leaving a clean path for future integration surfaces without forcing another information architecture rewrite later.

## Current state

The repo already started moving toward a broader documentation site, but it is still structurally inconsistent:

- `docs.json` now includes broader sections such as Getting Started, but the actual useful content still lives mostly in the Partner API pages.
- `main-info.mdx`, `faq.mdx`, and `support.mdx` are placeholders.
- site-level framing in `docs.json`, `README.md`, and `AGENTS.md` still describes the site primarily as a Partner API docs site.
- the existing API usage and API reference content is mostly sound and should be preserved where possible.

This means the best path is a restructure and reframe, not a full rewrite.

## Goals

- Position the site as **LightSwap partners**, not only as API docs.
- Support two main audiences:
  - partner/business readers who need a clear overview, fee-sharing explanation, and support path
  - developers who need integration guidance and API reference quickly
- Preserve the strong parts of the current API content.
- Introduce a structure that can grow later to widget and other integration methods.
- Keep the navigation short and understandable with today’s actual content.

## Non-goals

- Do not add deep future-doc sections for non-live integrations.
- Do not create a changelog, case studies, onboarding workflow section, or broad use-case library in this phase.
- Do not expose internal database, admin, provider, or key-generation details.
- Do not rewrite the OpenAPI reference structure beyond relocating it cleanly in navigation.

## Audience and positioning

The site is a **partner-facing umbrella docs site**.

It should not read like a developer portal only, and it should not read like a marketing microsite.

The home page should act as a **partner hub**:

- explain what LightSwap partners is
- explain what can be integrated today
- route readers into API usage, fee sharing, support, and future widget direction

## Naming model

Use a **hybrid naming approach**:

- broad section names at sidebar-group level
- task-oriented page names within groups

Important naming decisions:

- site name: **LightSwap partners**
- do not use `Partner API` as the primary user-facing integration name in navigation
- use **API Usage** instead of plain `API`
- keep **API Reference** as the technical reference section name

## Final information architecture

Use one tab only.

Sidebar structure:

- **Overview**
  - `Introduction`
  - `Fee sharing`
- **Integrations**
  - `API Usage`
    - `Introduction`
    - `Authentication`
    - `Integration flow`
    - `Statuses and errors`
    - `Limits`
  - `Widget`
    - `Coming soon`
- **API Reference**
  - `Introduction`
  - `Asset`
  - `Address`
  - `Quote`
  - `Swap`
  - `Swap status`
- **Support**
  - `Support`

## Page roles and content boundaries

### Overview

#### Introduction

This is the site home page.

It should:

- explain what LightSwap partners is
- explain what partners can build today
- link to API Usage, Fee sharing, Widget, and Support
- feel like a hub page, not like API docs

This page should reuse the existing `index.mdx` path and be rewritten for the new role.

#### Fee sharing

This page should:

- explain revenue sharing / commission at a high level only
- explain what partners generally earn from in principle
- explain that exact terms are handled through LightSwap directly

This page must stay commercial and simple.

It must not document internal fee mechanics, exact commercial terms, internal admin setup, or implementation details.

### Integrations

#### API Usage → Introduction

This is the main entry page for engineers.

It should:

- explain the API integration path at a practical level
- summarize the minimum backend integration flow
- route readers into auth, integration flow, statuses/errors, limits, and API Reference

This page should merge the current API overview and quick-start intent into one clearer entry page.

#### API Usage → Authentication

Covers:

- `x-api-key`
- request IDs
- rate limits
- key safety

#### API Usage → Integration flow

Covers:

- asset discovery
- address validation
- quote creation
- swap creation
- deposit detail usage
- polling
- idempotency
- quote expiry
- amount-string handling
- memo limitation

#### API Usage → Statuses and errors

Covers:

- public status meanings
- terminal states
- shared error format
- common operational troubleshooting guidance

#### API Usage → Limits

Covers MVP boundaries and what is not supported yet.

#### Widget → Coming soon

This page should exist and be visible in navigation.

It should:

- confirm widget integration is planned
- state clearly that it is not live yet
- route interested partners to Support

It must stay shallow and honest.

### API Reference

This section stays technical and OpenAPI-backed.

It should:

- keep the current endpoint-reference model
- stay separate from partner-program explanation
- avoid broad conceptual or commercial content

The introduction page should briefly explain auth and error shape, then route into endpoint pages.

### Support

This remains a single page.

It should:

- explain how partners should contact support
- distinguish transaction-help context from integration-help context in wording
- tell readers what identifiers to include:
  - swap ID
  - request ID
  - external ID
  - deposit transaction hash when relevant

## Duplication rules

To keep the site scalable:

- **Overview** must not repeat endpoint-level detail.
- **API Usage** must not reproduce full API reference tables.
- **API Reference** must not carry broad partner-program explanation.
- **Fee sharing** must not drift into implementation or admin detail.
- **Support** must stay practical and operational.

## Content style rules

Keep the existing public-doc boundaries:

- partner-facing
- no provider names
- no internal DB/admin details
- no raw key generation instructions
- no unavailable features presented as live
- no zero-fee claims

Additional style direction for this restructure:

- use second person and concise sentences
- prefer hub-and-routing pages over dense long-form pages
- keep labels concrete and helpful
- prefer “what you can build,” “how it works,” and “where to start” framing over internal product terminology

## Recommended content improvements from competitor analysis

Borrow these patterns:

- from **Xgram**: simple, easy-to-follow usage flow structure
- from **Changelly**: clear separation between conceptual/usage docs and endpoint reference
- from **SimpleSwap**: better partner-business framing around API usage
- from **ChangeNOW**: product-family framing that makes multiple integration surfaces feel coherent
- from **LetsExchange**: strong status/transaction-reference style for later evolution
- from **Houdini**: focused troubleshooting and status guidance

Apply these selectively.

Do not copy their site breadth or expand beyond today’s live LightSwap scope.

## Migration strategy

Treat this as a restructure, not a from-scratch rewrite.

### Keep and repurpose

- rewrite `index.mdx` into the new site-home `Overview → Introduction`
- preserve and relocate the current API usage pages under `Integrations → API Usage`
- preserve the OpenAPI-backed endpoint reference under `API Reference`

### Add

- a real `Fee sharing` page
- a real `Widget → Coming soon` page
- a real `Support` page
- updated site-level framing in:
  - `docs.json`
  - `README.md`
  - `AGENTS.md`

### Rewrite or remove

- placeholder pages that no longer have a role
- duplicate or awkward introductory layers created by the previous partial restructure

## Acceptance criteria

The restructure is successful if:

1. The site reads as **LightSwap partners**, not as API docs with extra tabs.
2. The home page clearly explains:
   - what LightSwap partners is
   - what is live today
   - where fee sharing is described
   - where support lives
3. A developer can quickly find:
   - API Usage
   - Authentication
   - Integration flow
   - Statuses and errors
   - Limits
   - API Reference
4. Widget is visible as future direction, but clearly not live.
5. The sidebar remains short, clear, and extendable.
6. There are no empty placeholder pages left in navigation.
7. There is no stale site-level framing that still positions the project as only “Partner API docs.”

## Validation checklist for implementation

After implementation, verify:

- Mintlify navigation feels coherent in local preview
- page titles and descriptions match the new IA
- links are not broken
- no placeholder pages remain in nav
- no provider/internal/admin language is introduced
- API reference remains intact and reachable
- widget page clearly says coming soon

## Defaults chosen

- one-tab site
- no top nav menu
- conservative sidebar structure, not the deeper future-ready version
- `API Usage` as the integration label
- `Overview` with only:
  - `Introduction`
  - `Fee sharing`
- `Support` remains a single page
- `index.mdx` is reused as the site home and rewritten
