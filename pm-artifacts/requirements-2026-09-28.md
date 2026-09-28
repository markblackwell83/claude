# Advanced AI — Requirements Package
**Date:** 2026-09-28  
**Feature Opportunity:** Compliance-Grade Third-Party Integration Hub + Agentic MSL Pre-Call Brief  
**Source:** Derived from Market Analysis (2026-09-28)  
**Prepared for:** Lead Product Manager, Advanced AI

---

## Feature Opportunity: MSL Agentic Workflow Hub with Certified Integration Layer

### Why This Opportunity
Market analysis identified two converging gaps that align directly with the PM role scope:

1. **Integration gap:** No platform offers a pre-validated, compliance-grade integration hub connecting MSL workflows to EHRs (Epic/Oracle Health via FHIR R4), CRMs (Veeva, Salesforce), and medical information systems out of the box. Healthcare IT integration spend hit $5.8B in 2026, yet MSL-specific integration remains bespoke and expensive.

2. **Agentic workflow gap:** The dominant CRM vendors (Veeva, Salesforce) offer general-purpose AI agents that are not purpose-built for scientific exchange or MSL compliance requirements. Pure-play MSL tools (TikaMSL, Sorcero) are gaining ground but lack robust integration ecosystems.

Advanced AI has the opportunity to own the intersection: a governed agentic MSL workflow layer with a certified, expanding integration marketplace—exactly matching the "third-party integrations and MSL products" dual charter described in the job posting.

---

## User Stories and Acceptance Criteria

---

### Story 1: FHIR-Native EHR Integration for MSL Field Teams

**As an** MSL field representative,  
**I want** real-time access to a HCP's recent clinical activity (prescribing patterns, relevant patient population data) pulled directly from their hospital's EHR via a FHIR R4 connection,  
**so that** I can enter each scientific exchange informed by current clinical context rather than stale CRM data.

#### Acceptance Criteria

**Given** an MSL is preparing for a meeting with a KOL/HCP whose institution is connected via a certified FHIR R4 integration,  
**When** the MSL opens the pre-call brief view in the Advanced AI platform,  
**Then** the system displays a synthesized summary of the HCP's relevant clinical activity (last updated ≤24 hours), sourced from the EHR integration, alongside the MSL's prior engagement history from CRM—with data provenance labels visible for each data source.

**Given** the integration retrieves clinical data,  
**When** any patient-identifiable information is included in the FHIR response,  
**Then** the system must de-identify or mask PHI per HIPAA Safe Harbor before displaying or storing the data, and log the retrieval event with timestamp and user ID in the audit trail.

**Given** an institution has not yet connected via FHIR,  
**When** the MSL views the brief for an HCP at that institution,  
**Then** the system displays a clear "EHR data unavailable — institution not yet integrated" notice and surfaces only approved internal data sources.

---

### Story 2: Agentic Pre-Call Brief Generation

**As an** MSL preparing for a KOL meeting,  
**I want** the platform to automatically generate a structured pre-call brief that synthesizes recent relevant publications, the KOL's research interests, prior engagement history, and real-world evidence signals,  
**so that** I spend less time on preparation and can focus my limited time on scientific discussion strategy.

#### Acceptance Criteria

**Given** a scheduled or saved meeting with a KOL in the platform,  
**When** the MSL requests a pre-call brief (or one is auto-generated 24 hours before a scheduled meeting),  
**Then** the system produces a brief within 60 seconds containing: (a) up to 5 curated recent publications relevant to the KOL's research area, sourced from the approved scientific library via RAG; (b) a summary of prior MSL interactions with this KOL; (c) recommended talking points derived from current approved content; (d) a flagged section for any open adverse event reports or unsolicited requests requiring follow-up.

**Given** the brief is generated,  
**When** any AI-generated text is included,  
**Then** every claim must be traceable to a source document in the approved library (citation link visible), and the brief must display a "reviewed by AI — requires MSL review before use" disclaimer.

**Given** the KOL has no prior engagement history in the system,  
**When** the brief is generated,  
**Then** the system must still produce a partial brief with publication synthesis and approved talking points, and display a notice that no prior engagement data is available rather than silently omitting the section.

---

### Story 3: Insight Capture with Adverse Event Passthrough

**As an** MSL completing a post-call report,  
**I want** the platform to automatically detect potential adverse event mentions in my free-text field notes and route them to the pharmacovigilance workflow,  
**so that** I can fulfill regulatory reporting obligations without a separate manual process or risk missing a reportable event.

#### Acceptance Criteria

**Given** an MSL submits a post-call report containing free-text notes,  
**When** the system's NLP pipeline processes the text,  
**Then** any phrase matching adverse event patterns (defined by the configured AE detection model and approved terminology list) must be flagged within 30 seconds, with the detected phrase highlighted and a prompt asking the MSL to confirm or dismiss the potential AE.

**Given** the MSL confirms an AE flag,  
**When** the confirmation is submitted,  
**Then** the system must create a structured AE record pre-populated with HCP identity, product, event description, and date, route it to the configured pharmacovigilance integration (e.g., Veeva Vault Safety or equivalent), and store the routing event with timestamp in the audit log—without requiring the MSL to re-enter data.

**Given** the MSL dismisses a flag,  
**When** the dismissal is submitted,  
**Then** the system must record the dismissed flag, the MSL's rationale (required free-text field), and timestamp in the audit log for compliance review.

---

### Story 4: Integration Marketplace Onboarding for Admins

**As a** Medical Affairs IT administrator at a pharma company,  
**I want** a self-service integration marketplace where I can browse, configure, and activate pre-built connectors (Veeva CRM, Epic FHIR, Salesforce, Vault Safety),  
**so that** I can reduce integration implementation time from months to days without requiring custom engineering work.

#### Acceptance Criteria

**Given** an admin user with "Integration Admin" role accesses the integration marketplace,  
**When** they browse the connector catalog,  
**Then** each connector must display: supported integration version (e.g., FHIR R4, Veeva API v24), compliance certifications (e.g., HIPAA, 21 CFR Part 11), estimated setup time, required credentials/permissions, and a link to the connector's audit trail schema.

**Given** an admin selects a connector and enters required credentials,  
**When** the admin runs the connection test,  
**Then** the system must return a pass/fail result within 30 seconds, display specific error codes and remediation guidance on failure, and not store credentials in plaintext (must use secrets management).

**Given** a connector is successfully activated,  
**When** data begins flowing,  
**Then** the system must generate an integration health dashboard entry for that connector showing: last sync timestamp, record volume, error rate (target <0.1%), and a status indicator—visible to the admin within the marketplace UI.

---

### Story 5: MSL Insight Analytics for Medical Affairs Leadership

**As a** VP of Medical Affairs,  
**I want** a real-time dashboard that aggregates and categorizes field insights captured by MSLs (KOL feedback, medical questions, competitive intelligence, unsolicited requests),  
**so that** I can identify emerging medical questions and evidence gaps that should inform publication planning and medical strategy.

#### Acceptance Criteria

**Given** MSL post-call reports have been submitted across the field team over the trailing 30 days,  
**When** the VP accesses the Medical Affairs Insights Dashboard,  
**Then** the dashboard must display: top medical questions by frequency (NLP-tagged), insight trend lines over time, geographic heatmap of activity, and a breakdown by therapeutic area—with data refreshed no less than every 4 hours.

**Given** the VP selects a specific insight category (e.g., "competitor product questions"),  
**When** drilling down,  
**Then** the system must display the individual anonymized insight records, their NLP-assigned tags, the originating HCP institution type (academic/community—not individual identity), and a confidence score for each tag.

**Given** the dashboard data is exported,  
**When** the VP exports to PDF or CSV,  
**Then** the export must exclude any data fields that could identify individual HCPs or MSLs by name, and must include a data classification label ("Internal — Medical Affairs Confidential") on every exported page or file.

---

## One-Page Product Spec: Agentic MSL Workflow Hub

### Problem Statement
MSLs spend 30–40% of their time on administrative preparation and compliance documentation rather than scientific exchange. Existing CRM platforms (Veeva, Salesforce) are not purpose-built for scientific engagement, and purpose-built MSL tools lack the integration depth to pull real-time clinical and payer signals. Meanwhile, regulatory scrutiny of AI-generated content in pharma is rising, creating risk for teams that adopt general-purpose AI tools without proper governance. The result: MSLs are under-equipped, over-burdened, and operating without the full clinical context their HCP partners expect.

### Proposed Solution
Launch the **Advanced AI MSL Workflow Hub**: a governed agentic layer within the Advanced AI platform that:

1. **Connects** to EHRs (FHIR R4), CRMs (Veeva/Salesforce), and pharmacovigilance systems via a self-service certified integration marketplace.
2. **Generates** AI-native pre-call briefs using RAG over the customer's approved scientific library, with full citation provenance and a mandatory MSL review gate before use.
3. **Captures** field insights with NLP-powered tagging, adverse-event detection with automatic pharmacovigilance passthrough, and closed-loop analytics for MA leadership.
4. **Governs** every AI action with immutable audit logs, human-in-the-loop content approval, and PHI de-identification—meeting HIPAA and 21 CFR Part 11 requirements out of the box.

### Success Metrics

| Metric | Baseline (today) | Target (12 months post-launch) |
|---|---|---|
| MSL call preparation time | ~45 min/call | ≤30 min/call (33% reduction) |
| Integration onboarding time (new connector) | 8–16 weeks (custom eng) | ≤5 business days (self-service) |
| Adverse event detection miss rate | Manual / unmeasured | <2% miss rate (NLP-detected) |
| MSL field insight utilization by MA leadership | Ad hoc / low | Weekly dashboard consumption by >80% of MA VPs |
| Platform NPS (MSL users) | Baseline TBD at launch | ≥45 |

### Out of Scope (v1)
- Promotional content generation (strictly separated from medical workflows)
- Native video/telemedicine calling features (leverage existing solutions)
- Direct HCP-facing patient portal features
- Payer/reimbursement analytics (see MMIT partnership opportunity in Year 2)
- Multi-tenant data sharing between competing pharma clients
- AI model fine-tuning by end-users (RAG only; no customer-side model training in v1)
