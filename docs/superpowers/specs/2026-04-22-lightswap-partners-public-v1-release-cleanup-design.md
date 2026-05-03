---
title: "LightSwap Partners public v1 docs cleanup design"
date: "2026-04-22"
status: "proposed"
---

# LightSwap Partners public v1 docs cleanup design

## Summary

This spec defines a docs-only cleanup pass for the public LightSwap Partners Mintlify site in `/Users/rolaman/IdeaProjects/lightswap-docs`.

The goal is to move the docs from "technically good but operationally fuzzy" to a strong public v1:

- clear enough for first-time partners
- honest about what is live
- consistent about business contact vs operational support
- useful for both business readers and engineers

This pass does not change the app, the support form, or the Partner API contract. It only improves the public documentation and release readiness of the current docs site.

## Current state

The docs already have a solid foundation:

- a clean partner-facing information architecture
- a usable Direct API section
- a real OpenAPI-backed API Reference
- a high-level fee-sharing page
- a placeholder widget section
- a public support page

The remaining release issues are not about the basic docs structure. They are about routing, partner usefulness, and public accuracy:

1. partner/business contact is mixed with generic support
2. API access is not explicitly explained
3. the support guidance implies a more partner-aware support intake than the actual site provides
4. the widget card uses a broken icon
5. `externalId` is not yet centered strongly enough as the main partner-facing identifier
6. `x-request-id` is more prominent in public docs than desired for this v1

## Decisions locked from brainstorming

These decisions were explicitly chosen and should be treated as fixed for this pass:

- Optimize for **strong public v1 docs**
- Split contact by intent
- Use **one partner email** for all partner-side contact
- Use **email-first** for partner/business/onboarding/widget/API access questions
- Keep `/support` only for swap issues and existing integration help
- Make **`externalId`** the primary partner-facing support reference
- Treat `x-request-id` cleanup as a **later contract cleanup task**
- Treat the fee-sharing range and partner email as **confirmed public policy**
- Add API access guidance **inside `Integrations -> Direct API -> Introduction`**
- Keep Widget visible as **coming soon**, but route it to partner email
- Fix the broken widget icon now
- Keep this pass **docs-only**, with no app repo implementation changes

## Goals

This pass should make the docs answer these questions clearly:

- What can I integrate today?
- How do I get access to the API?
- Where do I send business or onboarding questions?
- Where do I send widget-interest questions?
- What identifier should I store and share if I need help?
- When should I use `/support`, and when should I use partner email?

## Non-goals

This pass does not attempt to build a complete partner portal or restructure the app-side support system.

Out of scope:

- app support form changes
- support page backend changes
- `x-request-id` API contract changes
- dashboard or onboarding workflow
- sandbox environment documentation
- widget product design or widget API contract
- webhook docs

## Target public v1 contact model

### Partner email

Partner email is the primary path for:

- API access
- onboarding
- fee-sharing discussions
- widget interest
- general partner/business questions

The public docs should treat this as the normal path for starting or growing a partner relationship.

### Support route

`/support` remains the operational help path for:

- specific swap issues
- existing integration issues
- cases where a partner already has a working integration and needs help with an actual flow or real transaction

The docs should stop implying that `/support` is the right place for commercial, onboarding, or widget interest.

## Identifier strategy for public docs

### Primary identifier

`externalId` becomes the primary partner-facing identifier.

The docs should advise partners to:

- always set `externalId` on quote creation
- store it in their own order system
- use it as the first reference when asking for help

### Secondary identifier

Once a swap exists, the LightSwap swap ID is also useful and should be shared when available.

### Deferred identifier

`x-request-id` should stop being emphasized in partner-facing narrative docs. Full contract cleanup is deferred to a later implementation pass, so the strict API reference can remain accurate for now.

## Content changes

### 1. Home page

Update the home page so that its routing language matches the public v1 support model.

Changes:

- keep `Fee sharing` as the business/commercial route
- keep `Widget` visible as coming soon
- make sure `Support` reads as operational help, not onboarding
- replace the broken widget icon with a Mintlify-supported icon

The page should remain a partner hub, but it should no longer blur business contact and support.

### 2. Direct API introduction

This page becomes the primary place to answer:

- how the API works
- how a new partner starts

Add a short "How to get access" section that:

- explains that access is enabled through the LightSwap partner team
- tells readers to contact the partner email
- tells them what to send at a high level, such as their product, intended integration, and rollout goals

This page should also start operationally prioritizing `externalId` so engineers treat it as required partner context even if the raw request technically allows omission.

### 3. Authentication

Keep:

- `x-api-key`
- backend-only guidance
- rate limiting
- `externalId` and `metadata`

Change:

- reduce or remove public narrative emphasis on `x-request-id`
- make `externalId` and metadata more clearly useful for partner support and order attribution

The technical truth of the current contract can remain in the API Reference/OpenAPI until a later cleanup.

### 4. Support page

Reframe the support page so it matches the current actual support surface.

The page should clearly say:

- use this for swap issues and existing integration help
- do not use it as the primary route for API access, widget interest, or commercial discussions

The page should recommend including:

- `externalId` first
- LightSwap swap ID if available
- deposit transaction hash when relevant

Because the current support form is generic, the wording should not imply a dedicated partner intake with structured fields for API-specific context.

### 5. Widget coming soon

Keep the page visible and honest.

Change the CTA so widget-interest traffic goes to partner email, not `/support`.

The page should position widget as planned, not live, and route readers into the right business contact path.

### 6. Fee sharing

Keep the current public policy:

- partner email stays public
- the `0.5%` to `2%` range stays

Do not add more commercial detail in this pass.

### 7. API Reference

The API Reference remains the strict contract surface and should stay accurate to the current implementation.

For this pass:

- do not redesign the OpenAPI contract
- do not remove `x-request-id` from the strict reference if it is still part of the real API
- keep the current endpoint reference structure intact

The cleanup here is narrative, not contract-level.

## Proposed file-level changes

### Files to update

- `index.mdx`
- `integrations/direct-api/introduction.mdx`
- `integrations/direct-api/authentication.mdx`
- `integrations/direct-api/statuses-errors.mdx`
- `support.mdx`
- `integrations/widget/coming-soon.mdx`

### Files that may need light wording alignment

- `integrations/direct-api/limits.mdx`
- `api-reference/introduction.mdx`

### Files expected to stay substantially unchanged

- `fee-sharing.mdx`
- `api-reference/openapi.json`
- endpoint wrapper files under `api-reference/`

## Release-readiness policy for this pass

### Fix now

- broken widget icon
- unclear API access path
- wrong routing of widget/business traffic into `/support`
- support-page wording that overpromises partner-specific support intake
- weak emphasis on `externalId`

### Keep, but frame carefully

- fee-sharing range
- partner email
- strict API contract facts that are still technically true today

### Defer

- app-side support form alignment
- full `x-request-id` contract cleanup
- sandbox/onboarding/dashboard/product-surface expansion

## Acceptance criteria

This pass is successful if:

1. A new partner can understand:
   - what is live now
   - how to request API access
   - where to send partner/business questions
   - where to send widget-interest questions
   - where to go for swap or existing-integration help

2. The docs consistently treat:
   - `externalId` as the main partner-side identifier
   - swap ID as secondary operational context
   - `/support` as operational help rather than business contact

3. The docs no longer route widget or onboarding traffic into the generic support route.

4. The broken widget icon is replaced with a supported one.

5. The docs remain accurate enough with the current live API contract.

6. Mintlify validation and broken-links checks pass after the content changes.

## Validation plan after implementation

After implementation, verify:

- `mint validate`
- `mint broken-links`
- local preview of:
  - home page
  - Direct API introduction
  - Widget coming soon
  - Support
  - Fee sharing
- widget/home icon renders without remote asset failures
- navigation and CTA links route correctly
- public docs no longer operationally center `x-request-id`

## Risks

### Risk: docs drift from actual support surface

Mitigation:

- keep this pass docs-only
- make wording match the current generic support experience
- avoid promising partner-specific support intake

### Risk: public docs hide too much contract detail

Mitigation:

- keep strict API details in API Reference/OpenAPI
- only simplify public narrative pages

### Risk: partner readers still do not know how to start

Mitigation:

- make API access guidance explicit in `Direct API -> Introduction`
- route business/onboarding/widget questions to the partner email from multiple points

## Result after this pass

If implemented as designed, the docs should be ready for a strong public v1 release:

- business readers get a clear contact path
- engineers get a clear integration and access path
- support guidance becomes honest and usable
- the docs stay lean and do not overbuild ahead of the product
