# Requirements Package: Advanced AI MSL & Integration Platform

**Date:** 2026-06-29  
**Prepared for:** ADVANCE AI — Product Manager, Third-Party Integrations & MSL Products  
**Linked Analysis:** `market-analysis-2026-06-29.md`

---

## Feature Opportunity: Real-Time MSL Intelligence Hub with Integrated Payer Context

### Background

Market analysis identified two compounding gaps in the current health tech AI landscape:

1. **MSL insight capture is broken.** Field medical teams generate high-value clinical insights during HCP interactions, but capture is unstructured (freeform notes, emails, verbal), synthesis is manual, and insights rarely flow systematically back to medical strategy teams. No vendor has built a purpose-designed, AI-native insight management workflow for MSLs.

2. **Payer intelligence doesn't reach the field.** MMIT and similar platforms serve market access teams at HQ. MSLs have no real-time access to formulary status, step-therapy requirements, or payer policy changes at the point of HCP engagement—leading to misaligned conversations and missed opportunities.

**The opportunity:** Build a unified MSL Intelligence Hub that (a) captures and structures field insights via AI-assisted voice and text workflows, (b) surfaces real-time payer policy context relevant to the HCP's covered population, and (c) pushes synthesized insight reports upstream to medical strategy—all integrated with the Veeva/Salesforce CRM ecosystem and FHIR-compliant clinical data sources.

This opportunity is directly aligned with the ADVANCE AI PM role's ownership of third-party integrations and MSL products, and addresses the market access and MSL workflow gaps none of the identified competitors fully serve.

---

## User Stories

---

### Story 1: AI-Assisted Field Insight Capture

**As an** MSL conducting post-HCP-meeting documentation,  
**I want** to speak a freeform debrief into the ADVANCE AI mobile app and have it automatically structured into tagged insight fields (HCP sentiment, unmet medical need, off-label interest, competitive mentions, follow-up actions),  
**so that** I can submit a complete, structured insight record in under 2 minutes without switching tools, and my medical affairs team receives consistent, analyzable data across all field interactions.

#### Acceptance Criteria

**Given** the MSL has completed an HCP meeting and opens the insight capture screen,  
**When** the MSL records a voice debrief of 30–300 seconds,  
**Then** the system transcribes the audio, extracts and pre-populates structured fields (HCP name, therapeutic area, sentiment score, unmet need tags, competitive brand mentions, follow-up action type and due date), and presents a review screen within 15 seconds.

**Given** the MSL reviews the auto-populated insight draft,  
**When** the MSL taps "Submit" or edits and submits,  
**Then** the structured insight record is written to the linked Veeva CRM contact record and to the ADVANCE AI insights database within 30 seconds.

**Given** an insight contains a flagged regulatory-sensitive term (e.g., off-label promotion signal, unverified safety claim),  
**When** the AI identifies such content during extraction,  
**Then** the field is highlighted with a compliance warning, submission is paused pending MSL confirmation, and the event is logged in the audit trail with a timestamp and the MSL's user ID.

---

### Story 2: Real-Time Payer Context at Point of HCP Engagement

**As an** MSL preparing for or immediately following a meeting with a high-volume prescriber,  
**I want** to see a one-screen summary of the payer coverage landscape relevant to that HCP's patient population (formulary tier, prior auth requirements, recent policy changes, access block status for my therapeutic area),  
**so that** I can tailor my scientific exchange to the real access barriers the HCP's patients face, and flag urgent payer issues for my market access colleagues.

#### Acceptance Criteria

**Given** the MSL opens an HCP profile in the ADVANCE AI mobile app,  
**When** the HCP record has associated payer mix data (from CRM, claims data, or MSL-entered zip code),  
**Then** the app displays a "Payer Context" card showing: top 3 payers by covered lives %, formulary status for the relevant product(s), any UM/step-therapy requirements, and a "policy change" badge if any of those payers issued a formulary update in the past 30 days.

**Given** a payer has issued a material formulary or policy change in the past 48 hours affecting the MSL's therapeutic area,  
**When** the MSL opens any HCP profile whose payer mix includes that payer,  
**Then** a push notification and in-app alert are surfaced with a plain-language summary of the change and a link to the full policy document.

**Given** payer data is unavailable for a specific HCP,  
**When** the system cannot resolve payer mix,  
**Then** the app displays a "Payer data not available — tap to enter zip code for regional payer estimate" prompt rather than a blank or error state.

---

### Story 3: Synthesized Insight Reporting for Medical Strategy Teams

**As a** Medical Affairs Director reviewing field insights across 20+ MSLs,  
**I want** a weekly AI-synthesized insights digest that surfaces recurring HCP themes, emerging unmet needs, and competitive intelligence trends by therapeutic area and geography,  
**so that** I can identify where clinical evidence gaps or market access friction are affecting adoption, and make data-informed decisions about publication strategy, medical information priorities, and MSL deployment.

#### Acceptance Criteria

**Given** at least 5 structured insight records have been submitted in the past 7 days for a therapeutic area,  
**When** the weekly digest generation job runs (configurable day/time, default: Monday 7am local),  
**Then** the system produces a digest report containing: top 3–5 recurring HCP themes (with frequency count and representative quotes), emerging unmet need signals (defined as themes new in the last 14 days), competitive brand mention frequency ranked by brand, and MSL field activity summary (meetings logged, follow-ups due).

**Given** the digest is generated,  
**When** the Medical Affairs Director opens the digest in the web dashboard or receives it by email,  
**Then** each insight cluster links through to the underlying individual insight records for drill-down, and the report is exportable as PDF and CSV.

**Given** the digest includes any HCP quotes or identifiable clinical information,  
**When** the report is generated,  
**Then** all HCP-identifiable data is either anonymized by default or gated behind role-based access control that requires explicit permission for the viewer's user role.

---

### Story 4: Veeva/Salesforce CRM Bi-Directional Integration

**As an** MSL using Veeva CRM as my system of record,  
**I want** all ADVANCE AI insight captures, payer context views, and follow-up actions to sync bi-directionally with my Veeva contact and activity records,  
**so that** I never have to enter the same information twice, my CRM remains the authoritative source of HCP engagement history, and my manager has full visibility in the tool they already use.

#### Acceptance Criteria

**Given** an MSL submits a structured insight record in ADVANCE AI,  
**When** the submission is confirmed,  
**Then** a corresponding Activity record is created in the linked Veeva CRM contact within 60 seconds, including the insight summary, key tags, and a deep link back to the full ADVANCE AI record.

**Given** an MSL schedules a follow-up action in ADVANCE AI (e.g., "send publication reprint," "escalate to Medical Information"),  
**When** the action is saved,  
**Then** a Task is created in Veeva CRM assigned to the MSL with the specified due date, action type, and HCP context.

**Given** an HCP record is updated in Veeva CRM (e.g., new affiliation, role change),  
**When** the update syncs to ADVANCE AI via the integration layer,  
**Then** the ADVANCE AI HCP profile reflects the change within 15 minutes and any cached payer context is invalidated and re-fetched.

**Given** the Veeva CRM OAuth token expires or the connection is interrupted,  
**When** an MSL attempts to submit an insight,  
**Then** the insight is queued locally on-device and automatically synced when the connection is restored, with no data loss and a visible "Queued for sync" status indicator.

---

### Story 5: FHIR-Native Clinical Site Integration for Trial-Participating MSLs

**As an** MSL supporting a clinical trial site,  
**I want** to view real-time trial enrollment status, protocol amendments, and site-level performance data pulled via FHIR from the site's EHR or CTMS,  
**so that** I can have informed, data-rich conversations with site investigators about trial progress and proactively flag enrollment or compliance issues to the clinical operations team.

#### Acceptance Criteria

**Given** a clinical site has authorized the FHIR integration and the MSL is assigned to that site,  
**When** the MSL opens the site profile in the ADVANCE AI app,  
**Then** the app displays: current enrollment count vs. target, last patient visit date, any open protocol deviations flagged in the source system, and site investigator contact information—all sourced via FHIR R4 API.

**Given** the FHIR API returns a protocol deviation or enrollment lag alert for a site,  
**When** the alert is detected during a scheduled data pull (minimum: every 4 hours),  
**Then** the assigned MSL receives an in-app push notification and the alert is logged in the site activity feed.

**Given** a site's EHR uses a non-FHIR legacy integration standard,  
**When** the MSL's site profile is configured,  
**Then** the integration settings screen clearly indicates the site's integration method (FHIR, HL7 v2, or Manual), and manual data entry fields are available as a fallback with a prompt to request IT-assisted FHIR onboarding.

---

## One-Page Product Spec: MSL Intelligence Hub — v1.0

---

### Problem Statement

Medical Science Liaisons are the highest-touch interface between pharmaceutical companies and the clinical community—but they operate with inadequate tooling. Insight capture is slow, unstructured, and disconnected from medical strategy systems. Payer intelligence is siloed at headquarters, leaving MSLs unable to address the access barriers HCPs and patients actually face. These gaps reduce the strategic value of field medical investment and create compliance risk through inconsistent documentation. No existing platform in the competitive landscape provides a unified, AI-native solution that serves MSL workflows, integrates with Veeva/Salesforce and FHIR systems, and connects field insights to medical strategy—while meeting the FDA/EMA 2026 AI governance standards.

---

### Proposed Solution

ADVANCE AI's MSL Intelligence Hub is a mobile-first, AI-native platform that transforms how MSLs capture insights, access payer intelligence, and connect with clinical systems. Core capabilities for v1.0:

- **AI Insight Capture:** Voice-to-structured-insight transcription and classification, embedded in the MSL's existing Veeva/Salesforce workflow via bi-directional API sync.
- **Payer Context Engine:** Real-time formulary status and policy change alerts surfaced at the HCP profile level, powered by integration with market access data sources (MMIT API, CMS machine-readable files).
- **Medical Strategy Digest:** Weekly AI-synthesized report surfacing cross-MSL insight themes, emerging HCP needs, and competitive signals for Medical Affairs leadership.
- **FHIR-Native Clinical Integration:** Read access to trial enrollment and site performance data via FHIR R4 for MSLs assigned to investigator sites.
- **Compliance-First Architecture:** Audit logging, human-in-the-loop review for flagged content, role-based access control, and GDPR/HIPAA-compliant data handling throughout.

---

### Success Metrics

| Metric | Baseline (Pre-Launch) | v1.0 Target (90 Days Post-Launch) |
|---|---|---|
| MSL insight capture time per HCP interaction | ~15–20 minutes (manual) | ≤ 3 minutes (AI-assisted) |
| Insight record completeness score (required fields populated) | ~45% | ≥ 85% |
| Payer context view adoption (% of MSL-HCP interactions with payer card opened) | 0% (no feature) | ≥ 60% of active users |
| Medical Affairs director weekly digest engagement (open rate) | N/A | ≥ 70% |
| Veeva CRM sync error rate | N/A | < 0.5% of submissions |
| Compliance flag rate (flagged insights reviewed before submission) | N/A | 100% of flagged insights reviewed |
| Enterprise customer NPS (MSL platform module) | Baseline TBD | ≥ 45 |

---

### Out of Scope — v1.0

- **Autonomous AI MSL agents** (digital humans conducting HCP conversations without an MSL present) — this is a v2+ capability requiring additional regulatory review.
- **Two-way FHIR write access** (writing data back to hospital EHRs) — read-only in v1.0; write access requires per-site data governance agreements.
- **Full eCTD / regulatory submission integration** — out of scope for MSL product; handled separately by clinical operations team.
- **Non-Veeva CRM platforms** (e.g., Salesforce Health Cloud standalone, Microsoft Dynamics) — Veeva CRM is v1.0 only; additional CRM support is v2 based on customer demand.
- **AI-generated medical information responses** (auto-drafting responses to HCP medical inquiries) — requires separate medical/regulatory review and is a distinct product workstream.
- **Patient-facing features** — this product serves MSLs and Medical Affairs staff only; patient engagement is a separate product domain.
