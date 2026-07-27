# Requirements Package — Advanced AI MSL Platform

**Date:** 2026-07-27
**Based on:** Market Analysis 2026-07-27
**Domain:** MSL Engagement + Third-Party Integrations
**PM:** Automated research run

---

## Feature Opportunity: Unified MSL Pre-Call Intelligence Brief (Agentic)

### Market Gap Identified

The market analysis reveals that no single vendor currently unifies:
- Payer policy context (MMIT's domain)
- Real-world patient voice / RWE synthesis (Semalytix's domain)
- KOL past interaction history
- Published evidence summary
- EHR/biomarker signals

…into a single, compliance-auditable pre-call brief delivered within the MSL workflow. The Veeva–Salesforce CRM split (September 2025) means MSLs must now navigate data fragmentation across two dominant CRM ecosystems. This is the highest-value gap ADVANCE AI can address given its position as a purpose-built MSL platform with an integrations mandate in the job description.

---

## User Stories

### Story 1 — Pre-Call Intelligence Brief

**As an** MSL preparing for a KOL engagement,
**I want** the platform to auto-generate a pre-call brief that consolidates the KOL's past interaction history, recent publications, relevant payer policy updates, and real-world patient sentiment on the relevant indication,
**so that** I can walk into every scientific conversation fully prepared without spending 45+ minutes manually gathering information across four separate tools.

#### Acceptance Criteria

**Given** an MSL has selected an upcoming HCP/KOL meeting in the platform,
**When** they request a pre-call brief,
**Then** the platform should:
- Pull the KOL's interaction history from the CRM (Veeva Vault or Salesforce LSC) within 30 seconds
- Surface the KOL's last 3 relevant publications and citation impact
- Include a payer policy summary for the relevant indication (sourced from MMIT or equivalent API)
- Include a patient-sentiment snapshot (aggregated from public sources, GDPR/HIPAA-compliant)
- Flag any adverse events or off-label topics in the brief with a compliance warning
- Display a human-readable audit trail showing data sources and retrieval timestamp
- Allow the MSL to export or save the brief as a PDF

**Given** the CRM integration is unavailable or returns an error,
**When** the brief is generated,
**Then** the platform should notify the MSL of the missing data source, generate a partial brief with available data, and log the gap for admin review.

---

### Story 2 — CRM Bi-Directional Sync (Veeva Vault + Salesforce LSC)

**As a** medical affairs operations manager,
**I want** MSL field insights captured in ADVANCE AI to automatically sync to our Veeva Vault CRM or Salesforce Life Sciences Cloud instance,
**so that** KOL engagement records are maintained in a single authoritative system of record without manual re-entry.

#### Acceptance Criteria

**Given** an MSL has completed and submitted a field insight report in ADVANCE AI,
**When** the submission is saved,
**Then** the platform should:
- Push the structured insight (KOL name, meeting date, topics discussed, insight tags, sentiment) to the mapped CRM object within 60 seconds
- Support both Veeva Vault CRM and Salesforce Life Sciences Cloud as sync targets (configurable per organization)
- Preserve the ADVANCE AI record as the source with CRM record ID cross-referenced
- Log any sync failures with error detail and auto-retry up to 3 times

**Given** a sync configuration is first being set up by an admin,
**When** they navigate to Integration Settings,
**Then** the platform should offer a guided setup wizard for Veeva Vault OAuth and Salesforce Connected App credentials, with field mapping UI and a test-sync function, requiring no developer involvement for standard object mappings.

---

### Story 3 — Compliance-Auditable AI Content Review

**As a** medical compliance officer,
**I want** every AI-generated response, insight summary, or scientific draft produced by the platform to carry a full audit trail — including which models were used, what source documents were cited, and whether a human reviewed and approved the output,
**so that** the organization can demonstrate regulatory compliance and defend any AI-generated content in an audit or adverse-event investigation.

#### Acceptance Criteria

**Given** the platform generates any AI output (brief, summary, draft, insight),
**When** the output is displayed to the user,
**Then** the system must:
- Attach a metadata panel showing: model identifier, retrieval sources (URLs/document names), generation timestamp, and any compliance flags triggered
- Require a "Reviewed and Approved" acknowledgment from a human user before the output can be exported or shared externally
- Store the human-approval event in an immutable audit log (user, timestamp, IP, action)
- Flag any output containing off-label drug references, promotional language patterns, or unverified efficacy claims with a yellow/red compliance indicator

**Given** a compliance officer queries the audit log,
**When** they filter by date range or user,
**Then** the system should return results within 5 seconds and support export to CSV.

---

### Story 4 — Agentic RWE Synthesis for KOL Conversations

**As an** MSL supporting an oncology portfolio,
**I want** the platform to synthesize real-world evidence — from clinical registries, published studies, and patient outcomes data — into a concise, indication-specific summary I can reference in KOL conversations,
**so that** I can discuss post-approval RWE with clinical depth and credibility, bridging trial efficacy data with real-world practice patterns.

#### Acceptance Criteria

**Given** an MSL has selected a drug-indication pair in the platform,
**When** they request an RWE synthesis,
**Then** the platform should:
- Query indexed medical literature (minimum 10 M publications) and any connected clinical registry APIs
- Return a synthesized summary of 3–5 key RWE findings with citation links, rated by evidence quality (meta-analysis > RCT > cohort > case series)
- Distinguish clearly between Phase III trial data and real-world observational data within the summary
- Refresh the synthesis if source data is more than 30 days old
- Provide a "Share with Medical" workflow that routes the synthesis for medical reviewer sign-off before it can be used in external-facing context

**Given** no RWE data is available for a rare indication,
**When** the MSL requests synthesis,
**Then** the platform should surface the absence clearly ("No published RWE found for [indication] as of [date]") rather than generating speculative content.

---

### Story 5 — Integration Health Dashboard for Ops Teams

**As a** medical affairs operations manager,
**I want** a real-time integration health dashboard showing the status of all third-party data connections (CRM, EHR, payer data, literature APIs),
**so that** I can immediately identify and escalate data pipeline failures before they impact MSL field productivity or data integrity.

#### Acceptance Criteria

**Given** an admin navigates to the Integration Dashboard,
**When** the page loads,
**Then** the dashboard should:
- Display connection status (green/amber/red) for each configured integration with last-successful-sync timestamp
- Surface the count of failed sync events in the past 24 hours, grouped by integration
- Provide a one-click "Test Connection" action per integration that returns a result within 10 seconds
- Send an email + in-app alert to the admin within 5 minutes of any integration moving to a failed state

**Given** an integration has been in a failed state for more than 2 hours,
**When** the admin views the dashboard,
**Then** the system should display a recommended resolution action (e.g., "OAuth token expired — re-authenticate") and a link to support documentation.

---

## One-Page Product Spec: Unified MSL Pre-Call Intelligence Brief

### Problem Statement

MSLs currently spend 30–60 minutes before each KOL engagement manually aggregating information from 4–6 disparate systems: Veeva or Salesforce CRM (past interactions), PubMed (publications), MMIT or similar (payer access), and internal medical portals (brand data). This overhead reduces field time, introduces inconsistency in scientific conversation quality, and creates compliance risk when MSLs rely on unvetted or outdated information. No existing platform unifies these sources for MSLs with the compliance controls that medical affairs organizations require.

### Proposed Solution

An agentic Pre-Call Intelligence Brief feature within ADVANCE AI that:
1. Triggers on-demand from an upcoming meeting record (CRM-synced or manually entered)
2. Orchestrates parallel retrieval from CRM history, literature index, payer policy API, and patient-voice dataset
3. Synthesizes a structured, readable brief with source citations and compliance flags
4. Requires human acknowledgment before external use and logs approval to an immutable audit trail
5. Delivers the brief within 60 seconds for standard requests

The feature integrates with Veeva Vault CRM and Salesforce Life Sciences Cloud out of the box, supports FHIR-based EHR read access for relevant patient-population context, and runs on ADVANCE AI's existing RAG + compliance infrastructure.

### Success Metrics

| Metric | Baseline | 6-Month Target |
|---|---|---|
| Avg. MSL pre-call prep time | 45 min (survey) | ≤ 15 min |
| Brief generation adoption rate | 0% (new feature) | ≥ 60% of meetings with ≥1 brief generated |
| Compliance flag acknowledgment rate | — | 100% (gated by design) |
| CRM sync error rate | — | < 2% of brief-to-CRM sync events |
| MSL satisfaction score (feature-specific CSAT) | — | ≥ 4.2 / 5.0 |
| Time from integration setup to first brief | — | ≤ 30 minutes for standard CRM configs |

### Out of Scope (v1)

- Promotional content generation or off-label content (compliance boundary — medical content only)
- Direct write-back to EHR systems (read-only EHR access only in v1)
- Automated sending of briefs to KOLs or HCPs
- Integration with non-Veeva/non-Salesforce CRM systems (Phase 2 roadmap)
- Real-time biomarker or pathology data from digital pathology vendors (Phase 2)
- Multi-language brief generation beyond English (Phase 2)

---

*Persona reference: MSL (Medical Science Liaison), Medical Affairs Ops Manager, Medical Compliance Officer.*
*Requirements grounded in market gaps identified in market-analysis-2026-07-27.md.*
