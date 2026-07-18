---
layout: post
title: "Aadhaar XML vs Aadhaar OTP — picking the right KYC flow"
date: 2026-05-02
permalink: /blog/aadhaar-xml-vs-otp/
canonical_url: https://finovo.tech/blog/aadhaar-xml-vs-otp
description: "Aadhaar OTP and Aadhaar XML (offline) are the two regulator-blessed paths for Aadhaar-based KYC. They look similar from outside; they're very different in pract"
tags: ["aadhaar", "ekyc", "compliance", "india"]
---

> **Originally published at [finovo.tech/blog/aadhaar-xml-vs-otp](https://finovo.tech/blog/aadhaar-xml-vs-otp)** — the canonical version has the latest updates.

Aadhaar-based KYC is the backbone of digital onboarding in India. SEBI, RBI, and IRDAI all accept it for individual customer verification. There are two paths — Aadhaar OTP and Aadhaar XML (also called offline Aadhaar) — and the choice between them isn't obvious.

## Aadhaar OTP

The customer enters their Aadhaar number; UIDAI sends an OTP to their registered mobile; they enter the OTP; UIDAI returns a digitally-signed eKYC packet with their verified data.

- **Cost**: roughly ₹6-8 per KYC (UIDAI charges per call)
- **Latency**: 12-18 seconds for the round trip
- **Data returned**: name, DOB, address, gender, photo (low-resolution, signed by UIDAI)
- **Audit trail**: UIDAI signs the response so it's verifiable later
- **UX**: clean — customer types Aadhaar, types OTP, done
- **Failure modes**: registered mobile not active, OTP delay, UIDAI service downtime (rare but happens)

## Aadhaar XML (offline)

The customer downloads an Aadhaar XML zip from the UIDAI website (myaadhaar.uidai.gov.in), encrypted with a 4-character share code they set. They upload the zip + share code to the broker; the broker decrypts and verifies the contents.

- **Cost**: zero (no UIDAI per-call fee)
- **Latency**: depends on the customer downloading the file (few minutes)
- **Data returned**: name, DOB, gender, address, photo (high-resolution, signed by UIDAI)
- **Audit trail**: same UIDAI signature
- **UX**: requires the customer to do a multi-step download, set a share code, upload to you
- **Failure modes**: customer forgets share code, customer can't navigate UIDAI site, file expires (24h validity)

## When to use OTP

Default to OTP for retail individual customers. The cost is real but the UX win compensates. We measure end-to-end completion 12-15 percentage points higher with OTP than with XML for the same customer demographic.

Use OTP for:

- Mass-market retail brokers
- MFD platforms
- NBFC personal-loan customers
- Insurance customers

## When to use XML

XML wins when:

- The customer is high-net-worth and the broker can hand-walk the customer through it (HNI / PMS / wealth management contexts)
- The customer is rural or in a low-bandwidth area where the OTP delivery is unreliable
- Cost matters at scale (a 1M-KYC/year broker pays ~₹70 lakh/year in OTP fees; XML saves that)
- The broker wants the high-resolution photo for facial-match scoring

## What about Aadhaar Biometric (e-Aadhaar)?

There's a third path — Aadhaar fingerprint or iris biometric authentication via a hardware device. SEBI permits it; we don't recommend it for retail because it requires a physical biometric device at the customer's end, which is rarely available.

For specific contexts (in-person KYC desks at branch offices), it makes sense. For purely-remote retail, no.

## What you can't get from Aadhaar (any path)

- The customer's PAN (separate, has to be collected + validated separately)
- The customer's email (Aadhaar has no email field)
- Real-time photo of the customer right now (you get the Aadhaar-stored photo, which may be 5-10 years old; for fresh selfie, run a video PD)
- Bank account details
- Family info beyond father's name
- Source of funds, occupation, risk-cat (separate questionnaires)

## Hybrid flows

The pragmatic answer for most brokers is hybrid: try OTP first, fall back to XML if OTP fails. Smart fallback:

- Customer enters Aadhaar
- System tries OTP path
- If OTP fails after 2 retries, system says "we'll fall back to offline Aadhaar — here's how"
- Customer is walked through the XML download
- If they complete it, KYC goes through; if not, manual review

We see ~4% fallback to XML across most retail brokers; the other 96% complete via OTP.

## Cost optimisation at scale

For brokers doing 1M+ KYCs/year, OTP fees add up. Options:

- Negotiate volume rates with the broker's AUA (Authorisation User Agency, who routes the OTP call)
- Cache OTP-verified KYCs at the broker level so re-KYC reuses the OTP packet without a fresh call (within UIDAI's caching policy)
- Default to XML for specific customer categories where the customer is patient (corporate accounts, HNI)

A combination of these typically saves 30-40% of OTP cost without UX degradation.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
