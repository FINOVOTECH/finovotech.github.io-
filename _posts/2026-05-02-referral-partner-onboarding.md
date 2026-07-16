---
layout: post
title: "Referral partner onboarding with TDS-compliant payouts"
date: 2026-05-02
permalink: /blog/referral-partner-onboarding/
canonical_url: https://finovo.tech/blog/referral-partner-onboarding
description: "Referral partners (insurance agents, finance bloggers, IFAs) bring meaningful customer volume. A referral platform that doesn't handle TDS, conversion-tracking,"
tags: ["referrals", "partnerships", "tds"]
---

> **Originally published at [finovo.tech/blog/referral-partner-onboarding](https://finovo.tech/blog/referral-partner-onboarding)** — the canonical version has the latest updates.

Referral programs are the most common growth channel for Indian financial services. A typical broker has 200-500 referral partners (insurance agents, IFAs, finance bloggers, social-media creators) who collectively bring in 15-30% of new customers. Most of these programs are run from a Google Sheet.

[Referral partner onboarding](/services#referral-onboarding) replaces the spreadsheet with a managed platform.

## What a referral program needs

The bare minimum for a program that scales past 50 partners:

- Self-serve signup (don't make every partner email you for credentials)
- A unique referral code per partner (link-based attribution)
- Real-time conversion tracking (partner can see "did my customer convert?" without asking)
- Per-tier commission rates (gold partner gets 30%; silver gets 20%, etc.)
- TDS-compliant payouts (Section 194-H for commission, 10% TDS, with quarterly TDS certificate)
- A dispute resolution path (when the partner thinks a customer was theirs and the broker disagrees)

Below this bar, you'll spend more in operations cost than you earn from the channel.

## Self-serve signup

The partner submits:

- Identity (PAN + bank account proof)
- Tax info (PAN with TDS profile, GST if applicable)
- Marketing channel (where they'll promote)
- Their target audience description

Compliance review queue handles approval. Most partners are approved within 2 working days. Approval triggers their unique referral code generation.

## Referral code mechanics

Each partner gets a code (e.g. `JOSH-FINOVO-X7`). Customers bringing this code in via:

- A direct URL: `finovo.tech/refer?ref=JOSH-FINOVO-X7`
- The customer typing it into a "referral code" field at signup

…are tagged to that partner permanently. The tag persists through the customer lifetime — so when the customer transacts a year later, the partner still gets attributed.

## Real-time conversion tracking

The partner has a dashboard showing:

- Total referrals (clicks on their code)
- Verified customers (passed KYC)
- Active customers (have transacted at least once)
- Pending payout (commission earned, not yet disbursed)
- Paid payout history

Updates in real-time. A partner can see at 11pm "I just got 3 conversions today" without emailing support.

## Tier-based commissions

The system supports multiple tiers based on:

- Customer-conversion volume (50+ this quarter = silver, 200+ = gold)
- Customer-AUM brought in
- Time-with-program tenure
- Manual override (some partners are special-cased)

Tier-up triggers automatically; the partner sees the new commission rate in their dashboard the next day.

## TDS-compliant payouts

This is where most broker-run referral programs fail compliance. Section 194-H of the Income Tax Act requires 10% TDS on commission paid to a non-employee. The deductor (broker) has to:

- Deduct TDS at the time of payout
- Deposit TDS to the IT Department by the 7th of the next month
- File quarterly TDS returns (Form 26Q)
- Issue Form 16A (TDS certificate) to the partner quarterly

Partners need Form 16A to claim the TDS credit on their own tax return. Without it, the partner pays tax twice — first via TDS, then again on their own filing because they can't claim the deduction.

The platform automates all of this. Payout calculations happen weekly / monthly per the broker's policy; TDS is computed and deducted; deposit to IT Department happens via the broker's TAN; Form 16A generates and emails to the partner each quarter.

## Dispute resolution

The most common dispute: "Customer says they signed up via my referral but I don't see them in my dashboard." Usually means:

- The customer used a different device (referral cookie didn't follow)
- The customer abandoned and re-signed up later
- The partner's code wasn't entered correctly

Each case needs a paper trail. The platform logs every click on a referral link with timestamp + IP + user-agent + cookie ID, so disputes can be checked against actual log data, not memory.

## What it replaces

A 200-partner referral program in a spreadsheet typically has:

- 30-50% of partners with stale or wrong banking details
- 5-10 disputes per month escalated to ops
- Ad-hoc TDS calculation, often missed entirely (which makes the broker liable)
- Random partner churn because they got tired of asking for updates

After the platform: 0 of those problems. Adds about 0.5 ops-FTE for review-only work.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
