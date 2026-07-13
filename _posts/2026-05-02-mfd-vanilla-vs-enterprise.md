---
layout: post
title: "MFD platforms: vanilla vs enterprise (which one fits)"
date: 2026-05-02
permalink: /blog/mfd-vanilla-vs-enterprise/
canonical_url: https://finovo.tech/blog/mfd-vanilla-vs-enterprise
description: "A 1-ARN MFD running solo doesn't need the same platform as a 200-ARN distributor with a sub-ARN hierarchy. We've packaged the differences explicitly."
tags: ["mfd", "mutual-funds", "distribution"]
---

> **Originally published at [finovo.tech/blog/mfd-vanilla-vs-enterprise](https://finovo.tech/blog/mfd-vanilla-vs-enterprise)** — the canonical version has the latest updates.

India has 250,000+ registered MFDs (Mutual Fund Distributors). They range from a single CFP working from home to large national distributors with hundreds of sub-ARNs. The platform a 1-ARN MFD needs is fundamentally different from what a 200-ARN distributor needs — and trying to use one for the other ends in tears.

## When to pick MFD vanilla

[MFD vanilla](/services#mfd-vanilla) fits if:

- You're a single ARN (one license, one MFD)
- &lt; 2,000 customers
- You're fine with a Finovo-branded customer app (or your customers don't notice / care)
- You don't have sub-distributors under you
- Pricing pressure is on per-AUM cost, not feature surface

The vanilla product gives you BSE StAR Connect (transactions), customer self-signup for SIPs / SWPs / switches, an iOS + Android app the customer downloads, statement-on-demand, and the full KYC + re-KYC pipe.

It onboards in about a week. You log in, configure your name and ARN, customers can sign up the next day.

## When to pick MFD enterprise

[MFD enterprise](/services#mfd-enterprise) fits if:

- You have multiple ARNs (or sub-distributors)
- You want a custom-branded app on your domain (App Store + Play Store under your developer account)
- You have a hierarchy: master distributor → regional → individual ARN
- You need per-distributor commission splits
- You have your own RM team that needs a desktop dashboard
- &gt; 5,000 customers, or you'll be there within 6 months

Enterprise gives you the full vanilla feature set plus:

- White-label: your logo, your domain, your design tokens, your push-notification certs
- Sub-ARN hierarchy: every customer is tagged to the ARN that brought them in; commissions split automatically
- Per-region commission overrides (when sub-ARNs negotiate slightly different splits)
- Desktop RM dashboard (separate from the customer app)
- Custom domain mobile-app deep linking
- HRMS for your RMs (attendance, sales targets, pipeline)
- A dedicated migration engineer for the first 90 days

## The hidden cost of starting on the wrong tier

Most MFDs we work with started on a vanilla product (often a competitor's), grew past 3,000 customers, and then realized they needed sub-ARN logic — at which point they had to migrate every customer. The migration is doable but takes 6-8 weeks of disruption.

Rule of thumb: if you'll be at 5K customers within 6 months, start on enterprise. The marginal cost vs. vanilla pays for itself in the migration you didn't have to do.

## What "white-label app" really means

The most-requested feature for enterprise is the white-label mobile app. People often underestimate what's involved:

- App Store + Play Store accounts in the distributor's name (not Finovo's)
- App-store screenshots, copy, age-rating per their listing
- Apple Developer enterprise certs for code-signing
- Android upload key + Play Console permissions
- Push-notification credentials (APNs + FCM) per app
- App-tracking-transparency consent (iOS)

We handle the build pipeline, the cert management, the per-version review submission. The distributor's marketing team owns the listing copy. First app release is typically 3 weeks; subsequent updates are 2-4 days.

## What stays the same

The actual transaction engine (BSE StAR), the AMC integrations, the KYC pipe, the SEBI reporting — all the same code. You're not losing engineering quality going to vanilla; you're just choosing how much of the surrounding infrastructure to take.

## Pricing shape

- Vanilla: flat per-customer monthly + per-transaction. Cheap until you grow.
- Enterprise: platform fee + per-transaction (no per-customer). Cheaper at scale.

The breakeven for most distributors lands somewhere between 8K and 12K customers.

For a deeper dive, see our [how to become mutual fund distributor india](https://finovo.tech/guide/how-to-become-mutual-fund-distributor-india).

For a deeper dive, see our [best app for mutual fund distributor](https://finovo.tech/guide/best-app-mutual-fund-distributor-guide).

For a deeper dive, see our [how to start mutual fund distribution](https://finovo.tech/glossary/start-mutual-fund-distribution).

## Migration path

Vanilla → enterprise is a no-code migration: same backend, new app shell + admin tools provisioned. Customer accounts persist, transaction history persists, ARN tagging gets re-applied. Typical downtime: zero (the new app ships alongside the old one for 30 days; old app is force-updated to the new one).

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
