# Advanced AI — Requirements Package
**Date:** 2026-11-09  
**Prepared by:** PM, Third-Party Integrations & MSL Products  
**Based on:** Market Analysis 2026-11-09

---

## Feature Opportunity: CRM-Agnostic MSL Integration Hub with Governed AI Content Co-Pilot

### Why This Opportunity

The market analysis identifies two converging forces:

1. **CRM platform consolidation risk:** Veeva's Salesforce exit (2026–2029) leaves thousands of MSL teams uncertain about their data infrastructure. Neither Veeva nor Salesforce offers a neutral field analytics layer.
2. **Governed AI content delivery gap:** Syneos's AI MSL is powerful but locked inside a CRO services bundle. No standalone platform provides a compliance-first, source-traceable AI content overlay for MSL field work.

ADVANCE AI's unique position — purpose-built field engagement tracking with the proprietary APEX Sentiment Score — is the right foundation to become the CRM-agnostic connective layer MSL teams need during this period of platform disruption. Adding a governed AI Content Co-Pilot elevates the platform from analytics reporting to active workflow enablement.

**Target Personas:**
- **Field MSL** — Needs scientific evidence and approved claims surfaced pre-call without leaving their workflow
- **MSL Manager / Medical Affairs Leader** — Needs performance benchmarks and sentiment trends across the team, regardless of CRM
- **IT / Integration Manager at pharma** — Needs FHIR-compliant, audit-ready connectors that satisfy compliance and security requirements
- **Compliance / Regulatory Affairs Officer** — Needs source traceability and human-review gates on all AI-generated content

---

## User Stories

### Story 1: CRM Connector — Field MSL

**As a** field Medical Science Liaison working in a Veeva Vault CRM environment,  
**I want** my ADVANCE AI engagement data (HCP visit logs, APEX scores, follow-up tasks) to sync automatically with my Veeva Vault CRM records,  
**so that** I don't have to enter data twice and my manager has a single source of truth for my field activity.

#### Acceptance Criteria

**Given** I am authenticated in both ADVANCE AI and Veeva Vault CRM,  
**When** I log an HCP engagement in ADVANCE AI,  
**Then** the engagement record (date, HCP ID, topic, APEX score, follow-up flag) is written to the corresponding Vault CRM call record within 5 minutes via the Veeva Vault REST API, with no manual action required from me.

**Given** the Vault CRM sync is active,  
**When** a Vault CRM record for an HCP is updated by another team member (e.g., a commercial rep),  
**Then** the update is surfaced as a notification in my ADVANCE AI HCP profile within 15 minutes.

**Given** a sync error occurs (API timeout, auth failure),  
**When** the error is detected,  
**Then** the failed record is queued for retry (up to 3 attempts, exponential backoff) and I receive an in-app notification with the error detail and a manual retry option.

---

### Story 2: Governed AI Content Co-Pilot — Field MSL Pre-Call Prep

**As a** field MSL preparing for an HCP meeting,  
**I want** an AI-generated pre-call brief that surfaces the most relevant approved scientific content for this HCP's clinical focus areas,  
**so that** I walk into every meeting fully prepared with on-label, compliance-approved talking points without spending 30+ minutes on manual literature searches.

#### Acceptance Criteria

**Given** I open the HCP profile for an upcoming meeting in ADVANCE AI,  
**When** I request a pre-call brief,  
**Then** the system generates a summary of ≤500 words that includes: (a) 3–5 approved scientific claims with source citations from the connected content library, (b) the HCP's specialty and recent prescribing signals (if FHIR data is available), and (c) suggested discussion topics based on past ADVANCE AI engagement history.

**Given** a pre-call brief is generated,  
**When** the brief contains any AI-generated claim,  
**Then** every claim is linked to its approved source document, and the brief displays a compliance banner ("Content AI-generated from approved library — human review required before HCP sharing").

**Given** no approved content is available for a topic,  
**When** I request a brief including that topic,  
**Then** the system surfaces a "No approved content available" indicator for that topic rather than generating unsourced claims.

---

### Story 3: FHIR Integration — IT / Integration Manager

**As an** IT / Integration Manager at a pharma company evaluating ADVANCE AI,  
**I want** ADVANCE AI to expose and consume FHIR R4-compliant APIs authenticated via SMART on FHIR,  
**so that** we can integrate ADVANCE AI with our EHR systems and existing data infrastructure without custom ETL development or compliance exceptions.

#### Acceptance Criteria

**Given** my organisation has an EHR system that supports FHIR R4 / SMART on FHIR (e.g., Epic, Oracle Health, athenahealth),  
**When** our admin configures the FHIR integration in ADVANCE AI,  
**Then** the system authenticates via SMART on FHIR OAuth 2.0 and can retrieve HCP-level FHIR resources (Practitioner, Organization, Observation) within the approved data scope.

**Given** FHIR data is retrieved,  
**When** it is surfaced within the ADVANCE AI MSL interface,  
**Then** the data is labelled with its source system, timestamp, and data classification, and no FHIR data is stored beyond the user's configured retention policy.

**Given** an audit request is raised,  
**When** compliance reviews ADVANCE AI's FHIR data access logs,  
**Then** a full audit trail is exportable in CSV or JSON showing every FHIR API call with timestamp, user, resource type, and access scope.

---

### Story 4: Performance Dashboard — MSL Manager

**As an** MSL Manager overseeing a team of 12 MSLs,  
**I want** a team-level performance dashboard that shows APEX Sentiment Score trends, HCP engagement frequency, and content usage by MSL,  
**so that** I can identify coaching opportunities, top performers, and content gaps without manually pulling reports from multiple systems.

#### Acceptance Criteria

**Given** I am logged in with manager-level permissions,  
**When** I open the Team Performance Dashboard,  
**Then** I see, for each direct report: (a) APEX Sentiment Score trend (trailing 30/60/90 days), (b) number of HCP engagements logged in the period, (c) top 3 content assets used, and (d) a "coaching flag" indicator if APEX score has declined >10% over 30 days.

**Given** I want to export team data for a Medical Affairs review,  
**When** I click Export,  
**Then** I can export a PDF or Excel report of the dashboard in ≤30 seconds, with no PHI or confidential HCP identifiers included unless I have explicit data export permission.

**Given** I manage MSLs across two CRM environments (Veeva Vault and Salesforce LSC),  
**When** I view the Team Performance Dashboard,  
**Then** ADVANCE AI aggregates engagement data from both CRM connectors into a unified view with a CRM-source label per record.

---

### Story 5: Compliance Audit Trail — Compliance Officer

**As a** Regulatory Affairs / Compliance Officer at a pharma company,  
**I want** every AI-generated content output in ADVANCE AI to have a full, exportable audit trail showing what AI generated, from which sources, and what human review actions were taken,  
**so that** we can demonstrate compliance with our Medical Affairs SOPs and pharmaceutical advertising regulations during internal audits and regulatory submissions.

#### Acceptance Criteria

**Given** an MSL uses the AI Content Co-Pilot to generate a pre-call brief or response,  
**When** the brief is generated,  
**Then** the system logs: (a) the prompt/request context, (b) the source documents referenced, (c) the AI model version used, (d) the timestamp, (e) the MSL user ID, and (f) any human review/approval action taken.

**Given** an audit is initiated,  
**When** the Compliance Officer accesses the AI Audit Log,  
**Then** they can filter by date range, user, content type, and approval status, and export a full log in CSV format within 60 seconds.

**Given** an MSL shares AI-generated content externally with an HCP (e.g., via email or printed document),  
**When** the share action occurs,  
**Then** the system requires an explicit human review confirmation before the share is completed, and records this confirmation in the audit log.

---

## One-Page Product Spec: CRM-Agnostic MSL Integration Hub & AI Content Co-Pilot

### Problem Statement

MSL teams are caught in a CRM platform transition (Veeva-to-Vault migration, 2026–2029) that creates data fragmentation and workflow disruption. Simultaneously, the demand for AI-generated scientific content support is growing, but pharma compliance teams cannot accept AI outputs without source traceability and human-review gates. ADVANCE AI risks being perceived as a siloed analytics tool rather than a core MSL workflow platform if it cannot integrate with the dominant CRM environments and provide governed AI content delivery.

### Proposed Solution

Build a **CRM Integration Layer** (Phase 1) and **Governed AI Content Co-Pilot** (Phase 2) that together position ADVANCE AI as the CRM-agnostic MSL operating system:

**Phase 1 — CRM Integration Layer (Q1 2027):**
- Pre-built bidirectional connectors for Veeva Vault CRM and Salesforce Life Sciences Cloud
- FHIR R4 / SMART on FHIR data ingestion module for EHR-sourced HCP signals
- Unified engagement data model across CRM sources
- Full audit-trail logging for all data flows

**Phase 2 — Governed AI Content Co-Pilot (Q2 2027):**
- Pre-call brief generator drawing from connected approved content libraries (Veeva Vault PromoMats, Salesforce DAM, or customer-uploaded corpora)
- Source-citation enforcement on all AI outputs
- Human-review gate before any AI content is flagged as shared
- Compliance audit log export (CSV/JSON/PDF)

### Success Metrics

| Metric | Target (12 months post-launch) |
|---|---|
| CRM integration adoption | ≥40% of enterprise accounts activate ≥1 CRM connector |
| AI Co-Pilot weekly active users | ≥60% of MSL-tier users generate ≥1 pre-call brief/week |
| Duplicate data entry reduction | MSL reported duplicate entry time reduced by ≥50% (survey) |
| Compliance audit pass rate | 100% of AI content outputs auditable; 0 compliance escalations from AI-generated content |
| Net Revenue Retention impact | NRR improvement ≥5pp in accounts using integration + Co-Pilot vs. analytics-only |
| Time-to-integration for new enterprise customers | ≤4 weeks from contract to first CRM connector live |

### Out of Scope (Phase 1 & 2)

- Native MSL training simulation / AI avatar features (separate roadmap item)
- Direct EHR write-back (read-only FHIR integration only)
- Consumer-facing or HCP-facing portals
- Real-time video/telehealth integration
- Automatic submission to regulatory agencies of AI-generated content
- Support for CRM platforms outside Veeva Vault and Salesforce LSC in Phase 1 (Dynamics 365 considered for Phase 3)

---

*Based on: Advanced AI Market Analysis 2026-11-09 | For internal PM use only*
