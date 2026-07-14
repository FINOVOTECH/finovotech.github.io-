---
layout: post
title: "Corporate eKYC: PVT Ltd / LLP / Partnership digital onboarding"
date: 2026-05-02
permalink: /blog/corporate-ekyc-coming-soon/
canonical_url: https://finovo.tech/blog/corporate-ekyc-coming-soon
description: "Corporate accounts are the highest-revenue KYCs and the slowest. We're shipping a corporate eKYC product that handles PVT Ltd, LLP, and partnership entities dig"
tags: ["corporate", "ekyc", "pvt-ltd", "compliance"]
---

> **Originally published at [finovo.tech/blog/corporate-ekyc-coming-soon](https://finovo.tech/blog/corporate-ekyc-coming-soon)** — the canonical version has the latest updates.

Corporate trading accounts are the most valuable customers a broker has — average ticket size 100x retail, repeat trading volume in lakhs per month — and traditionally the slowest to onboard. A typical PVT Ltd account opening at a Tier-1 broker takes 3-5 weeks of paperwork shuffling.

Corporate eKYC is a Finovo upcoming product that compresses that to under a day.

## What corporate accounts need

The regulator's required corporate KYC inputs:

- The entity's PAN
- The entity's CIN (Corporate Identification Number from MCA)
- A verified ROC filing snapshot
- KYC of every director (individual KYC, complete)
- KYC of every beneficial owner with &gt; 25% stake
- The board resolution authorising the account opening
- An AOA / MOA (or equivalent for LLP / partnership)
- Bank account proof in the entity's name
- Signature of the authorised signatory

The directors' individual KYC is the same flow as our retail eKYC — proven path. The novel parts are:

1. ROC integration so we don't re-collect data the MCA already has
2. Beneficial-owner capture (a non-trivial UX problem when ownership goes through holding companies)
3. Board resolution upload + parsing

## ROC integration

Every PVT Ltd has a public profile on the MCA portal — directors, registered address, share-capital structure, last filing date. The corporate eKYC flow asks the customer for the CIN, then auto-pulls:

- Registered name (as filed)
- Registered address
- Date of incorporation
- Authorized + paid-up capital
- Director list (with DINs + appointment dates)

The customer reviews + confirms. They don't re-type any of this.

## Beneficial owner capture

This is where corporate KYC traditionally drags. SEBI requires you to identify every individual with &gt; 25% beneficial ownership — including indirect ownership through holding companies. So if Acme Pvt Ltd is owned by Beta Holdings Pvt Ltd which is owned by an individual, you need to know about the individual.

The flow handles this iteratively: customer enters the immediate shareholders. If any are companies, the flow asks for those companies' shareholders. Recurses until it lands on individuals or stops at the 25% beneficial-ownership threshold.

For the typical 5-shareholder closely-held PVT Ltd, this is 90 seconds. For a 4-layer holding-company structure, it can take 10-15 minutes — but you're not redoing the whole KYC on a phone call when you discover the structure.

## Board resolution

The board resolution authorising account-opening + appointing a signatory is uploaded as PDF. We OCR + parse to extract:

- The resolution date
- The directors present
- The named signatory's name and DIN
- The trading limits (if specified)

Customer reviews the parsed output. We attach the original PDF to the audit trail.

## Why "coming soon"

The product is functional and in pilot with three brokers. We're holding general availability until two things land:

- Multi-language support for AOA / MOA parsing (currently English-only; next is Hindi)
- A migration path from the legacy paper-corporate-KYC database that most brokers carry

Both should land in the next quarter. If you're a high-volume corporate-account broker, [book a demo](/contact) and we'll add you to the early-access list.

## What it replaces

Today, the typical corporate account workflow is:

1. RM emails the customer a 40-page PDF
2. Customer prints, signs, scans, emails back
3. Broker ops physically files the original at HQ
4. RM emails the customer 4 follow-up requests for missing documents
5. ROC verification is manual (someone literally types the CIN into the MCA portal)
6. After 18-21 days, the account is opened — and the customer has half-forgotten why they were opening it

Corporate eKYC moves all of step 1-5 into a 30-minute self-serve flow. RM still does the customer relationship; they just stop doing the paperwork.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
