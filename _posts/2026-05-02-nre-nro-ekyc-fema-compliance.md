---
layout: post
title: "NRE / NRO eKYC: NRI onboarding under FEMA compliance"
date: 2026-05-02
permalink: /blog/nre-nro-ekyc-fema-compliance/
canonical_url: https://finovo.tech/blog/nre-nro-ekyc-fema-compliance
description: "NRI accounts (NRE, NRO, NRO-PIS) have a layered compliance stack — KYC + FEMA + tax-residence + investment-restriction rules. Digital NRI onboarding has to hand"
tags: ["nri", "fema", "ekyc", "compliance"]
---

> **Originally published at [finovo.tech/blog/nre-nro-ekyc-fema-compliance](https://finovo.tech/blog/nre-nro-ekyc-fema-compliance)** — the canonical version has the latest updates.

NRI account opening is the highest-stakes KYC in Indian finance. The customer is high-net-worth, the ticket size is large, and the compliance surface is massive: SEBI + RBI's FEMA + the customer's country-of-residence regulator + FATCA + tax-residence implications.

Most brokers' NRI onboarding is still manual — a relationship manager and a compliance officer working together over email for 2-3 weeks per customer.

Digital NRI onboarding ([NRE/NRO eKYC](/services#nre-nro-account)) compresses this to a single end-to-end flow.

## The account types

There are three flavours of NRI account a broker typically opens:

- **NRE (Non-Resident External)**: USD-rupee account, repatriable. Used for fresh foreign earnings the NRI wants to invest in India.
- **NRO (Non-Resident Ordinary)**: Rupee account, restricted repatriation (currently $1M / year). Used for income earned in India (rent, dividends, etc.).
- **NRO-PIS (Portfolio Investment Scheme)**: A specific NRO sub-type for stock-market investments, mandatory designation per RBI.

Each has different documentation requirements and per-country restrictions.

## Passport-OCR + OCI / PIO capture

NRIs are identified by passport (not Aadhaar — many don't have one any more, and FEMA doesn't recognise Aadhaar for NRI status). Passport OCR is harder than PAN OCR because:

- Passports vary by country (different layouts, MRZ encoding, photo position)
- Date formats differ
- Some countries' passports have non-Latin name fields

Our OCR runs an MRZ-first parser (the machine-readable zone at the bottom is standardised by ICAO) and falls back to layout-based extraction. Coverage: 50+ countries with &gt; 95% extraction accuracy.

OCI (Overseas Citizen of India) and PIO (Person of Indian Origin) cards are uploaded separately when the customer has them — they're not technically required for NRI status but help establish Indian-origin claims.

## FATCA / CRS declaration

US persons (or US-tax-residents anywhere) are subject to FATCA. The flow asks:

- Are you a US citizen? (yes / no)
- Are you a US tax resident? (yes / no, with criteria explained)
- Do you have a US TIN? (entered if yes)

Non-US NRIs are subject to CRS (Common Reporting Standard) — declaration of all tax-residence jurisdictions, with TIN per jurisdiction. The flow auto-detects countries with CRS reporting agreements with India and drives the right declarations.

Misreported FATCA / CRS is one of the most common reasons for SEBI observation letters on NRI accounts. Worth getting right.

## FEMA declaration

The actual FEMA-mandated declarations are about source of funds + repatriation intent + portfolio investment cap. We ask:

- Source of funds (employment / business / investment / inheritance / other)
- Whether they intend to repatriate proceeds
- Their NRI status start date (so we can determine FEMA category)
- Whether they hold any restricted securities under their country's law (e.g. some US tax-residents can't hold certain Indian instruments)

These are presented as quick-reply forms with explanations, not as a free-form box.

## Country-of-residence investment restrictions

Some NRI investment products are restricted by the customer's country-of-residence regulator:

- US persons cannot invest in most Indian mutual fund schemes (SEC reasons)
- Canadian residents can but with extra disclosure
- Some EU countries require MIFID-II suitability tests
- UAE is generally open

The flow checks the customer's country at sign-up and shows / hides eligible products on the broker's catalogue. This avoids the broker having to manually intervene later.

## Bank account proof

NRE / NRO accounts at the broker reference an existing NRE / NRO bank account. The flow validates the provided IFSC + account number against the bank's NRE / NRO designation. Customer-provided "savings account" that's not actually NRE-flagged gets caught here.

## Video PD considerations

NRIs are generally outside the broker's geo-fence. Video PD with a real operator works (we have queues across IST + EST + GMT business hours). For high-net-worth customers, we offer scheduled video PD slots so the customer can pick a convenient time.

## What's hard about NRI onboarding

The compliance stack is layered. Each step alone is solvable; the integration is what gets you. We've shipped NRI eKYC for several large brokers; total launch time is typically 4-6 weeks because every broker's NRI customer mix is different and the country-of-residence config has to be tuned.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
