# ADVANCE AI — Requirements Package
**Date:** 2026-06-22  
**Feature Opportunity:** Agentic MSL Workflow Assistant with Integration Hub  
**Prepared for:** Lead Product Manager / Engineering  
**Role Context:** PM — Third-Party Integrations & MSL Products

---

## Feature Opportunity

**From Market Analysis:** The convergence of agentic AI and medical affairs automation has created a clear gap in the market: no single platform delivers end-to-end agentic workflow automation for MSL field execution — pre-call planning, post-call insight capture, competitive signal routing, and automated follow-up drafting — in a compliance-ready, MLR-traceable package that also connects to existing enterprise systems (Veeva, Salesforce, IQVIA OCE, EHRs).

Mid-size biopharma companies ($50M–$5B revenue) are underserved by Veeva (too complex, too expensive) and unserved by CRO-bundled solutions like Sageforce (requires full service engagement). They need an AI-native MSL intelligence platform that:

1. **Plugs into their existing CRM and data systems** via standards-based integrations (FHIR R4, REST, HL7)
2. **Automates high-friction MSL workflows** — pre-call briefs, post-call note capture, competitive intelligence digests
3. **Maintains compliance posture** — MLR review routing, off-label guardrails, full audit trail

This positions ADVANCE AI as the intelligence layer *above* the CRM in a $3.8B+ medical affairs technology market growing at 18%+ CAGR.

---

## User Stories

### Story 1: Pre-Call Intelligence Brief for MSL
**As an** MSL preparing for an HCP scientific exchange,  
**I want** an automatically generated pre-call brief that surfaces the HCP's recent publications, congress activity, trial involvement, and my team's prior interaction history,  
**so that** I can enter the conversation with full context and deliver a more relevant, credible scientific exchange without spending 45+ minutes on manual research.

#### Acceptance Criteria

**Scenario 1: Brief generation for a scheduled meeting**
- **Given** an MSL has a meeting scheduled with an HCP in their calendar (synced via Veeva, Salesforce, or Google/Outlook integration)
- **When** the meeting is 24 hours away
- **Then** the system automatically generates and delivers a pre-call brief containing: (a) HCP publication summary (last 12 months), (b) congress/advisory board activity, (c) open clinical trials in HCP's therapeutic area, (d) last 3 interaction summaries from CRM, (e) competitive activity alerts relevant to HCP's specialty
- **And** the brief is delivered in-app and via email in under 60 seconds of generation trigger

**Scenario 2: On-demand brief generation**
- **Given** an MSL is viewing an HCP profile in the platform
- **When** they click "Generate Pre-Call Brief"
- **Then** a fresh brief is generated within 90 seconds using the same data sources
- **And** the brief includes a "last refreshed" timestamp and data source citations

**Scenario 3: Compliance guardrail for off-label content**
- **Given** the pre-call brief aggregates published data
- **When** the AI attempts to include information related to off-label indications not approved in the MSL's region
- **Then** the content is flagged with a compliance warning and routed through the MLR review queue before display, or suppressed with a logged audit event

---

### Story 2: Post-Call Note Capture and CRM Sync
**As an** MSL who has just completed a field engagement with an HCP,  
**I want** to use voice-to-text or structured templates to capture call notes, which are then automatically enriched, summarized, and synced back to Veeva or Salesforce,  
**so that** I spend less than 5 minutes on administrative documentation and my medical affairs team has accurate, searchable records without data re-entry.

#### Acceptance Criteria

**Scenario 1: Voice note capture and structured extraction**
- **Given** an MSL is on mobile after a field meeting
- **When** they record a voice note of 1–5 minutes via the mobile app
- **Then** the system transcribes the audio within 60 seconds, extracts structured fields (HCP name, topics discussed, questions raised, follow-up actions, sentiment), and presents a draft note for MSL review
- **And** the MSL can edit any field before confirming

**Scenario 2: CRM push on confirmation**
- **Given** an MSL has reviewed and confirmed a post-call note
- **When** they tap "Sync to CRM"
- **Then** the structured note is pushed to the connected CRM (Veeva or Salesforce) within 30 seconds, mapping ADVANCE AI fields to the CRM's native call activity schema
- **And** a sync confirmation with record ID is displayed in-app
- **And** any sync failure triggers an in-app alert with retry option and local draft preservation

**Scenario 3: Duplicate detection**
- **Given** a CRM record for the same HCP and same date already exists
- **When** the sync is attempted
- **Then** the system flags the potential duplicate, shows both records side-by-side, and requires explicit MSL confirmation to merge or create new before writing to CRM

---

### Story 3: Integration Connector Configuration (Admin)
**As a** Medical Affairs Operations manager,  
**I want** to configure and manage third-party system integrations (Veeva, Salesforce, IQVIA OCE, EHR systems) through a self-service admin console,  
**so that** my team can connect ADVANCE AI to our enterprise systems without requiring IT developer resources for every configuration change.

#### Acceptance Criteria

**Scenario 1: New connector setup**
- **Given** an admin user with integration management permissions
- **When** they navigate to the Integration Hub and select "Add Connector"
- **Then** they can select from a library of pre-built connectors (minimum: Veeva Vault CRM, Salesforce Life Sciences Cloud, IQVIA OCE, Epic via FHIR R4)
- **And** the setup wizard guides them through OAuth2/API key configuration in under 15 minutes without requiring a developer
- **And** a test connection validates credentials and field mapping before going live

**Scenario 2: Field mapping customization**
- **Given** an active connector for Veeva CRM
- **When** an admin opens the field mapping editor
- **Then** they can map ADVANCE AI data fields to Veeva fields using a drag-and-drop interface
- **And** they can set sync direction (ADVANCE AI → CRM, CRM → ADVANCE AI, or bidirectional) per field
- **And** changes take effect on the next scheduled sync cycle without system downtime

**Scenario 3: Connector health monitoring**
- **Given** an active integration connector
- **When** a sync event fails due to authentication expiry or API rate limiting
- **Then** the admin dashboard displays a connector health alert with error details, last successful sync timestamp, and a one-click re-authentication action
- **And** affected MSL users receive an in-app notification that their sync is paused

---

### Story 4: Competitive Intelligence Digest for Medical Strategy Teams
**As a** Medical Affairs Director overseeing a therapeutic area,  
**I want** a weekly automated digest of competitive intelligence signals — competitor trial registry updates, publications, regulatory filings, and congress abstracts — filtered to my therapeutic area,  
**so that** my medical strategy team spends time acting on insights rather than manually monitoring 15+ sources.

#### Acceptance Criteria

**Scenario 1: Digest generation and delivery**
- **Given** a Medical Affairs Director has configured their therapeutic area and competitor watchlist in ADVANCE AI
- **When** the weekly digest generation runs (configurable day/time)
- **Then** the system produces a structured digest containing: (a) new publications by monitored KOLs, (b) clinical trial registry updates (ClinicalTrials.gov, EU CTR), (c) regulatory submission signals, (d) congress abstract alerts, prioritized by AI-assessed relevance score
- **And** the digest is delivered via email and in-app, with deep links to each source

**Scenario 2: Alert escalation for high-priority signals**
- **Given** the system detects a competitor trial achieving primary endpoints or receiving a regulatory approval
- **When** the event is classified as high-priority (configurable threshold)
- **Then** an immediate push notification and email alert is sent to the Director — not waiting for the weekly digest
- **And** the alert includes a one-paragraph AI-generated summary with source citations

**Scenario 3: Configuring watchlist scope**
- **Given** a user in the platform's intelligence configuration screen
- **When** they define therapeutic area keywords, competitor drug names, and competitor companies
- **Then** the system confirms coverage by showing estimated weekly signal volume and source distribution
- **And** they can add/remove watchlist items at any time with changes taking effect within 24 hours

---

### Story 5: MLR Compliance Review Routing
**As a** Medical, Legal, and Regulatory (MLR) reviewer,  
**I want** AI-generated content produced by MSLs (pre-call briefs, follow-up email drafts, scientific summaries) to be automatically routed to my review queue with clear flagging of content that requires approval,  
**so that** our field team can use AI-assisted content creation without creating compliance risk or requiring manual content policing.

#### Acceptance Criteria

**Scenario 1: Automatic content flagging**
- **Given** an MSL uses the AI to generate a follow-up scientific summary for an HCP
- **When** the AI-generated content includes claims about a drug's efficacy, safety data, or disease area information
- **Then** the content is automatically scored against a configurable compliance ruleset (approved indications, label claims, regional regulatory requirements)
- **And** content classified as "requires review" is placed in the MLR queue before the MSL can send it
- **And** content classified as "pre-approved" (e.g., from the approved content library) is released immediately with an audit log entry

**Scenario 2: MLR review and approval workflow**
- **Given** a piece of AI-generated content is in the MLR queue
- **When** an MLR reviewer opens the review task
- **Then** they see the original content, the AI's compliance flags with specific rule citations, the MSL's intended recipient and context, and approve/reject/modify controls
- **And** approval releases the content to the MSL with a timestamped audit trail
- **And** rejection sends a notification to the MSL with the reviewer's comments

**Scenario 3: Audit trail export**
- **Given** a compliance audit is requested
- **When** an admin exports the MLR activity log for a specified date range
- **Then** the export includes: content item ID, generation timestamp, MSL user, compliance classification score, reviewer identity, review timestamp, and final disposition (approved/rejected/modified)
- **And** the export is available in CSV and PDF formats within 60 seconds

---

## One-Page Product Spec: Agentic MSL Workflow Assistant

### Problem Statement

MSLs spend 35–45% of their field time on administrative tasks: researching HCPs before meetings, writing call notes after meetings, and monitoring competitive landscape manually. Existing solutions either require Veeva-level investment and complexity (pricing out mid-size biopharma) or are CRO-bundled services that cannot be procured as standalone software. As a result, MSL teams are slow to act on scientific opportunities, inconsistent in documentation quality, and generating compliance risk through unreviewed AI-assisted content.

### Proposed Solution

An **Agentic MSL Workflow Assistant** embedded in ADVANCE AI's platform that automates the three highest-friction MSL tasks:

1. **Pre-call intelligence briefs** — AI-generated, compliance-screened summaries delivered 24h before each HCP meeting, pulling from publications, clinical trial registries, congress data, and CRM history
2. **Post-call note capture and CRM sync** — voice-to-structured-note transcription with automatic push to Veeva or Salesforce, reducing post-call admin from 30+ minutes to under 5 minutes
3. **MLR-compliant content routing** — all AI-generated MSL content auto-classified against configurable compliance rulesets, with an integrated review queue for MLR teams

Delivered as an **Integration Hub** with self-service connectors to Veeva Vault CRM, Salesforce Life Sciences Cloud, IQVIA OCE, and Epic (FHIR R4), enabling deployment without custom engineering on the customer's side.

### Target Personas

- **Primary:** Field MSL (daily active user) — 5–50 person teams at mid-size biopharma
- **Secondary:** Medical Affairs Director — weekly digest and strategic intelligence consumer
- **Tertiary:** MLR Reviewer / Medical Affairs Ops — compliance queue management and connector administration

### Success Metrics

| Metric | Baseline (Pre-Launch) | Target (6 months post-GA) |
|---|---|---|
| MSL post-call note completion rate | ~60% (industry avg.) | >90% |
| Time to complete post-call documentation | 30–45 min | <5 min |
| Pre-call brief adoption (% of meetings with brief generated) | 0% | >75% |
| Integration setup time (new connector) | 4–8 weeks (custom) | <15 min (self-serve) |
| MLR review cycle time for AI-generated content | N/A | <48h |
| Customer NPS (MSL persona) | N/A | >50 |
| Integration connectors live at GA | 0 | 4 (Veeva, Salesforce, IQVIA OCE, Epic FHIR) |

### Out of Scope (v1)

- Full replacement of Veeva or Salesforce CRM (ADVANCE AI is an intelligence + automation layer, not a system of record)
- Clinical trial management / EDC functionality (TrialHub/CTMS space)
- Payer/formulary data intelligence (MMIT's domain — potential future integration, not v1 build)
- Patient-facing communications or patient engagement portals
- Autonomous sending of external communications without human MSL confirmation — all outbound content requires MSL review before send
- Custom LLM fine-tuning or model training for individual customer datasets (Phase 2 consideration)
- Regulatory submission authoring (e.g., dossier creation, CTD modules)

---

*Analysis based on: current MSL workflow research, competitive landscape review (June 2026), and market gap identification documented in `market-analysis-2026-06-22.md`.*
