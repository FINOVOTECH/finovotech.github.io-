---
layout: post
title: "MFD SDK: embed mutual funds into your existing app"
date: 2026-05-02
permalink: /blog/mfd-sdk-embed-mutual-funds/
canonical_url: https://finovo.tech/blog/mfd-sdk-embed-mutual-funds
description: "If you're a broker, NBFC, or fintech with an existing customer app, MFD SDK lets you ship a complete mutual-fund experience without the overhead of running a se"
image: "https://amplify-d3sdrn3vxts2f-main-b-aiimagebucketf893b34d-j21epbs6beu4.s3.ap-south-1.amazonaws.com/media/ai-generated/2026-05-04/cfe7654c-307c-402c-81d5-ded69b72cc9e.png"
tags: ["mfd", "sdk", "mutual-funds", "embed"]
---

> **Originally published at [finovo.tech/blog/mfd-sdk-embed-mutual-funds](https://finovo.tech/blog/mfd-sdk-embed-mutual-funds)** — the canonical version has the latest updates.

Most fintechs that run a customer-facing app already have engagement, KYC, and a payment integration. What they lack is a mutual-fund experience inside the app — and building one from scratch is 6-9 engineering months for the regulator-aware parts alone.

[MFD SDK](/services#mfd-sdk) is a drop-in module: React for web apps, native for iOS / Android. You ship it inside your existing app shell. Customers see one continuous experience.

## What's in the box

The SDK includes:

- Fund discovery (search, filter, compare)
- Fund details page with NAV history, holdings, fact-sheet
- SIP / SWP / lump-sum setup flows
- Transaction history with statement generation
- Mandate management (e-NACH, UPI mandate)
- Withdrawal / switch / pause flows
- Tax statement (capital gains report)
- KYC re-check (uses your existing KYC if compatible)

Each component is independently themeable to match your app's design system.

## What stays your problem

The SDK does the regulated parts. You still own:

- The app shell + navigation
- The customer's login / authentication
- The push notifications (we publish events for you to subscribe to)
- The marketing surfaces ("Top 5 SIPs this month", etc.)
- Customer support routing

This separation is intentional. We don't want to be in the way of your product team. We just don't want you to rebuild BSE StAR integration.

## How the SDK is shipped

For web: a React component library, distributed as `@finovo/mfd-sdk`. Initialise with your API key:

```js
import { MfdProvider, FundList, SipFlow } from '@finovo/mfd-sdk';

<MfdProvider apiKey={key} customerId={customer.id} theme={appTheme}>
  <FundList />
</MfdProvider>
```

Routes are component-based; you wire them into your existing router.

For iOS: a Swift package. For Android: a Maven dependency. Same shape — initialise, drop in components, theme.

## Customer KYC

If your customers have completed KYC in your app, you pass us the KYC packet (we accept the SEBI-standard CKYC schema). We use it to onboard the customer with the AMCs without re-collecting.

If your customers haven't done KYC yet, the SDK can run our standard eKYC flow inline — same flow as our standalone product, but inside your app.

## Fund universe

We integrate with all major Indian AMCs via BSE StAR. The fund universe is whatever your AMC arrangements allow:

- All AMCs (most common): full universe
- Selected AMCs: only the ones you've signed a MoU with
- Custom universe: specific schemes only (some private banks do this)

Configurable in the dashboard, no SDK code change.

## Compliance posture

The SDK is itself a SEBI-registered product. Customers transacting via it are transacting on Finovo's MFD ARN by default — your app is the surface, we're the regulated entity behind it.

If you have your own ARN, we can configure the SDK to transact under your ARN instead. This is the "white-label" mode. Different commercials.

## Performance

The full SDK is ~80KB gzipped (React version), ~450KB Swift framework, ~600KB AAR. Lazy-loaded by default — fund-discovery code doesn't load until the customer opens the MF section.

## What customers tell us

The most-quoted reason fintechs pick the SDK over building from scratch:

> "We had 4 engineers ready to build mutual funds for 6 months. With the SDK, we shipped in 6 weeks with 1 engineer. The 4 engineers built the things only we could build."

We don't try to be a platform; we try to be the most boring, well-tested commodity in the stack.

## Pricing

Per-AUM platform fee + per-transaction. Lower than per-customer pricing because we don't cost per dormant customer. Typically priced as a percentage of revenue you're earning, so the SDK pays for itself out of revenue.

## Who shouldn't use it

If you're greenfield with no existing app and no existing customer base, just use [MFD vanilla](/services#mfd-vanilla) — same features, full app, zero engineering work. The SDK is for when you already have a surface.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
