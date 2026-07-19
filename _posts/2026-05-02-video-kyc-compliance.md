---
layout: post
title: "Video KYC compliance: SEBI / RBI / IRDAI rules and how Finovo handles them"
date: 2026-05-02
permalink: /blog/video-kyc-compliance/
canonical_url: https://finovo.tech/blog/video-kyc-compliance
description: "Video PD (Personal Discussion) is the most-asked-about KYC step. The regulator rules are not identical across SEBI, RBI, and IRDAI. Here's the merged checklist."
tags: ["video-kyc", "compliance", "sebi", "rbi", "irdai"]
---

> **Originally published at [finovo.tech/blog/video-kyc-compliance](https://finovo.tech/blog/video-kyc-compliance)** — the canonical version has the latest updates.

Video KYC (also called V-CIP — Video-based Customer Identification Process) is permitted by all three Indian financial-sector regulators. The rules aren't identical, but a well-designed flow can satisfy all three.

## SEBI's video KYC rules

SEBI permits V-CIP for individual KYC under specific conditions:

- The video call must be live, not pre-recorded
- The broker's authorised official conducts the call (not a chatbot, not the customer's spouse)
- The customer's geo-location must be verified during the call (in India)
- The customer's PAN must be visually confirmed during the call (held up to the camera)
- The customer's face must match the photo on file (visual + algorithmic match)
- The full video is recorded and stored
- The recording includes the broker's official's identification

Reference: SEBI Master Circular on KYC + Master Direction on V-CIP.

## RBI's video KYC rules (for NBFCs and banks)

RBI's V-CIP rules are very similar but have one extra:

- Random questions to confirm the customer's identity (e.g. "what's your father's name?", asked verbally and matched against the form)
- The official can only conduct V-CIP from "an approved location" (typically the official's office or registered home location)

Reference: RBI Master Direction on Video-based Customer Identification Process.

## IRDAI's video KYC rules (for insurers)

IRDAI followed RBI's V-CIP guidelines mostly. Specifics for insurance:

- For high-value policies (sum insured above a threshold), video KYC may be replaced by physical verification
- Insurance-specific declarations (occupation hazards, etc.) are part of the video conversation
- Recording must be tagged with the policy reference, not just the customer ID

Reference: IRDAI circular on V-CIP.

## What a single flow needs to satisfy all three

A flow that hits all three regulators' requirements:

- Live video, both sides shown
- Customer's geo-fenced (we use IP + device-GPS + browser geolocation as triangulation)
- PAN held up + visually verified by the official
- Random question per RBI (we ask 2-3 standard questions: father's name, DOB, full address)
- Official's identification visible in the recording
- Recording stored with metadata (timestamp, duration, geo, customer ID, official's employee ID)
- Tagged for the right vertical (broker / NBFC / insurer) so audit retrieval works

## What goes wrong in DIY video KYC

Brokers building their own video KYC tools usually miss:

- Geo-fencing — they ask for IP location only, which the customer can VPN around
- Random questions — they hard-code the same 3 questions; auditors notice
- Recording quality — they use stock WebRTC without proper resolution / codec settings; the recording can't establish identity later
- Storage retention — they store on their own server with no automatic 8-year retention
- Audit metadata — they record the video but don't tag it with the structured metadata regulators want

## Operator side

Video KYC requires real humans on the operator side. We staff:

- IST business hours: full coverage with 30-90 second wait times
- IST early morning / late evening: limited coverage, customers can schedule a slot
- NRI customers: GMT + EST + AEST coverage for high-volume markets

Operator training is regulator-mandated: each operator goes through a 40-hour V-CIP curriculum + recurrent annual training. We maintain the training records for audit.

## When video KYC isn't required

Video KYC is mandatory in some cases (high-risk customers, certain product categories) and optional in others (low-risk retail individual KYC). The regulators allow other PD methods:

- In-person verification at a branch (still common for HNI)
- Aadhaar e-sign + standard fields (for lowest-risk retail in some product categories)

A smart KYC flow uses video PD only when required, not by default. This drops cost and improves customer experience.

For a deeper dive, see our [video kyc cost](https://finovo.tech/p/video-kyc-cost-india).

## Cost considerations

Video KYC has a meaningful per-call cost — operator time + recording storage + bandwidth. Typical cost: ₹20-40 per video PD at scale, vs ₹6-8 for Aadhaar OTP.

For high-risk customer flows, mandatory. For low-risk retail, decisively skip when allowed.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
