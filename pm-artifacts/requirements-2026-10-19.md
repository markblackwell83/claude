# Requirements Package: MSL Intelligence & Integration Platform
**Date:** 2026-10-19  
**Prepared for:** ADVANCE AI — Product Management  
**Based on:** market-analysis-2026-10-19.md

---

## Feature Opportunity: Governed Agentic Pre-Call Intelligence for MSLs

### Background
Market analysis reveals a clear gap: MSLs need AI-powered pre-call planning that is both agentic (proactive, multi-source synthesis) and governed (compliant, auditable, source-attributed). Current competitors either have compliance depth (Sorcero) or agentic architecture (Semalytix) — no single platform unifies both for the MSL field workflow. Meanwhile, HCPs are increasingly arriving to scientific exchange armed with consumer AI outputs, raising the bar for what MSLs need to provide in those conversations.

ADVANCE AI's positioning as a third-party integrations platform makes it well-placed to aggregate data from Veeva CRM, scientific databases (PubMed, ClinicalTrials.gov), KOL intelligence tools, and EHR/FHIR systems into a single, governed pre-call and on-call intelligence layer.

---

## User Stories

### Story 1: Pre-Call Intelligence Briefing

**As an** MSL preparing for a KOL meeting,  
**I want** the platform to automatically generate a pre-call briefing from the HCP's recent publications, congress presentations, clinical trial activity, and past interaction history,  
**so that** I can enter the conversation with relevant, current talking points without spending 2+ hours on manual research.

#### Acceptance Criteria

**Given** an MSL has a meeting scheduled with an HCP in their Veeva CRM,  
**When** the MSL opens the meeting record in the ADVANCE AI platform,  
**Then** a pre-call briefing is generated within 60 seconds, surfacing:
- The HCP's last 5 publications (with source links and publication dates)
- Any congress presentations or abstracts in the past 12 months
- Active or recently completed clinical trials the HCP is associated with
- Key themes from prior MSL interaction notes (from CRM)
- Flagged topics where the HCP's research intersects with the company's therapeutic area

**Given** the briefing is generated,  
**When** the MSL reviews it,  
**Then** every AI-generated claim includes an inline source citation (DOI, ClinicalTrials.gov ID, or CRM note reference)

**Given** a briefing is generated,  
**When** it is viewed or downloaded,  
**Then** a tamper-evident audit log entry is created recording: MSL user ID, HCP ID, timestamp, data sources queried, and model version used

---

### Story 2: Scientific Exchange Assist (Response to HCP AI Outputs)

**As an** MSL in a scientific exchange where an HCP cites an AI-generated summary,  
**I want** to quickly surface peer-reviewed evidence that contextualizes, validates, or corrects the AI claim the HCP referenced,  
**so that** I can provide the HCP with verifiable, authoritative information and maintain credibility as a scientific resource.

#### Acceptance Criteria

**Given** an MSL is in an active HCP interaction and opens the Scientific Exchange Assist panel,  
**When** the MSL types or pastes a claim or topic (e.g., a drug's subgroup analysis the HCP mentioned),  
**Then** the platform returns within 10 seconds:
- 3–5 relevant peer-reviewed citations from PubMed/scientific databases
- A brief, plain-language summary of each citation's relevance
- A confidence indicator for each result (high / moderate / low based on evidence strength)

**Given** a citation is returned,  
**When** the MSL selects it,  
**Then** they see the full abstract, author list, publication date, and a direct link to the source

**Given** the MSL uses the Scientific Exchange Assist during a visit,  
**When** the interaction is logged,  
**Then** the queries made and citations retrieved are appended to the interaction record in the connected CRM (Veeva / Salesforce) as a structured note

---

### Story 3: Integration Connector Setup (Self-Serve)

**As a** Medical Affairs operations manager at a pharma company onboarding ADVANCE AI,  
**I want** to connect our existing Veeva Vault CRM, PubMed API, and internal SharePoint document library without needing engineering resources,  
**so that** our MSL team can start using the platform within a single business day.

#### Acceptance Criteria

**Given** the ops manager accesses the Integrations Catalog in the admin console,  
**When** they select the Veeva Vault connector,  
**Then** they are guided through an OAuth2/API key configuration flow with step-by-step instructions requiring no code

**Given** credentials are entered,  
**When** the ops manager initiates a connection test,  
**Then** the platform confirms successful data pull within 30 seconds or returns a plain-English error message with a remediation suggestion

**Given** a connector is configured,  
**When** data syncs,  
**Then** a sync log is available showing: last sync time, records synced, any failed records and the reason

**Given** the integration is live,  
**When** the ops manager invites the MSL team,  
**Then** MSLs can access connected data within the platform immediately, with no IT ticket required

---

### Story 4: Compliance-Grade Audit Trail

**As a** compliance officer at a pharmaceutical company,  
**I want** all MSL AI interactions with the platform to generate a complete, immutable audit log,  
**so that** I can demonstrate regulatory compliance (21 CFR Part 11, GxP) and respond to audit requests without reconstructing activity from multiple systems.

#### Acceptance Criteria

**Given** any MSL uses the platform (pre-call briefing, scientific exchange, literature search),  
**When** the interaction occurs,  
**Then** an audit log entry is created containing: user ID, action type, data sources accessed, AI model version, input query (hashed or full, configurable), output generated, and timestamp (UTC)

**Given** the compliance officer accesses the Audit Log console,  
**When** they apply a date range and user filter,  
**Then** filtered results are returned in under 5 seconds and are exportable as CSV and PDF

**Given** an audit log entry is created,  
**When** it is written to the database,  
**Then** it is immutable (no edit or delete path exists, including for platform admins)

**Given** a retention policy is configured,  
**When** the retention period is reached,  
**Then** logs are archived (not deleted) and remain available for compliance download with an access reason required

---

### Story 5: MSL Field Reporting Automation

**As an** MSL after completing an HCP interaction,  
**I want** the platform to draft a structured field report from my meeting notes and captured interaction data,  
**so that** I can review, edit, and submit a compliant interaction record in less than 5 minutes instead of 30.

#### Acceptance Criteria

**Given** an MSL completes an HCP interaction and opens the post-meeting report screen,  
**When** they initiate report generation,  
**Then** the platform drafts a structured report including: HCP name and affiliation (from CRM), meeting date/location, topics discussed (from pre-call briefing and any notes taken), action items, and follow-up literature to send

**Given** the draft is generated,  
**When** the MSL reviews it,  
**Then** they can edit any field inline and add free-text sections

**Given** the MSL submits the report,  
**When** submission is confirmed,  
**Then** the report is pushed to the CRM record (Veeva / Salesforce) as a structured activity, and a copy is stored in the ADVANCE AI platform with full audit metadata

**Given** the report is submitted,  
**When** a compliance officer queries interactions for that HCP,  
**Then** the interaction report is retrievable via the Audit Log console with all associated metadata

---

## One-Page Product Spec: MSL Pre-Call Intelligence Engine

### Problem Statement
MSLs spend 2–4 hours per week on manual pre-call research, aggregating data from scientific databases, CRM history, and KOL tracking tools. This time is unstructured, inconsistent across team members, and not auditable. Meanwhile, HCPs are arriving to scientific exchanges informed by consumer AI — raising expectations for the depth and quality of MSL-led conversations. Existing platforms (Veeva, Sorcero) address pieces of this problem but do not offer a unified, governed, agentic pre-call intelligence product purpose-built for the MSL role.

### Proposed Solution
Build a **Pre-Call Intelligence Engine** within the ADVANCE AI platform that:
1. Automatically triggers a pre-call briefing synthesis when a meeting is confirmed in a connected CRM (Veeva, Salesforce)
2. Aggregates data from scientific databases (PubMed, ClinicalTrials.gov), congress proceedings, and CRM interaction history via pre-built connectors
3. Generates a structured, source-attributed briefing delivered to the MSL's mobile or desktop interface
4. Logs all AI activity with an immutable, compliance-grade audit trail

The solution is differentiated by: (a) native integration with existing pharma tech stack, (b) compliance architecture built in from day one (not bolted on), and (c) source attribution on every AI-generated claim.

### Success Metrics
| Metric | Baseline | Target (6 months post-launch) |
|---|---|---|
| Pre-call research time per MSL per week | ~3 hours (manual) | ≤45 minutes (AI-assisted) |
| Briefing generation latency | N/A | <60 seconds |
| MSL adoption rate among onboarded teams | N/A | ≥70% weekly active users |
| Compliance audit pass rate | N/A | 100% (all interactions logged) |
| Integration setup time (ops admin) | Multi-day (IT ticket) | <1 business day (self-serve) |
| Net Promoter Score (MSL users) | Baseline TBD at launch | ≥40 |

### Out of Scope (v1)
- AI-generated promotional content or off-label clinical recommendations
- EHR patient-level data access (patient data privacy; HIPAA complexity deferred)
- Full autonomous agent mode (human review required for all AI outputs in v1)
- Building new scientific databases (ADVANCE AI connects to existing sources; does not host primary literature)
- Replacing Veeva or Salesforce CRM (platform is an intelligence layer, not a CRM replacement)
- Multilingual support (English-only in v1; expansion planned for v2)
