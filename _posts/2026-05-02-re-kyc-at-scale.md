---
layout: post
title: "Re-KYC at scale: SEBI 6-month compliance, automated"
date: 2026-05-02
permalink: /blog/re-kyc-at-scale/
canonical_url: https://finovo.tech/blog/re-kyc-at-scale
description: "SEBI mandates 6-month re-KYC for high-risk customers and 2-year for everyone else. The cost of doing this manually is brutal. This is what an automated re-KYC p"
tags: ["rekyc", "sebi", "compliance", "automation"]
---

> **Originally published at [finovo.tech/blog/re-kyc-at-scale](https://finovo.tech/blog/re-kyc-at-scale)** — the canonical version has the latest updates.

If you run more than 100,000 customers, the SEBI re-KYC mandate isn't a project — it's a constant grind. High-risk customers need re-verification every 6 months; everyone else, every 2 years. Manual ops teams burn out. Customer experience suffers (a customer-favorite question to support: "why are you asking me for KYC again?"). And the regulator audits your audit trail.

The fix is to treat re-KYC as a calendar-driven automated pipeline, with manual review only for the cases that fail.

## The architecture

A re-KYC pipeline has three layers:

1. **Calendar engine** — for every customer, computes the next-due date based on risk category, last-completed date, and product. Fires a Lambda when due.
2. **Re-KYC orchestrator** — the actual customer-facing flow. Tries the cheapest verification first (OTP + recent transaction confirmation), escalates to OVD upload + video PD only when needed.
3. **Reconciliation** — once daily, reads the regulator's CKYC database and compares against our snapshot. Surfaces any drifts (address change, PAN deactivation, etc.) for manual review.

## Why "OTP-first"

The cheapest valid re-KYC for a low-risk customer is just an Aadhaar OTP — 12 seconds, no friction. SEBI accepts this for routine refresh as long as the customer's category hasn't changed. Most re-KYC fails get triggered because the broker over-engineered the flow and asked for full document re-upload, even though the rules don't require it.

Smart escalation:

- **Tier 1**: OTP + recent transaction confirmation (90% of cases)
- **Tier 2**: PAN re-OCR if the PAN looks aged or low-confidence (8% of cases)
- **Tier 3**: Full video PD if any field has changed materially (2% of cases)

Most pipelines we've audited do Tier 3 for everyone, which is why their completion rates are at 30%.

## The "address change" trap

A common surprise: a customer who moved to a different city since their last KYC might pass OTP fine, but their address proof is now stale. SEBI doesn't auto-detect this; you have to ask. Best UX is a single-question pre-check: "Is your communication address still 4 / Park Street, Kolkata?" Yes → continue. No → trigger Tier 3.

We see ~3% of customers report address change at re-KYC. That sounds small until you realize at 1M customers you're looking at 30,000 forced Tier-3 flows that someone has to handle.

## Audit trail

The regulator audits not the customer's data but **how you got it**. Every re-KYC step needs:

- Timestamp
- IP + device fingerprint
- The actual question asked (so you can prove you didn't lead the customer)
- The customer's literal answer
- The system's classification (auto-pass / auto-fail / review-required)
- The reviewer (if manual)

A typical re-KYC packet has 40-60 logged events. Storage is cheap; failing the audit isn't.

## What you avoid by automating

A 500K-customer broker doing manual re-KYC typically spends:

- 12-20 ops people full-time on the queue
- 6-8 weeks each cycle to clear the high-risk list
- 8-15% of customers in inactive-pending-rekyc status at any time (lost trading volume)
- 2-4 SEBI observation letters per year about specific customers

After automation:

- 2-3 ops people for review-only queue
- The full high-risk list closes within 3 days of the due-date
- <1% of customers in pending-rekyc status
- No observation letters about systematic delay (specific-case ones still happen, but those are unrelated to volume)

For a deeper dive, see our [what is sebi re kyc](https://finovo.tech/glossary/sebi-re-kyc).

## The integration

This is the [re-KYC product](/services#rekyc). It integrates with whatever broker / NBFC / insurer system you already have via standard webhooks — calendar engine queries your CRM, results write back to it. We don't replace your CRM; we add the automation layer between it and the regulator-facing KYC pipes.

If you're spending more than 4 ops-FTE-equivalents on re-KYC right now, the math probably already works.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
