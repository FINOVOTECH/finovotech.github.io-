---
layout: post
title: "Why brokers, NBFCs and insurers need a unified onboarding stack"
date: 2026-05-02
permalink: /blog/unified-onboarding-stack/
canonical_url: https://finovo.tech/blog/unified-onboarding-stack
description: "Indian financial customers increasingly hold accounts across categories — broker + MFD + NBFC + insurance. A unified onboarding stack makes the cross-sell work;"
image: "https://amplify-d3sdrn3vxts2f-main-b-aiimagebucketf893b34d-j21epbs6beu4.s3.ap-south-1.amazonaws.com/media/ai-generated/2026-05-04/621c2c04-eb01-4967-a8de-3af1c6aff560.png"
tags: ["unified", "cross-sell", "architecture"]
---

> **Originally published at [finovo.tech/blog/unified-onboarding-stack](https://finovo.tech/blog/unified-onboarding-stack)** — the canonical version has the latest updates.

Most Indian financial customers under 35 hold accounts in 3+ categories: a broker for stocks, an MFD for mutual funds, a bank for NBFC products, an insurer. These were historically four separate operations with separate KYC, separate apps, separate logins.

The customer never asked for it that way. They just want their money to work for them.

A unified onboarding stack — same KYC, same identity, shared customer record across categories — is the foundation for actually serving that customer. Here's what changes when you have it.

## The cross-sell math

A broker who's also an MFD distributes mutual funds to a fraction of their broking customers. The fraction depends mostly on onboarding friction:

- If MFD onboarding is a separate app + separate KYC: 8-12% conversion
- If MFD onboarding is the same app + reused KYC: 35-50% conversion
- If MFD products are shown in-context within the broking app: 60-80% conversion

The difference isn't marketing genius. It's onboarding architecture.

## The unified stack

A unified stack has, at minimum:

- **One customer record**: a customer ID that's the same across broker + MFD + NBFC + insurance product lines, with KYC linked to the ID, not duplicated per product.
- **One KYC pipeline**: the customer goes through KYC once; the resulting CKYC packet is reused for any new product they want to enable.
- **One audit trail**: regulator audits target a specific category, but the audit data lives in one structured store, queryable per category.
- **Per-category compliance overlays**: each regulator's specific rules apply per-product without forcing the customer to re-do anything.
- **One unified consent layer**: customer consents per-product but their consent state is managed in one place.

## What it's NOT

A unified stack isn't:

- A single regulator (still SEBI for broking, RBI for NBFC, IRDAI for insurance — three regulators, one customer)
- A single product (still distinct trading account, distinct loan account, distinct policy)
- Cross-product transaction visibility without consent (privacy boundaries are real)
- A merger of legal entities (the broker, MFD, NBFC, insurer are still separately licensed)

The stack is the operational layer beneath the regulated entities, not a replacement for them.

## What it enables

Practical capabilities:

- A customer who's KYC-cleared at the broker can open an MFD account in 30 seconds (no re-KYC)
- A customer who's borrowing against shares (LAS) at the NBFC can have their position visible to the broker who issued the shares
- An insurance customer can buy term insurance with KYC reused from their broker (with explicit consent)
- The customer-success team sees the customer's full footprint when they call about any one product

## What we ship

Finovo's stack is unified at the technical level. The same KYC pipeline serves brokers, NBFCs, and insurers. Customer records are unified. Audit trails are unified.

That said: not every Finovo client uses all the categories. Most are single-category (just broking, or just MFD). Some are dual (broking + MFD). Few are full-stack (broking + NBFC + insurance + MFD).

The unified-stack benefit is realised gradually as a client expands their product surface. A broker that's ALSO becoming an MFD distributor gets the cross-sell win immediately. A pure broker doesn't see the unified-stack benefit until they expand.

## What it doesn't fix

Unified onboarding isn't a magic bullet:

- Bad customer-experience inside any one product still hurts cross-sell. If your broker app crashes, customers won't trust your MFD pitch.
- Regulator-side complications still exist. Some products require physical signatures; some require specific category-only flows. Unified stack reduces friction but doesn't eliminate it.
- Customer mistrust around data sharing is real. Even with consent screens, some customers don't want their broker to know about their loan.

## The infrastructure investment

Building a unified onboarding stack from scratch in-house: 3-5 years and a 15-25 person team. Most fintechs don't have that time horizon.

Buying it: ~3-6 month integration with a vendor like Finovo, depending on which categories you're starting in.

The real value is when you cross product categories. If you're only ever going to be a single-category business, a unified stack is over-engineered for you. If you'll be in 2+ categories within 24 months, the unified stack saves you the integration tax of running parallel onboarding pipes.

## Final thought

The customer's mental model is "I have one financial life." The industry's mental model is "you have one account per product per regulator." Closing that gap is what unified onboarding does. Done well, the customer barely notices the underlying complexity. Done poorly, every cross-product interaction reminds them.

Whether you build it or buy it, build for the customer's mental model. They'll thank you with their AUM.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
