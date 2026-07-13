# Requirements Package — MSL Integration Intelligence
**Date:** 2026-07-13
**Prepared for:** ADVANCE AI Product Team
**Feature Domain:** Third-Party Integrations & MSL Products
**Derived from:** Market Analysis 2026-07-13

---

## Feature Opportunity

**Contextual MSL Briefing Engine with Third-Party Data Integration**

Market research reveals that the most significant unaddressed gap in the MSL tooling space is the absence of a real-time, compliance-aware intelligence briefing that synthesizes third-party data (EHR/FHIR, payer formulary, real-world evidence, patient voice) directly into an MSL's pre-engagement workflow. Veeva's Pre-call Agent (launched Dec 2025) addresses internal CRM data only. MMIT and Semalytix serve research and market access teams — not field medical. No platform assembles a unified, compliant HCP dossier from heterogeneous external sources at the moment the MSL needs it.

ADVANCE AI's position at the intersection of third-party integrations and MSL products makes this the highest-leverage feature to build. It converts the integrations capability into MSL workflow value, creates data-network effects as more connectors are added, and establishes a compliance-forward moat that enterprise buyers require.

**Target Personas:**
- **MSL (Medical Science Liaison):** Field-based PhD/PharmD professionals conducting scientific exchange with KOLs and HCPs
- **Medical Affairs Director:** Oversees MSL team strategy, insight aggregation, and compliance governance
- **Integration/IT Lead (Pharma):** Responsible for connecting ADVANCE AI to internal systems (CRM, EHR, payer data vendors)

---

## User Stories

---

### Story 1: Pre-Engagement Smart Briefing

**As an** MSL preparing for an HCP meeting,
**I want** an AI-generated briefing document assembled from my HCP's profile, relevant recent publications, active payer restrictions on my product, and patient-reported experience data,
**so that** I can walk into every scientific exchange well-prepared without spending 45+ minutes manually aggregating information from multiple systems.

#### Acceptance Criteria

**Scenario: Briefing auto-generated before scheduled meeting**
- **Given** an MSL has a CRM-scheduled HCP meeting within the next 24 hours
- **When** the system detects the upcoming meeting via calendar/CRM integration
- **Then** a Smart Briefing is automatically generated and delivered to the MSL's mobile app and email at least 60 minutes before the meeting start time

**Scenario: Briefing includes integrated third-party data**
- **Given** the MSL's organization has active connectors for payer data (e.g., MMIT) and literature feeds
- **When** the Smart Briefing is generated
- **Then** it includes: (a) HCP's recent publication activity and therapeutic area focus; (b) current payer formulary coverage status for ADVANCE AI products in the HCP's region; (c) relevant patient-reported experience summaries from active RWE connectors; and (d) the MSL's own prior interaction history with this HCP

**Scenario: Briefing flagged for MLR review when required**
- **Given** the briefing includes data from a connector flagged as requiring MLR clearance (e.g., off-label adjacent content)
- **When** the briefing is generated
- **Then** the flagged section is watermarked as "Pending MLR Review" and the MSL is notified that the section requires review before use in field engagement

---

### Story 2: FHIR-Compliant EHR Connector Setup

**As an** integration/IT lead at a pharma company,
**I want** to configure a certified FHIR R4 connector between ADVANCE AI and our EHR system (Epic, Cerner, or equivalent) using a guided, no-code setup flow,
**so that** MSLs can receive HCP-relevant patient-population data without requiring a custom engineering engagement.

#### Acceptance Criteria

**Scenario: Successful connector configuration**
- **Given** an admin user has appropriate EHR API credentials and FHIR R4 endpoint URL
- **When** they complete the ADVANCE AI Connector Setup wizard
- **Then** the connector is active within 30 minutes with a green status indicator, and a test data pull returns a sample patient cohort summary with no PII exposed at the MSL view layer

**Scenario: Data access scope enforcement**
- **Given** a FHIR R4 connector is active
- **When** MSL-facing views are generated from EHR data
- **Then** all data is de-identified and aggregated to population-level (no individual patient records are surfaced to the MSL), and an audit log entry is created for every data pull with timestamp, requesting user, and data scope

**Scenario: Connector health monitoring**
- **Given** an active EHR connector
- **When** the connection fails or the data refresh is delayed beyond 4 hours
- **Then** the admin contact receives an automated alert with the error type and recommended resolution steps, and affected briefings are flagged with a "Data may be outdated" banner

---

### Story 3: MSL Field Insight Capture with Compliance Triage

**As an** MSL completing an HCP interaction,
**I want** to record my field insights via voice or structured form immediately after the meeting, with the system automatically categorizing and routing insights that require MLR or safety review,
**so that** my insights contribute to the organization's medical intelligence pipeline without burdening me with manual categorization or creating compliance risk.

#### Acceptance Criteria

**Scenario: Voice-to-insight transcription**
- **Given** an MSL activates the "Capture Insight" mode in the mobile app after completing a meeting
- **When** they speak a free-form verbal debrief (up to 5 minutes)
- **Then** the system produces a structured insight record within 2 minutes, categorized into: (a) HCP sentiment; (b) scientific feedback; (c) adverse event mention (if any); (d) market access observation; and (e) follow-up action items

**Scenario: Automatic adverse event escalation**
- **Given** an MSL submits an insight that contains language matching adverse event detection criteria
- **When** the system processes the insight
- **Then** a pharmacovigilance alert is automatically generated and routed to the designated safety reporting workflow within 15 minutes, and the MSL receives a confirmation notification that the report was escalated

**Scenario: Insight contributes to aggregated intelligence**
- **Given** multiple MSLs submit insights about the same therapeutic area or HCP-raised topic
- **When** 3 or more insights share a tagged theme within a 14-day rolling window
- **Then** the system surfaces a trend alert to the Medical Affairs Director dashboard, with supporting insight excerpts (anonymized by MSL) and suggested follow-up actions

---

### Story 4: Payer Intelligence Integration for MSL Scientific Exchange Prep

**As an** MSL preparing for engagement with an HCP in a market-access-complex account (e.g., an IDN or hospital system),
**I want** to see the current formulary status, prior authorization requirements, and recent coverage changes for my products at the payer level relevant to that HCP's patient population,
**so that** I can proactively address reimbursement barriers during scientific exchange and provide the HCP with accurate access context.

#### Acceptance Criteria

**Scenario: Payer data visible in HCP profile**
- **Given** the MMIT (or equivalent) payer data connector is active and the HCP's affiliated payer mix is populated
- **When** the MSL views the HCP profile
- **Then** they see a "Coverage Snapshot" section showing: product coverage tier, PA requirements, any step-therapy edits, and date of most recent payer policy change — for the top 3 payers in the HCP's coverage mix

**Scenario: Coverage alert for significant policy change**
- **Given** a payer changes coverage policy (PA requirement added, tier change, coverage removal) for a tracked product
- **When** the payer data connector syncs the update
- **Then** all MSLs whose HCP territory includes that payer receive an in-app alert within 24 hours of the policy change, with a plain-language summary and suggested talking points

**Scenario: Data attribution and freshness disclosure**
- **Given** the MSL is viewing payer coverage data
- **When** data is displayed
- **Then** the source, last-refresh timestamp, and a disclaimer noting that coverage data should be verified with payer directly before use in formal reimbursement conversations are always visible alongside the data

---

### Story 5: Medical Affairs Director — Insight Analytics Dashboard

**As a** Medical Affairs Director,
**I want** a consolidated view of field insights, HCP engagement frequency, trending scientific topics, and integration health across my MSL team,
**so that** I can identify strategic patterns, allocate MSL resources effectively, and demonstrate ROI of the medical affairs function to leadership.

#### Acceptance Criteria

**Scenario: Real-time insight trend visualization**
- **Given** MSLs have submitted insights over the past 30 days
- **When** the Medical Affairs Director opens the Analytics Dashboard
- **Then** they see a ranked list of top-5 trending themes by insight volume, with sparkline trend charts, geographic distribution by MSL territory, and drill-down to de-identified supporting insight excerpts

**Scenario: Integration health monitoring**
- **Given** multiple third-party data connectors are active
- **When** the Director opens the Integrations Health panel
- **Then** they see status (green/amber/red), last successful sync time, and data freshness score for each active connector, with a one-click path to alert the admin if any connector is degraded

**Scenario: Exportable report for leadership**
- **Given** a Director selects a date range and clicks "Generate Report"
- **When** the report is generated
- **Then** a PDF summary is produced within 60 seconds containing: total HCP interactions, unique HCPs engaged, top 5 insight themes, coverage alert actions taken by MSLs, and integration uptime — formatted for sharing with VP/C-suite stakeholders without requiring platform access

---

## One-Page Product Spec: Contextual MSL Briefing Engine

### Problem Statement

Medical Science Liaisons spend an average of 45–90 minutes preparing for each HCP meeting, manually pulling data from CRM, literature databases, internal slide decks, and market access systems that don't communicate with each other. Insight capture after meetings is inconsistently documented, creating compliance risk and preventing organizations from extracting strategic intelligence from field interactions. As Veeva and Salesforce embed native AI agents into their ecosystems, ADVANCE AI risks being positioned as a data-poor point solution if it does not establish deep integration connectivity and contextual AI value for MSLs before 2027.

### Proposed Solution

Build the **ADVANCE AI Contextual Briefing Engine**: a real-time, compliance-aware intelligence layer that:

1. **Connects** to third-party data sources via FHIR R4 (EHR), payer intelligence APIs (MMIT/equivalent), RWE/patient-voice feeds (Semalytix-compatible), and internal CRM through a pre-certified connector marketplace.
2. **Synthesizes** a Smart Briefing per HCP meeting — automatically assembled and delivered 60 minutes before engagement — combining HCP profile, recent publications, payer coverage context, patient experience insights, and prior interaction history.
3. **Captures** field insights via voice or structured input post-meeting, with automatic adverse event detection, MLR routing, and theme aggregation for Medical Affairs leadership.
4. **Governs** all data flows with audit trails, de-identification at MSL view layer, MLR workflow integration, and a compliance health dashboard.

**MVP Scope (Q3–Q4 2026):** FHIR R4 EHR connector (Epic first), CRM calendar integration for briefing triggers, Smart Briefing generation (literature + CRM history), voice insight capture with AE detection. Payer intelligence and RWE connectors in Phase 2 (Q1 2027).

### Success Metrics

| Metric | Baseline (Pre-Launch) | 6-Month Target | 12-Month Target |
|---|---|---|---|
| MSL pre-meeting prep time | ~60 min/meeting | ≤ 20 min/meeting | ≤ 15 min/meeting |
| Insight capture completion rate | < 40% of meetings | ≥ 70% of meetings | ≥ 85% of meetings |
| Time from AE mention to safety report filed | > 24 hours | < 2 hours | < 30 minutes |
| Active third-party connectors per customer | 0 | ≥ 2 connectors/customer | ≥ 4 connectors/customer |
| MSL satisfaction score (CSAT) | TBD at baseline | ≥ 4.0/5.0 | ≥ 4.3/5.0 |
| Customers with ≥1 EHR connector active | 0 | 3 pilot customers | 10 customers |

### Out of Scope (Phase 1)

- Direct-to-HCP AI communication (digital human MSL functionality)
- Drug discovery or clinical trial management workflows
- Commercial sales force automation (separate from medical affairs)
- Non-FHIR legacy EHR integration methods (HL7 v2, custom EDI)
- Multilingual briefing generation (English-first MVP)
- Patient-level data surfacing to any user role (aggregate only, by design)
- Building a proprietary payer or RWE data set (connector/partnership model only)
