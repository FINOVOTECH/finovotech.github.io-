---
layout: post
title: "eKYC with SSO: KYC once, use everywhere across India's financial industry"
date: 2026-05-02
permalink: /blog/ekyc-with-sso-kyc-once/
canonical_url: https://finovo.tech/blog/ekyc-with-sso-kyc-once
description: "Aadhaar-XML-share and CKYC are the regulator-blessed paths for KYC reuse. The customer experience of using them is still terrible. eKYC SSO is a cross-broker SS"
tags: ["ekyc", "sso", "ckyc", "interoperability"]
---

> **Originally published at [finovo.tech/blog/ekyc-with-sso-kyc-once](https://finovo.tech/blog/ekyc-with-sso-kyc-once)** — the canonical version has the latest updates.

Every Indian financial customer goes through KYC at least 5 times in their life — at their first broker, at their bank, at their MF distributor, at their first insurance policy, at their loan provider. Each one is the same regulatory questionnaire and the same documents.

CKYC (Central KYC Records Registry) was supposed to fix this. In practice, CKYC retrieval is slow, the data quality varies, and the customer-side experience is "give us your CKYC number" — most customers don't know what their CKYC number is.

[eKYC with SSO](/services#ekyc-sso) is a cross-Finovo-client KYC sharing layer that makes reuse feel like one click.

## How it works

A customer who's already KYC'd at Finovo Client A wants to open an account at Finovo Client B. Instead of redoing KYC:

1. Customer reaches B's onboarding flow.
2. The flow asks: "Are you KYC'd anywhere already? (Reuse with one click)"
3. Customer clicks "Yes, I have a Finovo SSO account."
4. They authorise B to receive their KYC packet from A (one tap, OAuth-style consent).
5. A's verified KYC packet (PAN, Aadhaar, video PD, address proof) is shared with B.
6. B's onboarding completes in 30 seconds — no re-collection.

It's the OAuth pattern applied to KYC.

## What's actually shared

The customer authorises B to receive specific fields:

- Identity: name, DOB, gender, photo (from Aadhaar)
- Address (current + permanent)
- PAN (verified)
- Father's name (for some categories)
- Phone + email
- Risk-cat answers

What's NOT shared:

- The customer's transaction history at A
- The customer's portfolio at A
- A's internal compliance notes about the customer

This is enforced server-side. B only ever sees what the customer explicitly authorised.

## Compliance posture

Each Finovo client is independently SEBI / RBI / IRDAI registered. CKYC sharing has explicit regulator support:

- SEBI Master Circular on KYC norms permits CKYC reuse
- RBI guidelines on KYC reuse for NBFCs
- IRDAI permits CKYC reuse for life insurance

eKYC SSO uses CKYC under the hood for cross-institution data sharing — but layered with a better customer-facing UX. The SSO layer is just consent capture + transport; the underlying KYC packet is the regulator-approved CKYC packet.

## CKYC fallback

If the customer has done KYC at a non-Finovo institution (which is most cases), the flow falls back to standard CKYC retrieval:

- Customer enters PAN / Aadhaar
- We look up CKYC by ID
- If found, the CKYC packet is presented to the customer for review + consent
- If they consent, the packet is used at B

CKYC retrieval has a 48-72h regulator-side latency for fresh records; for already-existing records it's near-instant.

## What customers experience

A customer onboarding at their second Finovo-client institution:

> Step 1: Email + phone verification (15s)
> Step 2: "We notice you're already KYC-cleared at [other client]. Reuse?" Yes (5s)
> Step 3: One-click consent screen, customer reviews fields shared (10s)
> Step 4: Account active (instant)

Total time: ~30 seconds. Customers are surprised — most expect 4 minutes of re-KYC.

## What it doesn't do

- Doesn't replace primary KYC for fresh customers (still need the standard flow)
- Doesn't share trade or transaction data (which would be privacy-violating without explicit consent)
- Doesn't auto-port a customer from A to B; the customer still has separate accounts
- Doesn't require A and B to be commercially aligned — A doesn't get a referral fee for B's customer

## Network effect

The more institutions on the SSO network, the more customers experience one-click reuse. We're building the network: each new Finovo client is a node, and customers benefit increasingly as the network grows.

This is the kind of infrastructure play that takes years. We're a few years in. ~50 institutions on the network as of writing; coverage of about 40% of new retail customer KYCs.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
