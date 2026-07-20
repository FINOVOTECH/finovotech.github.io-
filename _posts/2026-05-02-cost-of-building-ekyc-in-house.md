---
layout: post
title: "Cost of building eKYC in-house: a fintech founder breakdown"
date: 2026-05-02
permalink: /blog/cost-of-building-ekyc-in-house/
canonical_url: https://finovo.tech/blog/cost-of-building-ekyc-in-house
description: "A fintech CTO can build a working eKYC prototype in a sprint. The regulatory-compliant production version takes 9-15 months and a team of 4-6. This is the math."
image: "https://amplify-d3sdrn3vxts2f-main-b-aiimagebucketf893b34d-j21epbs6beu4.s3.ap-south-1.amazonaws.com/media/ai-generated/2026-05-04/00c37b13-afc9-45d2-b940-0fadad3b0068.png"
tags: ["build-vs-buy", "engineering", "cost"]
---

> **Originally published at [finovo.tech/blog/cost-of-building-ekyc-in-house](https://finovo.tech/blog/cost-of-building-ekyc-in-house)** — the canonical version has the latest updates.

Whenever we lose a sale, the most common reason is "we'll build it in-house." Sometimes that's the right call. Often, the founder is underpricing the work.

This is the actual cost breakdown, based on watching 30+ fintechs go down this path.

## The prototype that gets approved

Week 1: a CTO or founding engineer hooks up Aadhaar OTP via a third-party AUA, PAN OCR via Tesseract, and a basic form. Demo at standup. Everyone is excited.

Cost so far: 1 engineer-week.

This prototype works on the happy path. It does not pass SEBI / RBI / IRDAI inspection.

## The regulator-aware version

To get from prototype to compliant production, you need to add:

- **OVD support**: Aadhaar isn't the only acceptable identity proof. Voter ID, passport, driving license each have their own OCR + validation paths. ~3 engineer-weeks.
- **Video PD with operator pool**: live video, geo-fence, random questions, recording, retention. ~6 engineer-weeks for the platform + ongoing operator hiring + training.
- **Risk categorisation engine**: SEBI's risk categories with proper question flows. ~2 engineer-weeks.
- **CKYC integration**: lookup + push to CKYC registry. ~2 engineer-weeks.
- **Audit trail with regulator-grade retention**: 8-year retention, signed records, structured metadata. ~3 engineer-weeks.
- **Per-category compliance overlays**: corporate, HUF, NRI, PMS each have specific extra fields and rules. ~6 engineer-weeks.
- **Re-KYC pipeline**: calendar-driven, OTP-first, smart escalation. ~4 engineer-weeks.
- **Closure flow + reconciliation + regulator notifications**: ~4 engineer-weeks.
- **Bank-account validation against IFSC / micro-deposit verification**: ~2 engineer-weeks.
- **Spam / abuse / fraud detection**: ~3 engineer-weeks.
- **Compliance officer review queues**: dashboards, escalation, audit logs. ~3 engineer-weeks.

Add up: ~38 engineer-weeks of focused work, before you've shipped your first customer.

In practice, with team coordination overhead and the inevitable scope changes, this becomes 50-65 engineer-weeks. Call it 12-15 months for a 4-engineer team.

## The compliance maintenance treadmill

Once shipped, the work doesn't stop:

- SEBI publishes a Master Circular update every 4-6 weeks; some require code changes within 30 days
- UIDAI changes Aadhaar API contracts a few times per year
- RBI / IRDAI update their KYC rules quarterly
- Fraud patterns evolve faster than that

A continuous compliance team of 0.5-1 engineer + 0.25 compliance officer is the running cost. Annual: ~₹20-40 lakh in salary + ~₹5-10 lakh in audit / consulting.

## The audit cost

Every regulated entity gets audited. SEBI does annual broker audits; RBI does triannual NBFC audits; IRDAI does annual insurer audits. The auditor will:

- Pick 100-300 random customer KYCs
- Verify every step of each one against the audit trail
- Surface specific gaps with timeline for remediation

If your audit trail is missing or incomplete, the cost of remediation is on you — typically 2-4 weeks of focused engineering work + a follow-up audit.

We've seen audits where the cost of remediation alone (engineer time + outside consultants + delayed product launch) exceeded the cost of buying an off-the-shelf KYC system for the next 5 years.

## The opportunity cost

While 4 engineers are building eKYC, they're not building:

- Your unique product features
- Your customer-acquisition tooling
- Your data science / personalisation
- Your scale-out tooling

Most fintechs that succeed have a defensible product moat that ISN'T eKYC. Building eKYC in-house is the same engineering work as buying it, but with a slower clock to your actual product moat.

## When in-house makes sense

In-house eKYC is the right call when:

- You're a regulator-adjacent infrastructure company (i.e. you ARE the KYC vendor)
- You have unique customer-data requirements that off-the-shelf can't satisfy
- You have a compliance team of 5+ already on staff
- You're building a 10-year product, not a 3-year product

Otherwise: buy.

## The price comparison

Off-the-shelf KYC for a typical mid-size broker (50K KYCs / year):

- Buy: ~₹50-80 lakh / year (per-KYC pricing)
- Build: ~₹3-5 crore upfront (12-15 months × 4 engineers) + ~₹40-60 lakh / year ongoing

Build pays back at year 6-7 for a stable customer count. Most fintechs don't make it to year 6.

## We're biased — but the math is the math

Yes, this is a sales argument. We sell KYC. So our framing is suspect.

The actual numbers above are conservative. Engineering teams who've done this honestly will tell you we're under-estimating. Try the breakdown yourself with your team's burn rate.

If after the math, building still makes sense for your specific situation: build. If buying makes more sense, [book a demo](/contact) and we'll show you the production-ready version of what you would have built.

---

**Read more on our main site:** [https://finovo.tech/blog](https://finovo.tech/blog)  
**About Finovo Tech:** SEBI/RBI/IRDAI-aligned KYC + MFD infrastructure for Indian fintech. Visit [https://finovo.tech](https://finovo.tech).
