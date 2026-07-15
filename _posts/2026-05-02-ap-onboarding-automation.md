---
layout: post
title: "Authorised Person onboarding automation for SEBI-registered brokers"
date: 2026-05-02
permalink: /blog/ap-onboarding-automation/
canonical_url: https://finovo.tech/blog/ap-onboarding-automation
description: "Adding an Authorised Person to your SEBI broker license is a regulated process: NSE / BSE registration, AP code allocation, indemnity bond, KYC. Digital AP onbo"
tags: ["authorised-person", "sebi", "sub-broker"]
---

> **Originally published at [finovo.tech/blog/ap-onboarding-automation](https://finovo.tech/blog/ap-onboarding-automation)** — the canonical version has the latest updates.

Authorised Persons (APs) — formerly called sub-brokers — are the field force of most Indian brokers. SEBI mandates a specific onboarding process before an AP can transact on a broker's behalf:

- Individual KYC of the AP
- NISM-VIII (Equity Derivatives) certification (where required)
- NSE and / or BSE registration as that broker's AP
- AP code allocation
- Indemnity bond
- Customer-handling permissions config

Each step used to be paper. Each one took 1-2 weeks. The full chain often took 4-6 weeks per AP — which is why brokers tend to onboard APs in batches and why APs sit idle for the first month or two.

[AP onboarding](/services#ap-onboarding) compresses this to under 5 working days.

## The KYC step

Same individual KYC flow as a customer, but on the AP onboarding flow. Aadhaar OTP + PAN + video PD. APs are typically professionals (CFP, MBA, etc.) so they tend to complete this in under 2 minutes.

## NISM certification check

For APs handling derivatives, NISM-VIII certification is mandatory. The flow asks for the AP's NISM certificate ID and validates against the NISM database (NSE has a published API). If the AP doesn't have it, the flow blocks onboarding for derivatives but allows equity-only onboarding.

## NSE / BSE registration

This is where the digital flow really helps. Each exchange has an AP registration system:

- NSE: NEAT-ID-based AP registration
- BSE: BTN-based AP registration

Both require the broker to file Form-A (or its modern digital equivalent) on the exchange portal, naming the AP. The exchanges return an AP code within 1-3 days.

The AP onboarding flow handles the form filing automatically. The broker's ops team sees the AP code arrive in their inbox; they don't have to type it into anything.

## AP code allocation

Once the exchange returns the AP code, it's allocated in the broker's system to:

- A region (so geography-based commissions work)
- A team / RM (so reporting hierarchies work)
- A product permission set (equity-only / derivatives / both)

This is broker-policy work, not regulator work — but the flow has the config UI to do it.

## Indemnity bond

The AP signs an indemnity bond protecting the broker from AP-side mistakes. Standard SEBI-approved bond template; we host it as a PDF, the AP signs via Aadhaar e-sign.

## Customer-handling permissions

Once active, the AP gets:

- A unique customer-onboarding referral code (so customers brought in by this AP are automatically tagged to them)
- A login to the broker's RM dashboard (read-only by default; full access on broker policy)
- A commission-tracking page showing their revenue share in real-time

## Bulk onboarding

Most brokers add APs in waves — 50-200 APs after a hiring round. The flow supports CSV upload of basic AP details; each AP then gets an SMS / email link to complete their own onboarding flow. This way the broker's ops team doesn't have 200 KYC sessions to chaperone.

## Compliance reporting

SEBI requires brokers to report AP activity periodically. The AP onboarding flow captures the data points needed for the report — number of APs onboarded per quarter, geographic distribution, NISM certification rate — and outputs the SEBI-format CSV on demand.

For a deeper dive, see our [trading automation api nse](https://finovo.tech/p/trading-automation-api-nse).

## What it replaces

The typical AP onboarding workflow before:

- HR shortlists the AP
- HR hands a 30-page packet to the AP
- AP fills + signs + couriers back
- HR forwards to compliance
- Compliance forwards to NSE / BSE
- 1-3 weeks later, AP code arrives
- Compliance allocates the code to a region / team
- AP starts working

After:

- HR enters AP details into the dashboard
- AP receives a link, completes online flow in 30-45 minutes
- Exchange-side filing automatic
- AP code arrives in the dashboard (1-3 days, regulator latency)
- Allocation happens at AP-code arrival
- AP starts working

5-day vs 21-30-day onboarding. The customer-facing impact is that APs reach productive headcount faster.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
