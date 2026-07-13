---
layout: post
title: "Vanilla eKYC: 90-second retail onboarding"
date: 2026-05-02
permalink: /blog/vanilla-ekyc-90-second-onboarding/
canonical_url: https://finovo.tech/blog/vanilla-ekyc-90-second-onboarding
description: "Most retail brokers ship a 4-minute KYC and accept 60% completion. Here's the design choices that take it to 90 seconds and 94% completion without changing what"
tags: ["ekyc", "speed", "completion"]
---

> **Originally published at [finovo.tech/blog/vanilla-ekyc-90-second-onboarding](https://finovo.tech/blog/vanilla-ekyc-90-second-onboarding)** — the canonical version has the latest updates.

Every retail-broker pitch deck shows a "fastest KYC in India" stat. Most are 4-minute flows that the team rounded down. Real medians, taken across 1M+ customers, sit between 110 and 180 seconds.

90 seconds is achievable, but only if you make a small number of unintuitive choices early.

## What the regulator actually requires

For a normal individual with an Aadhaar + PAN, SEBI requires:

- Identity (Aadhaar or other OVD)
- Address (Aadhaar or other OVD)
- PAN
- A risk-categorisation question set (politically-exposed, source of funds, occupation)
- Either video PD or in-person verification

Note: video PD is not always required for all customers. Aadhaar OTP + PAN + risk-cat is sufficient for many low-risk individual customers. The default-on video-PD is a self-imposed compliance choice by many brokers, not a SEBI rule. We turn it on or off per risk-category.

## Where the seconds go

Profiled across many brokers, the long-tail in a typical "4-minute" flow:

| Step | Median time | What's actually happening |
|---|---|---|
| App / page load | 8s | First-paint + KYC form bundle |
| OTP entry | 22s | Wait for SMS, switch to SMS app, copy OTP, paste back |
| PAN photo | 31s | Find PAN, take photo, retry once |
| Video PD setup | 28s | Permission grant for camera, lighting, "say your name" prompt |
| Video PD recording | 45s | Live operator queue + 30s recording |
| Form fields | 24s | Address, occupation, FATCA, source-of-funds |
| Final review + submit | 14s | Long Ts and Cs, signature |
| **Total** | **172s** | |

The 90-second flow doesn't *skip* anything; it removes wait + switching costs.

## How we get to 90 seconds

The five biggest wins:

1. **Aadhaar OTP, no SMS round-trip**: capture OTP in the same screen via `<input>` autocomplete attribute (`autocomplete="one-time-code"`). On iOS this auto-pastes from SMS; on Android we use the SMS Retriever API. Saves ~12 seconds.

2. **PAN photo with on-device OCR**: don't ship the photo to a server for OCR. Run a small model in-browser (or in-app) that auto-captures the PAN when sharpness + glare are acceptable. The customer doesn't tap a shutter button; the page just notices the PAN is in frame and captures. Saves ~18 seconds.

3. **No video PD by default for low-risk**: as above, this isn't required for many customers. Skip it unless the risk-cat triggers it. Saves ~73 seconds for ~70% of customers.

4. **Pre-filled form fields from PAN + Aadhaar**: address from Aadhaar, name from PAN, DOB from PAN. Customer reviews + confirms instead of typing. Saves ~16 seconds.

5. **One-screen review-and-submit**: the legal copy is shown in a collapsed scroll-area (not a separate Ts and Cs page). Saves ~6 seconds + reduces drop-off.

## Pass rate, not just speed

Speed is meaningless if customers drop off. The vanilla flow ([eKYC vanilla](/services#ekyc-vanilla)) tracks at 94% pass rate measured across 200K+ recent flows. Failures are mostly:

- 3.2% PAN-mismatch (typo on form vs OCR)
- 1.4% Aadhaar OTP timeout
- 0.9% video PD anomaly (when triggered)
- 0.4% network error mid-flow
- 0.1% other

The PAN-mismatch failures usually convert on retry; total customer-side recovery is ~97%.

## Where vanilla isn't enough

Vanilla works for individuals. If you need:

- Custom branded flow on your domain
- Per-state regulatory variations (a few SEBI master circulars require state-specific clauses)
- Integration with your in-house RM workflow

…you want [eKYC enterprise](/services#ekyc-enterprise), which is the same engine wrapped in white-label + per-broker config.

## Try it

The 90-second number is verifiable — book a demo and we'll walk you through one customer's full flow with the timestamps visible. No staged demo accounts; we use the actual production logs.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
