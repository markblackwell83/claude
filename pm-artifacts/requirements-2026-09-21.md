# Requirements Package: ADVANCE AI — MSL & Integrations Product
**Date:** 2026-09-21  
**Feature Opportunity:** Agentic Pre-Meeting Intelligence & Structured Insight Routing  
**Based on:** Advanced AI Market & Competitive Analysis (2026-09-21)

---

## Feature Opportunity: Identified from Market Analysis

**Core Finding:** MSLs spend 30–60 minutes per HCP meeting assembling information from 4–6 disparate systems (CRM, publication databases, internal content portals, EHR-linked signals, payer data). No current platform — including market leader Veeva — delivers a single agentic briefing and insight-capture workflow that is simultaneously compliance-wrapped, audit-trailed, and interoperable with existing pharma tech stacks.

**Why This Matters for ADVANCE AI's Role:**
The job description calls for a PM to own third-party integrations and MSL products. This opportunity sits directly at that intersection: it requires integrating EHR/CRM/publication data sources (integrations domain), delivers value directly to MSL users (MSL product domain), and creates a durable competitive differentiator that mid-market pharma cannot get from Veeva at current pricing.

**Personas:**
- **Field MSL** — Field-based medical science liaison visiting KOLs and HCPs
- **MSL Manager** — Regional or national MSL team lead managing compliance and performance
- **Medical Affairs Director** — Head of medical affairs overseeing insight strategy and cross-functional reporting
- **Integration/IT Stakeholder** — Pharma IT or commercial operations leads managing data infrastructure

---

## User Stories

### Story 1: Pre-Meeting Intelligence Brief
> **As a** Field MSL,  
> **I want** to receive an AI-generated briefing document before each scheduled HCP meeting — drawing from the HCP's recent publication activity, our prior interaction history, approved scientific content relevant to the meeting context, and available real-world clinical signals —  
> **so that** I can walk into every meeting prepared with tailored, compliant, evidence-backed talking points without spending time across multiple systems.

#### Acceptance Criteria

**Given** an MSL has a meeting scheduled in the calendar integration (Outlook/Google Calendar/Veeva CRM),  
**When** the meeting is 24 hours away,  
**Then** the system automatically generates a structured pre-meeting brief containing: (1) HCP profile summary, (2) last 3 interaction notes, (3) up to 5 relevant publications from the approved content library, (4) any open medical information requests from this HCP, and (5) suggested discussion themes aligned to the active product dossier.

**Given** the brief has been generated,  
**When** the MSL opens it in the mobile or web app,  
**Then** every content item includes a traceable source citation, and the brief is logged as "viewed" with a timestamp in the audit trail.

**Given** a content item in the brief falls outside the approved scientific content library,  
**When** the AI attempts to surface it,  
**Then** the item is flagged for Medical Affairs review and is not surfaced to the MSL until approved — the brief is delivered without that item and includes an "awaiting approval" notice.

---

### Story 2: Structured Post-Meeting Insight Capture
> **As a** Field MSL,  
> **I want** to log meeting insights using a structured, AI-assisted capture form that classifies my notes by insight type (scientific question, competitive mention, unmet medical need, safety signal, reimbursement barrier) and routes them to the right team automatically,  
> **so that** I spend less time on administrative documentation and my insights actually reach the people who can act on them.

#### Acceptance Criteria

**Given** an MSL completes a meeting,  
**When** they open the post-meeting capture screen (web or mobile),  
**Then** the system presents a structured form with free-text and voice-to-text input, and the AI classifies each captured insight into one of 5 predefined categories within 10 seconds of submission.

**Given** a submitted insight is classified as a "safety signal" (AE-adjacent),  
**When** the classification is confirmed by the MSL or auto-classified with >90% confidence,  
**Then** the insight is immediately routed to the pharmacovigilance team via the configured integration (email/Slack/JIRA/Vault) and a compliance acknowledgment receipt is generated and stored.

**Given** any post-meeting note is submitted,  
**When** it is saved to the system,  
**Then** it is stored in the audit log with: submitting user ID, timestamp, meeting ID, classification, routing action taken, and the full original text — and this record cannot be edited or deleted by the MSL.

---

### Story 3: Third-Party CRM Sync for MSL Interactions
> **As an** Integration/IT Stakeholder at a pharma company,  
> **I want** ADVANCE AI to sync MSL interaction records bidirectionally with our existing Salesforce or Veeva CRM,  
> **so that** our commercial and medical affairs teams have a single source of truth for HCP engagement data without requiring MSLs to double-enter information.

#### Acceptance Criteria

**Given** a pharma company has configured a Salesforce or Veeva CRM integration via ADVANCE AI's integration settings panel,  
**When** an MSL submits a meeting record in ADVANCE AI,  
**Then** the record is synced to the CRM within 60 seconds as a new Activity/Interaction object, with field mapping maintained per the configured schema.

**Given** a CRM interaction record is updated externally (e.g., by a commercial rep),  
**When** the update involves a field mapped to ADVANCE AI's HCP profile,  
**Then** the change is reflected in ADVANCE AI's HCP record within 5 minutes via webhook or polling mechanism.

**Given** a sync attempt fails (network error, auth expiry, schema mismatch),  
**When** the failure occurs,  
**Then** the system retries up to 3 times with exponential backoff, logs the failure with error details, and sends an alert to the configured integration admin — without data loss.

---

### Story 4: Agentic Insight Summary for Medical Affairs Director
> **As a** Medical Affairs Director,  
> **I want** a weekly AI-generated summary of all field insights captured by my MSL team, organized by insight category, product, and geography,  
> **so that** I can identify emerging trends, unmet needs, and safety signals across the field without reading hundreds of individual notes.

#### Acceptance Criteria

**Given** it is Monday morning (configurable schedule),  
**When** the weekly digest agent runs,  
**Then** a structured report is delivered via email and in-app, containing: (1) total interactions logged, (2) top 5 themes per product by insight category, (3) safety signal count with a link to detail, (4) geographic activity heatmap, and (5) AI-identified "emerging trends" — patterns that increased >20% week-over-week.

**Given** the weekly digest contains a safety signal summary,  
**When** the Director views it,  
**Then** they are able to click through to the full, audit-logged original insight records without leaving the app.

**Given** the Director wants to export the digest,  
**When** they click "Export",  
**Then** a PDF and CSV of the full report are generated and available for download within 30 seconds.

---

### Story 5: FHIR-Compliant EHR Signal Integration for MSL Context
> **As a** Field MSL,  
> **I want** to see relevant, de-identified clinical signals from the HCP's patient population (e.g., disease prevalence, treatment patterns, guideline adherence rates) pulled from EHR data via FHIR integration — displayed in the HCP profile,  
> **so that** I can have scientifically relevant, data-informed conversations about unmet needs in the HCP's actual patient population rather than relying on generic epidemiology data.

#### Acceptance Criteria

**Given** a pharma company has configured a FHIR R4 EHR data integration,  
**When** an MSL views an HCP's profile,  
**Then** the profile displays an "HCP Practice Signals" panel showing: patient population metrics (condition prevalence, diagnosis codes, prescribing volume) derived from permitted, de-identified FHIR data, refreshed no less than weekly.

**Given** FHIR data is displayed,  
**When** any patient-level data is requested,  
**Then** the system returns only aggregate, de-identified population statistics — never individual patient records — and all FHIR queries are logged in the audit trail with data source, query timestamp, and fields accessed.

**Given** the FHIR data source becomes unavailable or returns stale data (>7 days),  
**When** the MSL views the HCP profile,  
**Then** a visible "Data last updated: [date]" indicator is shown and the signals panel displays a staleness warning.

---

## One-Page Product Spec: MSL Agentic Intelligence Hub

### Problem Statement

Medical Science Liaisons are the most strategically important field function in pharma medical affairs, yet they are paradoxically the most administratively burdened. A typical MSL spends 30–60% of available meeting preparation time aggregating information from 4–6 disconnected systems (CRM, internal content portals, PubMed/approved publication databases, EHR signals, payer data). Post-meeting, insights are captured inconsistently in free-text notes, rarely classified or routed, and frequently lost before they can inform commercial, HEOR, or pharmacovigilance workflows.

Current platforms (Veeva, S2N RepSignal, Sageforce AI MSL) address parts of this problem but not the integration layer that makes the data useful in real time. No mid-market-accessible platform today delivers: (1) a pre-meeting agentic briefing that pulls from approved scientific content + CRM + EHR signals, (2) structured insight capture with automatic classification and cross-team routing, and (3) bidirectional CRM sync — all within a single compliance-wrapped, audit-trailed platform.

### Proposed Solution

Build the **MSL Agentic Intelligence Hub** as the core product for ADVANCE AI's MSL product line. This is a two-sided platform: the **field layer** (pre-meeting brief agent, post-meeting insight capture, mobile-optimized UX) and the **integration layer** (FHIR EHR connectors, Salesforce/Veeva CRM sync, approved content library RAG pipeline, pharmacovigilance routing).

Key components:
- **Pre-Meeting Brief Agent:** Automated, AI-generated meeting prep document delivered 24h before scheduled HCP meetings. Pulls from approved content library (RAG), CRM history, EHR signals (FHIR), and open MI requests. Fully audit-logged.
- **Structured Insight Capture:** Post-meeting mobile-first capture with AI classification (5 insight types), auto-routing to downstream teams, and immutable audit records.
- **Integration Hub:** Pre-built connectors for Salesforce, Veeva Vault CRM, Epic (FHIR R4), and Medidata. Low-code connector builder for additional sources.
- **Director Digest Agent:** Weekly agentic summary of field insights by product, category, and geography for medical affairs leadership.

### Success Metrics

| Metric | Baseline (at launch) | Target (12 months) |
|---|---|---|
| Pre-meeting brief open rate (among eligible meetings) | 0% | ≥70% |
| MSL meeting prep time (self-reported, minutes) | ~45 min | ≤15 min |
| Post-meeting insight capture rate (structured vs. free-text) | <20% structured | ≥80% structured |
| Insight routing accuracy (correct team within 60s) | n/a | ≥90% |
| Safety signal escalation SLA (logged → routed, minutes) | untracked | ≤2 min, 100% |
| CRM sync success rate | n/a | ≥99.5% uptime |
| NPS from MSL users | n/a | ≥45 |
| Pharma companies with ≥1 active integration | 0 | ≥10 |

### Out of Scope (v1)

- Direct promotional content generation for commercial reps (medical affairs only; no off-label risk)
- Patient identity resolution or individual-level patient data display
- Real-time HCP chat or synchronous communication features
- Automated regulatory submission or eCTD filing
- Marketplace or third-party app store for external vendors
- HCP-facing portal or direct HCP communications
- Clinical trial site management or patient recruitment workflows (separate product line)
