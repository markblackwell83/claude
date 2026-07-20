# Requirements Package: MSL Integration Hub & Copilot
**Date:** 2026-07-20  
**Product Domain:** Third-Party Integrations & MSL Products  
**Prepared for:** ADVANCE AI — Product Manager, Integrations & MSL Products  
**Linked Analysis:** `market-analysis-2026-07-20.md`

---

## Feature Opportunity: Neutral Integration Hub with Compliance-First MSL Copilot

### Market Signal
The Veeva-Salesforce CRM bifurcation (2026) has left pharma IT teams managing two parallel field platforms with no neutral integration layer. Simultaneously, agentic AI for MSL workflows is maturing but compliance infrastructure is inconsistently implemented across the vendor landscape. Mid-market pharma ($500M–$5B revenue) is priced out of IQVIA Expert Engagement and Veeva MedComms, yet faces the same regulatory and field complexity as top-20 pharma.

ADVANCE AI is uniquely positioned to own the integration middleware layer and deliver a compliance-first MSL Copilot — connecting to the customer's CRM of choice (Veeva or Salesforce), surfacing approved scientific content, flagging AEs, and generating field-ready intelligence — without competing with the CRM platforms themselves.

---

## User Stories

### Story 1: CRM-Agnostic Interaction Logging (Integration Core)

**As an** MSL,  
**I want** my post-HCP interaction notes synced automatically to my organization's CRM (Veeva Vault or Salesforce Agentforce) from a single ADVANCE AI interface,  
**so that** I can capture field intelligence once and have it reflected in both compliance records and CRM reporting without duplicate data entry.

#### Acceptance Criteria

**Given** an MSL is authenticated in ADVANCE AI and their org has a configured CRM connector (Veeva Vault CRM or Salesforce Agentforce Life Sciences),  
**When** the MSL submits a post-call interaction note via the ADVANCE AI mobile or web interface,  
**Then** the note is mapped to the correct CRM object schema (Activity, Medical Interaction, or equivalent), pushed to the connected CRM within 60 seconds, and a confirmation receipt with CRM record ID is displayed to the MSL.

**Given** the CRM API is temporarily unavailable,  
**When** the MSL submits a note,  
**Then** the note is queued locally (with a visible "sync pending" indicator), automatically retried on connectivity restoration, and the MSL receives a push notification when sync succeeds or fails after 3 attempts.

**Given** the MSL's organization has both a Veeva Vault and a Salesforce environment active (e.g., during a platform migration),  
**When** a note is submitted,  
**Then** the admin-configured primary target receives the sync, and a secondary sync to the other platform is available as an optional toggle per user session.

---

### Story 2: Approved-Content RAG for HCP Pre-Read Briefs (MSL Copilot)

**As an** MSL preparing for a KOL meeting,  
**I want** an AI-generated pre-read brief based solely on my company's approved scientific content library,  
**so that** I can prepare a compliant, personalized engagement plan in under 10 minutes without risk of off-label content.

#### Acceptance Criteria

**Given** an MSL initiates a pre-meeting brief request for a specific KOL and indication,  
**When** the ADVANCE AI copilot generates the brief,  
**Then** every claim in the brief is sourced exclusively from the organization's approved scientific content library (RAG-bounded), each claim includes a citation to the specific approved document and version, and no content from unapproved or external sources is included.

**Given** the KOL has recent publications or public congress presentations on the indication topic,  
**When** the brief is generated,  
**Then** the copilot includes a section summarizing the KOL's recent scientific positions based on their public publication history, clearly labeled as "External KOL Profile" and separated from approved promotional or medical content.

**Given** an MSL attempts to ask the copilot a question that would require off-label or unapproved content to answer accurately,  
**When** the copilot processes the query,  
**Then** the copilot declines to answer the off-label portion, displays a message explaining the content boundary, and routes a Medical Information Request to the MSL's home office MI team with the full query context pre-populated.

---

### Story 3: Automated Adverse Event Detection and Escalation (Compliance)

**As a** Medical Affairs compliance officer,  
**I want** all MSL interaction notes processed automatically for potential adverse event mentions before CRM sync,  
**so that** my organization meets pharmacovigilance reporting obligations without relying solely on MSL manual identification.

#### Acceptance Criteria

**Given** an MSL submits an interaction note containing language that matches AE detection patterns (e.g., symptom descriptions, patient harm mentions, side effect reports),  
**When** the note is processed,  
**Then** the system flags the note with an "AE Review Required" status, withholds CRM sync, notifies the MSL and their Medical Affairs Compliance designee in real time, and surfaces a pre-populated AE intake form for the MSL to review and confirm or dismiss within a defined SLA (default 24 hours).

**Given** the AE flag is confirmed by the MSL,  
**When** the compliance officer or MSL clicks "Submit AE Report,"  
**Then** the AE data (date, HCP identifier, product, described event) is packaged per the organization's configured format (MedWatch 3500A or equivalent), accessible for submission to the safety database, and an immutable audit record is created linking the original note, the flag event, review action, and final disposition.

**Given** the MSL dismisses the AE flag as a false positive,  
**When** the dismissal is submitted with a mandatory reason field,  
**Then** the note proceeds to CRM sync, the dismissal reason and timestamp are stored in the audit log, and the note is tagged for periodic compliance review sampling.

---

### Story 4: Real-World Evidence Surface at Point of Engagement (MSL Copilot)

**As an** MSL in a meeting with a clinical researcher,  
**When** the researcher asks about real-world patient outcomes for my company's therapy in their patient population,  
**I want** to instantly retrieve relevant, compliant RWE summaries from integrated data sources,  
**so that** I can provide an evidence-grounded, on-label response without leaving the room to follow up later.

#### Acceptance Criteria

**Given** an MSL is in an active field session and queries ADVANCE AI for RWE on a specific therapy and patient population,  
**When** the system processes the query,  
**Then** the response surfaces data from approved, pre-integrated RWE data sources (e.g., integrated registry data, published outcomes studies, clinical trial subgroup analyses) within 5 seconds, each result includes data source, study design, population size, and relevant outcome measures, and results are filtered to on-label indications only.

**Given** no RWE data meeting the compliance criteria exists in the integrated sources for the queried population,  
**When** the MSL submits the query,  
**Then** the system returns a transparent "No compliant RWE available for this query" message rather than surfacing speculative or unapproved data, and optionally generates a Medical Information follow-up request pre-populated with the HCP's question.

**Given** the field session is offline (e.g., hospital basement, conference center),  
**When** the MSL queries for RWE,  
**Then** a locally cached set of pre-downloaded, approved RWE summaries (synced during last online session) is returned with a visible "Offline — last synced [timestamp]" indicator.

---

### Story 5: Admin Integration Health Dashboard (Integrations PM / IT Buyer)

**As an** IT administrator or Medical Affairs Operations lead at a pharma company,  
**I want** a single dashboard showing the status of all ADVANCE AI integrations (CRM, MI systems, safety databases, RWE data feeds),  
**so that** I can identify and resolve sync failures before they impact field teams or compliance timelines.

#### Acceptance Criteria

**Given** an admin is authenticated in the ADVANCE AI admin console,  
**When** they view the Integration Health Dashboard,  
**Then** they see real-time status (Connected / Degraded / Failed) for each configured integration, the timestamp of the last successful sync per integration, a 30-day trend of sync success rate per integration, and the count of records currently queued for retry.

**Given** any integration enters a "Failed" state (3 consecutive sync failures),  
**When** the failure is detected,  
**Then** the admin is notified immediately via email and in-app alert, the failure reason (API error, auth expiry, schema mismatch) is displayed in human-readable language with a suggested remediation step, and a detailed error log is accessible for download.

**Given** an admin clicks on any integration in the dashboard,  
**When** the detail view loads,  
**Then** they see a paginated log of the last 100 sync events (success, failure, queued) with timestamps and record IDs, and a manual "Retry All Queued" action button.

---

## One-Page Product Spec: MSL Integration Hub & Copilot

### Problem Statement
MSLs at mid-size and emerging pharma companies face three compounding challenges in 2026:

1. **Fragmented data entry**: Interaction notes captured in one system must be manually re-entered into CRM, safety databases, and MI tracking systems — costing 2-3 hours per MSL per week and introducing compliance gaps.
2. **Compliance risk at the point of engagement**: MSLs increasingly use general-purpose AI tools (ChatGPT, Claude) to prepare for meetings, with no guardrails against off-label content generation or missed AE reporting obligations.
3. **No accessible integrated MSL tooling below enterprise price points**: IQVIA Expert Engagement and Veeva MedComms serve top-20 pharma; mid-market MSL teams are left with fragmented point solutions or spreadsheets.

The Veeva-Salesforce CRM split has created an acute short-term pain point: pharma IT teams now managing dual-platform migration cannot afford a third custom integration project per AI vendor.

### Proposed Solution
**ADVANCE AI MSL Integration Hub & Copilot** — a CRM-agnostic, compliance-first field medical platform that:

- Provides **pre-certified connectors** to Veeva Vault CRM, Salesforce Agentforce Life Sciences, leading EHR/MI systems, and safety database platforms, with a visual Integration Health Dashboard for admin oversight.
- Delivers an **MSL Copilot** powered by RAG over the customer's approved scientific content library — for pre-meeting briefs, in-meeting RWE lookup, and compliant response-to-inquiry drafting — with AE detection and escalation built into every interaction note workflow.
- Supports **offline-first** mobile access so field teams retain functionality in low-connectivity environments (hospitals, conference centers).
- Offers **modular, consumption-based pricing** accessible to pharma teams of 10–500 MSLs, with a connector-only entry tier that expands to full Copilot capabilities.

### Success Metrics

| Metric | Target | Timeframe |
|---|---|---|
| CRM sync success rate | ≥ 99.5% over 30 days | 3 months post-launch |
| MSL time saved on data entry (self-reported) | ≥ 2 hours/week per MSL | 6 months post-launch |
| AE detection rate vs. manual identification | ≥ 95% recall on AE mentions in interaction notes | 6 months post-launch |
| Off-label content blocks | 0 off-label claims passed through to MSL in approved-content briefs | Launch |
| Net Promoter Score (MSL users) | ≥ 45 | 6 months post-launch |
| Connector integrations certified | Veeva Vault CRM, Salesforce Agentforce LS, 1x safety database | GA launch |
| Mid-market pharma customers acquired | ≥ 10 logos (≤$5B revenue) | 12 months post-launch |

### Out of Scope (v1)
- **Drug discovery or preclinical AI** — focus is post-regulatory-approval field medical, not R&D pipeline
- **Commercial/sales rep workflows** — MSL and Medical Affairs only; no promotional content features
- **Direct EHR integration for patient data** — RWE surfaces published/registry data only; no direct patient record access in v1
- **Autonomous AI that initiates HCP outreach** — the copilot assists MSLs; it does not autonomously schedule or conduct meetings
- **Payer/market access features** — MMIT-type payer formulary intelligence is out of scope for MSL product (separate integration opportunity)
- **Custom model training per customer** — RAG over customer content is in scope; fine-tuning or custom LLM hosting is not
