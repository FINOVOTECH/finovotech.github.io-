---
layout: post
title: "PMS individual eKYC: SEBI-aligned account opening"
date: 2026-05-02
permalink: /blog/pms-individual-ekyc/
canonical_url: https://finovo.tech/blog/pms-individual-ekyc
description: "PMS investments require a 50L+ minimum and SEBI requires specific extra disclosures. PMS eKYC handles the regulatory delta from regular eKYC."
tags: ["pms", "sebi", "ekyc", "portfolio-management"]
---

> **Originally published at [finovo.tech/blog/pms-individual-ekyc](https://finovo.tech/blog/pms-individual-ekyc)** — the canonical version has the latest updates.

Portfolio Management Services (PMS) is one of SEBI's regulated investment categories — your customer is investing 50 lakh+ minimum and the portfolio manager is making active decisions on their behalf. The regulatory bar is correspondingly higher than retail KYC.

[PMS individual eKYC](/services#pms-individual) handles the regulatory delta.

## What's different from retail KYC

A standard individual KYC packet doesn't cut it for PMS. SEBI requires:

- The full retail KYC (Aadhaar / PAN / video PD)
- A SEBI-specified suitability questionnaire that the customer fills out themselves (not by the RM)
- A fee structure disclosure document signed by the customer
- A risk profiling questionnaire
- Aadhaar e-sign on the PMS agreement (not just digital signature — actual e-sign with UIDAI)
- Disclosure of any related-party transactions
- The customer's investment objective in their own words

Each is a SEBI checklist item. Missing any gets the account opened but red-flagged on the next inspection.

## The suitability questionnaire

This is the most-watched part of PMS onboarding. SEBI is explicit that the questionnaire must be:

- Filled by the customer, not the RM (you can't auto-pre-fill)
- Time-stamped with each answer
- Reviewed by the portfolio manager (logged review event)
- Re-administered on any material change in the customer's financial position

The PMS eKYC flow renders the SEBI-spec questionnaire (we maintain the latest version) with each answer's timestamp logged. The portfolio manager reviews via a desktop tool; review action is logged. If the customer skips a question, the flow rejects the submission.

## Fee structure disclosure

The fee structure has to be disclosed before the customer signs the PMS agreement — not as an annex, not in the agreement, but as a separately signed document. The customer ticks "I have read and understood the fee structure" with timestamp. The fee schedule is generated dynamically from the portfolio manager's product config, so we don't show wrong fees.

## Aadhaar e-sign on the agreement

A digital signature pad isn't sufficient for the PMS agreement — SEBI requires Aadhaar-based e-sign (UIDAI eSign API). This adds an extra step in the flow:

- Customer enters Aadhaar
- UIDAI sends OTP
- Customer enters OTP
- UIDAI returns a signed XML
- The signed XML is embedded in the PMS agreement PDF
- The signed PDF is the master copy stored

The customer never has to print or scan anything. Total e-sign step: 30-45 seconds.

## Related-party transactions

If the customer is in any way related to the portfolio manager or its directors, that has to be disclosed. The flow asks:

- Are you related to any portfolio manager / director / employee of [PMS firm]?
- If yes, describe the relation

A "yes" doesn't block the account; it triggers a compliance-officer review event before the account goes live.

## Customer's investment objective

In their own words. This is a free-form text field that the portfolio manager reviews. SEBI's principle is that the customer's stated objective must align with the portfolio manager's strategy — and a one-line "I want returns" doesn't satisfy that. We show example phrasings as placeholders, but force the customer to type their own.

## What the broker / PMS firm avoids

Without an integrated PMS eKYC, PMS firms handle this with:

- A 30-page paper packet emailed to the customer
- A compliance officer reviewing each step manually
- A 2-3 week turnaround per account
- An ops team that re-types data into the back-office system

After integration:

- Single self-serve flow (still requires real customer attention — this isn't 90 seconds; PMS suitability is meant to be deliberate)
- Compliance officer review queue, not full manual handling
- 2-3 day median turnaround
- Direct write-through to back-office

## Compliance checklist verifier

We bundle a SEBI-checklist-aware verifier that runs on every PMS account before it can go live. It enumerates the SEBI-required items, checks each is captured + signed + timestamped, and refuses to mark the account active if any are missing. This is a hard gate, not a warning.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
