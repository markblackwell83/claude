# Requirements Package: Advanced AI – MSL & Third-Party Integrations
**Date:** 2026-10-12  
**Prepared by:** PM Assistant (Senior Health Tech AI Analyst)  
**Derived from:** Market Analysis 2026-10-12

---

## Feature Opportunity: EHR-Integrated MSL Engagement Intelligence

### Why This Opportunity

The market analysis identified a clear gap at the intersection of three converging forces:

1. **27% of MSLs use AI for KOL engagements** but lack a system that surfaces real-time clinical context (formulary status, trial enrollment, prescriber EHR activity) during field interactions.
2. **EHR interoperability (FHIR/SMART) is now regulatory expectation**, but no MSL platform has made FHIR-native clinical data a native part of the MSL workflow—Veeva and Salesforce offer CRM-side data, not clinical-side context.
3. **The Veeva–Salesforce migration window (2025–2030)** gives ADVANCE AI a rare chance to win mid-market accounts during a forced platform evaluation cycle.

The feature opportunity is a **Clinical Context Engine**: a FHIR-compliant integration layer that pulls relevant EHR signals (recent prescribing patterns, open clinical trials, payer formulary coverage) and surfaces them as pre-meeting briefs and post-meeting summaries inside the MSL's existing workflow.

---

## User Stories

### Story 1: Pre-Meeting Clinical Brief (MSL Field User)

**As a** Medical Science Liaison preparing for a KOL meeting,  
**I want** an automatically generated clinical brief that combines the physician's recent prescribing activity (from EHR), current formulary access for our product, and relevant published evidence,  
**so that** I can enter every interaction with contextually relevant talking points without spending 45–60 minutes on manual research.

#### Acceptance Criteria

**Given** an MSL has a meeting scheduled in the next 48 hours,  
**When** the MSL opens the interaction record in the platform,  
**Then** the system automatically generates a Clinical Brief containing: (1) the KOL's last 90-day prescribing volume for the relevant indication from connected EHR/claims data, (2) current payer formulary tier and prior authorization requirements for the MSL's product, and (3) the top 3 most-cited recent publications for the relevant indication—all surfaced without requiring manual search.

**Given** the EHR data source is unavailable or the data feed is stale (>48h),  
**When** the brief is generated,  
**Then** the system displays a data freshness indicator and a fallback message explaining which data source is unavailable, without suppressing the rest of the brief.

**Given** the KOL has opted out of data sharing under applicable privacy regulations,  
**When** a brief is requested for that KOL,  
**Then** the system omits prescribing-level data and displays a compliant notice, but still surfaces formulary and evidence content.

---

### Story 2: Post-Interaction AI Summary (MSL Field User)

**As a** Medical Science Liaison who has just completed a KOL interaction,  
**I want** the platform to generate a structured interaction summary with flagged follow-up actions,  
**so that** I can complete my compliance documentation in under 5 minutes and never miss a medical information request or escalation trigger.

#### Acceptance Criteria

**Given** an MSL completes an interaction and taps "End Interaction" in the app,  
**When** the interaction session closes,  
**Then** the platform generates a structured summary within 60 seconds containing: (1) interaction type, duration, attendees, (2) AI-extracted key discussion topics mapped to the product label, (3) flagged medical information requests requiring Medical Affairs follow-up, and (4) suggested next-interaction date based on engagement cadence.

**Given** the auto-generated summary is presented to the MSL,  
**When** the MSL reviews and edits the summary,  
**Then** every human edit is timestamped, attributed to the MSL, and preserved alongside the original AI-generated text in the audit log—maintaining regulatory traceability.

**Given** the AI identifies a potential adverse event mention in the interaction notes,  
**When** the summary is generated,  
**Then** the system automatically flags the record for Pharmacovigilance review, pre-fills a PV intake form with extracted details, and notifies the assigned PV contact within 15 minutes.

---

### Story 3: Compliance Administrator Governance Dashboard (Medical Affairs Ops / Compliance)

**As a** Medical Affairs Operations Manager responsible for AI governance,  
**I want** a centralized dashboard that shows how AI is being used across all MSL interactions—including what AI generated, what humans edited, and what was submitted to compliance systems—  
**so that** I can demonstrate to Legal and Regulatory Affairs that our AI use meets audit requirements and internal policy controls.

#### Acceptance Criteria

**Given** AI-generated content (briefs, summaries, suggested actions) exists in the system,  
**When** a compliance admin opens the Governance Dashboard,  
**Then** the dashboard displays: (1) total AI-generated vs. human-edited records for a configurable date range, (2) edit rate and delta between AI output and final submission by field, (3) flagged records where AI output differed significantly (>30% edit) from submitted content, and (4) a drill-down to the full audit trail for any individual record.

**Given** the organization has configured AI use policies (e.g., "AI summaries require MSL approval before submission"),  
**When** an MSL attempts to submit an AI-generated record without the required approval step,  
**Then** the system blocks submission and presents the policy requirement in context, with a one-click escalation path to a manager override.

---

### Story 4: Third-Party Integration Setup (IT Admin / Implementation)

**As a** health system IT Administrator onboarding ADVANCE AI,  
**I want** a guided integration wizard that connects our Epic EHR instance to the platform using SMART on FHIR 2.0,  
**so that** our MSL team can access clinical context without IT having to write or maintain custom integration code.

#### Acceptance Criteria

**Given** an IT Admin begins a new integration in the ADVANCE AI admin portal,  
**When** they select "Epic EHR" as the source system,  
**Then** the wizard guides them through OAuth 2.0 app registration, FHIR scope selection (prescribing data, patient demographics, formulary), and a test-connection validation—completing setup in under 2 hours with no custom code required.

**Given** the FHIR connection is established,  
**When** the admin runs a connection health check,  
**Then** the system returns a status report showing: data source name, last successful sync timestamp, record volume synced in the last 24h, and any permission or scope errors—displayed in plain language without requiring FHIR expertise to interpret.

**Given** the EHR integration is active and a FHIR API breaking change is detected,  
**When** the system detects schema mismatch or authentication failure,  
**Then** an automated alert is sent to the IT Admin and the ADVANCE AI Customer Success team within 15 minutes, with diagnostic detail sufficient to triage without escalating to engineering.

---

### Story 5: Sales-Facing Integration Capabilities Summary (Internal Sales / Pre-Sales)

**As a** ADVANCE AI Account Executive in a prospect conversation,  
**I want** a real-time, always-current view of which EHR and third-party data integrations are certified and in production,  
**so that** I can accurately represent integration capabilities to prospects without waiting for a technical resource and without accidentally over-promising features that are still in development.

#### Acceptance Criteria

**Given** a Sales rep opens the Integration Catalog in the internal ADVANCE AI portal,  
**When** they filter by "EHR" or "Payer Data" or "CRM,"  
**Then** the catalog returns a list of integrations with status labels (GA, Beta, Roadmap), last-validated date, supported FHIR version, and a one-sentence capability description—updated automatically when engineering marks a release as deployed.

**Given** a prospect asks about a specific integration not yet in the catalog,  
**When** the Sales rep submits an integration request via the catalog,  
**Then** Product receives a structured intake form with prospect name, use case, and urgency score, and the rep receives an estimated response time within 1 business day.

---

## One-Page Product Spec: Clinical Context Engine

### Problem Statement

MSLs spend 45–90 minutes per interaction on manual research—pulling prescribing data, checking formulary access, reviewing recent publications—using disconnected tools (spreadsheets, PDF slide decks, separate CRM, manual PubMed searches). This preparation burden limits interaction quality, reduces field productivity, and introduces compliance risk when interactions are not properly documented. At the same time, the clinical and payer data needed to personalize MSL interactions already exists in enterprise systems (EHRs, payer databases, medical literature APIs)—it is simply not accessible in the MSL's workflow at the moment of need.

### Proposed Solution

A **Clinical Context Engine** embedded in ADVANCE AI's existing MSL interaction workflow that:

1. **Pre-Meeting Brief** – Auto-generates a structured pre-meeting brief (prescribing context, formulary status, key publications) using FHIR API connections to certified EHR and payer data sources. Available 48 hours before scheduled interactions, accessible in-app and via mobile.

2. **AI Interaction Summary** – Post-interaction transcription and structured summary with auto-extracted follow-up flags (medical information requests, adverse event detection, next-step recommendations), with full MSL edit history preserved in the audit trail.

3. **Governance Layer** – Compliance dashboard with AI-vs-human edit analytics, policy enforcement controls (block submission without approval), and exportable audit logs for regulatory review.

4. **Integration Wizard** – Guided SMART on FHIR 2.0 connector setup for Epic, Oracle Health, and athenahealth—no custom code required, target <2 hour setup time for qualified IT admin.

### Success Metrics

| Metric | Baseline (Current) | Target (6 months post-launch) |
|---|---|---|
| Avg. MSL pre-meeting research time | 45–90 min | <10 min |
| Interaction documentation completion rate | ~65% (industry estimate) | >90% |
| Time to complete post-interaction summary | 20–30 min | <5 min |
| Adverse event flag response time | 24–48h manual | <15 min automated |
| EHR integration setup time (IT admin) | 4–8 weeks custom dev | <2 hours wizard |
| Compliance audit prep time (quarterly) | ~3 days manual | <4 hours dashboard export |
| Win rate in competitive deals vs. Veeva mid-market | Baseline TBD | +15 pp vs. Veeva in sub-500-person pharma |

### Out of Scope (v1)

- Direct EHR write-back (read-only integration only in v1)
- Automated KOL tier scoring / segmentation model (separate backlog initiative)
- Integration with non-FHIR legacy lab systems
- Multi-language clinical brief generation (English only in v1)
- Full MSL call planning / territory management (existing CRM handles this)
- Consumer-facing patient portals or patient data collection

---

*Analysis basis: ADVANCE AI job description; Market Analysis 2026-10-12 (this package); PubMed MSL AI adoption survey; Veeva/Salesforce Life Sciences Cloud competitive coverage; ONC SMART on FHIR 2.0 regulatory guidance; MMIT Mosaic/Ella AI product research.*
