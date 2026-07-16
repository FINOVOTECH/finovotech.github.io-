---
layout: post
title: "E-IPO Integration: from bidding to allotment tracking"
date: 2026-05-02
permalink: /blog/e-ipo-integration/
canonical_url: https://finovo.tech/blog/e-ipo-integration
description: "IPO bidding for retail customers used to mean printed forms. Today every broker offers some version of E-IPO; here's what a robust integration looks like."
image: "https://amplify-d3sdrn3vxts2f-main-b-aiimagebucketf893b34d-j21epbs6beu4.s3.ap-south-1.amazonaws.com/media/ai-generated/2026-05-04/50b3960c-b180-4e39-bf8b-e01ef11abfa8.png"
tags: ["ipo", "nse", "bse", "asba"]
---

> **Originally published at [finovo.tech/blog/e-ipo-integration](https://finovo.tech/blog/e-ipo-integration)** — the canonical version has the latest updates.

Indian retail IPO bidding moved fully digital with the SEBI ASBA mandate. Every broker has to offer customers some way to bid; the spread of quality is huge.

[E-IPO Integration](/services#eipo) is Finovo's bidding + allotment + tracking module that handles both NSE and BSE in one customer-facing flow.

## The IPO bidding lifecycle

For each IPO that opens, the broker has to:

1. Display the IPO to the customer (subscription period, price band, lot size, terms)
2. Take the customer's bid: shares + price + ASBA bank
3. Submit the bid to the exchange (NSE or BSE, sometimes both)
4. Reflect the locked-in funds in the customer's bank
5. Wait for allotment (usually 5-7 days)
6. Notify the customer of allotment outcome
7. Reflect allotted shares in the demat
8. Refund un-allotted portion to the customer's bank

Each step has its own SEBI / RBI / exchange compliance overlay. Most broker-side bugs we see are at step 5 or 8 — the funds-tracking part — because brokers underestimated how messy ASBA reconciliation gets.

## Why NSE + BSE both matter

Some IPOs are listed only on one exchange. Others are dual-listed. The retail customer doesn't care which; they just want to bid. The broker has to abstract the dual-API and present a single bid form to the customer.

NSE's E-IPO API and BSE's E-IPO API have different:

- Bid submission payloads
- Status polling cadence
- Allotment file formats
- Refund file formats

Wrapping both into a unified "broker-facing" API is what the integration does.

## ASBA mechanics

ASBA (Application Supported by Blocked Amount) is a SEBI mandate that bids must lock the bid funds in the customer's bank account, not transfer them out. The bank releases the locked funds:

- For allotted shares: transfers to the IPO issuer's account
- For un-allotted shares: releases the lock back to the customer

The broker's role is to construct the right payload to the customer's bank's ASBA system. UPI-based ASBA is the modern default; for customers without a UPI ID, the older bank-portal-based ASBA still works but takes more steps.

## Bid validation

Before submitting to the exchange, the bid is validated:

- Lot size: bid must be a whole multiple of the IPO's lot size
- Price band: bid price must be within the IPO's price band
- Customer eligibility: not a related party, not a director of the issuer, etc.
- Funds availability: the customer's bank must support the locked amount
- Customer category: retail vs HNI — different lots, different rules

Caught early, these prevent exchange-side rejections (which embarrass the broker because the customer thinks they bid successfully).

## Allotment tracking

Once the IPO closes, the issuer publishes a basis-of-allotment document. It maps applied lots → allotted lots per category. Brokers receive this from the registrar and must:

- Match against the customer's PAN
- Notify the customer of allotment / non-allotment / partial
- Reflect allotted shares in the customer's demat (DP)
- Reflect the refund (release of locked funds) in the customer's bank
- Generate the customer-facing allotment letter (PDF, downloadable)

Doing this manually for a popular IPO with 10K+ subscribers is a 2-day exercise per IPO. Automated, it's a 30-minute job.

## Customer notifications

The broker should send three notifications per IPO:

1. **Bid confirmation**: as soon as the exchange accepts (typically a few seconds)
2. **Allotment update**: the day allotment is announced
3. **Refund confirmation**: when the un-allotted lock is released (usually the same day, sometimes next day)

We send these via SMS + WhatsApp + push notification. Customers expect WhatsApp; they react when bid status changes via WhatsApp; they ignore email.

## Common gotchas

- Customers bid at the cut-off price thinking it's the upper-band; it's actually a special "I'll take whatever the final price is" indicator. Frame the UI carefully.
- Some HNI customers want to bid via a corporate account (HUF, PVT, etc.) — these have different ASBA paths.
- "Anchor allocations" happen 1 day before the public IPO opens; some brokers offer their HNI customers participation. Different flow entirely.
- Withdrawn IPOs (rare but happen): the broker has to tell every bidder, refund the lock, and not crash.

## Pricing

E-IPO is priced per active IPO, not per bid. Brokers pay a flat per-IPO platform fee + a small per-bid marginal cost. For a typical broker with 50K bids per IPO, this works out to a fraction of the customer-facing brokerage fee on a successful allotment.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
