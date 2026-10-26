# Requirements Package: Advanced AI — Integrations & MSL Product

**Date:** 2026-10-26  
**Prepared for:** ADVANCE AI Product Manager — Integrations & MSL  
**Based on:** Market Analysis 2026-10-26  

---

## Feature Opportunity: MSL Integration Hub with Compliant Insight Pipeline

### Market Gap Rationale

The market analysis identified a critical gap at the intersection of three forces:

1. **Post-Veeva–Salesforce fragmentation:** Pharma's CRM ecosystem is disrupted. Integrations between field tools, EHR systems, and market access data are patchwork.
2. **Audit and compliance as table stakes:** 2026 is the year pharma demands proven, traceable AI — not pilots. Platforms without governance baked in are losing procurement decisions.
3. **MSL insight-to-action loop is broken:** MSLs generate valuable field intelligence but lack tools to route it efficiently into medical strategy. Existing tools are either too light (notes capture only) or too expensive/locked-in (Veeva).

**The opportunity:** Build ADVANCE AI's **Integration Hub** — a standards-based connector layer paired with an AI-curated insight pipeline — that lets MSLs capture field observations in context, surfaces those observations as structured, auditable insights for Medical Affairs leadership, and integrates with the systems pharma already uses (Veeva Vault, Epic, MMIT, literature databases).

---

## User Stories

### Story 1: MSL Pre-Call Intelligence Brief
**As a** Medical Science Liaison preparing for a KOL meeting,  
**I want** an AI-generated pre-call brief that surfaces relevant recent publications, the KOL's known scientific interests, open questions from prior interactions, and formulary access context for my therapeutic area,  
**so that** I walk into every HCP conversation informed, differentiated, and compliant with approved content guidelines — without spending 45 minutes doing manual research.

#### Acceptance Criteria
- **Given** an MSL has a scheduled meeting with a KOL in the system,  
  **When** the MSL opens the meeting record 24–4 hours before the meeting,  
  **Then** the platform displays an AI-generated brief containing: (a) ≥3 recent relevant publications (≤90 days old) with plain-language summaries; (b) key scientific interests/questions attributed to that KOL from prior interactions; (c) current formulary access status for relevant products in the KOL's region; (d) a compliance badge confirming all content is from the approved content library.

- **Given** the MSL is offline (e.g., in a hospital with no signal),  
  **When** the MSL opens the meeting record,  
  **Then** the platform serves a cached version of the brief generated at the last sync point, clearly labelled with the cache timestamp.

- **Given** a KOL appears in the system for the first time (no interaction history),  
  **When** the MSL opens the meeting record,  
  **Then** the platform displays a brief built from external data sources (PubMed, congress feeds) attributed to the KOL's publication history, with a notice that no internal interaction history exists yet.

---

### Story 2: Post-Call Insight Capture with AI Structuring
**As a** Medical Science Liaison completing a KOL interaction,  
**I want** to record my field observations via voice or free-text and have the platform automatically tag, structure, and classify those observations into insight categories (e.g., unmet need, product feedback, competitive mention, research interest),  
**so that** my observations are immediately useful to Medical Affairs leadership without manual re-formatting or data entry burden.

#### Acceptance Criteria
- **Given** an MSL submits a post-call note (≥50 words, voice or text),  
  **When** the note is saved,  
  **Then** the platform applies AI tagging within 30 seconds: at minimum classifying the note by insight category, sentiment, and therapeutic area, and surfacing any detected compliance flags (e.g., off-label mention) for human review.

- **Given** an AI-tagged insight has been reviewed and approved by a Medical Affairs reviewer,  
  **When** that insight is approved,  
  **Then** it is added to the aggregated insights dashboard with full source traceability (MSL, date, KOL, meeting ID) and becomes queryable by insight category and therapeutic area.

- **Given** a compliance flag has been raised on a post-call note,  
  **When** the flag is raised,  
  **Then** the MSL is notified immediately and the note is held in a "pending review" queue; the note is NOT visible in the aggregated insights dashboard until cleared by an authorized Medical Affairs reviewer.

---

### Story 3: Third-Party CRM / EHR Integration (Veeva Vault & Epic)
**As a** Medical Affairs IT administrator,  
**I want** to connect ADVANCE AI to our existing Veeva Vault CRM and Epic EHR instances using a self-service integration wizard,  
**so that** KOL profiles, interaction records, and formulary access data flow bidirectionally without bespoke development work or ongoing IT maintenance burden.

#### Acceptance Criteria
- **Given** an admin has valid API credentials for Veeva Vault and/or Epic,  
  **When** the admin initiates an integration via the Integration Hub,  
  **Then** the platform displays a step-by-step configuration wizard, validates credentials in real time, and confirms a successful test sync within a single session (≤30 minutes end-to-end for a standard configuration).

- **Given** a bidirectional Veeva Vault integration is active,  
  **When** an MSL updates an interaction record in ADVANCE AI,  
  **Then** the corresponding record in Veeva Vault is updated within 5 minutes, and vice versa; no duplicate records are created; conflicts are surfaced to the admin for resolution.

- **Given** an integration is configured,  
  **When** the admin visits the Integration Hub,  
  **Then** they see a live health dashboard showing: last sync time, records synced in last 24h, error rate, and a log of the last 50 sync events with error details where applicable.

---

### Story 4: Aggregated KOL Insights Dashboard for Medical Affairs Leadership
**As a** Medical Affairs Director,  
**I want** a real-time dashboard that aggregates approved MSL field insights by therapeutic area, insight category, and geography, with trend lines over time and drill-down to source observations,  
**so that** I can identify emerging unmet needs, competitive signals, and research gaps and translate them into actionable strategy within weekly review cycles.

#### Acceptance Criteria
- **Given** the Medical Affairs Director opens the insights dashboard,  
  **When** the page loads,  
  **Then** the dashboard displays aggregated insights from the last 30 days by default, segmented by: (a) therapeutic area, (b) insight category (unmet need / product feedback / competitive / research interest), (c) geography (country / region); each segment shows count, trend (up/flat/down vs. prior 30 days), and top 3 verbatim representative quotes.

- **Given** the Director clicks on an insight cluster,  
  **When** the drill-down opens,  
  **Then** all source observations contributing to that cluster are listed with full attribution (MSL name, KOL, date, meeting type) and a link back to the original post-call note.

- **Given** an insight cluster has ≥5 observations in 7 days (spike threshold),  
  **When** the spike is detected,  
  **Then** an automated alert is sent to the Medical Affairs Director and the Lead PM with a summary of the cluster, source count, and a suggested next action (e.g., "Flag for medical strategy review," "Add to scientific platform update").

---

### Story 5: Compliance-Gated Content Delivery in MSL Workflows
**As a** Compliance Officer at a mid-size pharma company,  
**I want** all AI-generated content surfaced to MSLs (pre-call briefs, literature summaries, KOL talking points) to be governed by an approved content library with version control and audit logging,  
**so that** I can demonstrate to regulators that every piece of content an MSL could share or reference has been reviewed and approved, and that no unapproved AI-generated content reaches HCPs.

#### Acceptance Criteria
- **Given** an AI-generated pre-call brief or content suggestion is created,  
  **When** the content is generated,  
  **Then** every piece of content in the brief is tagged with its source (internal approved library version + document ID, or external PubMed/congress citation with URL), and no content appears without a traceable source tag.

- **Given** an approved content library item is retired or superseded,  
  **When** the item is retired in the content management system,  
  **Then** all active pre-call briefs and suggestions referencing that item are automatically flagged within 1 hour, and MSLs see a banner indicating the content needs review before their next meeting.

- **Given** a Compliance Officer requests an audit report,  
  **When** the report is generated,  
  **Then** the system produces a downloadable PDF/CSV listing all AI-generated content delivered to MSLs in the specified date range, the approved source for each item, the MSL who viewed it, and the KOL interaction it was associated with.

---

## One-Page Product Spec: MSL Integration Hub

### Problem Statement

ADVANCE AI's MSL product serves field teams and Medical Affairs organizations, but today lacks the integration depth needed to fit into customers' existing technology stacks. Customers use Veeva Vault for CRM, Epic or Cerner for EHR-adjacent access, and MMIT/Norstella for market access data. Each of these systems holds data MSLs need — yet extracting and synthesizing it requires manual effort or bespoke IT work. Simultaneously, the insights MSLs generate in the field are lost or underutilized: captured as free-text notes that never become structured, queryable intelligence for Medical Affairs strategy. This creates a dual problem: MSLs are under-equipped before meetings, and the organization fails to capture the full value of its MSL investment after them.

The 2026 market context makes this urgent: pharma is moving to auditable AI, and platforms that cannot demonstrate compliance and traceability will lose procurement decisions. Competitors like Veeva are entrenched but slow; Semalytix is newer and AI-native but lacks MSL workflow depth. ADVANCE AI has the opportunity to own the "integration-first, compliance-native MSL intelligence" category before it consolidates.

### Proposed Solution

Deliver the **ADVANCE AI Integration Hub** in two phases:

**Phase 1 (Q1 2027 — MVP):**
- Pre-built connectors for Veeva Vault CRM (bidirectional) and PubMed/congress feed APIs (read)
- AI-powered post-call insight capture with automated tagging (insight category, sentiment, compliance flag)
- Medical Affairs aggregated insights dashboard with source traceability
- Compliance-gated content delivery: approved content library with audit log

**Phase 2 (Q2–Q3 2027):**
- Epic EHR read integration (formulary context for MSL pre-call briefs)
- MMIT market access data connector (payer/formulary status in pre-call briefs)
- Self-service integration wizard (admin-configured, no-code)
- Agentic pre-call brief generation (mobile-first, offline-capable)
- Insight spike alerts and automated escalation workflows

### Success Metrics

| Metric | Baseline (Pre-launch) | Target (6 months post-Phase 1) |
|---|---|---|
| MSL post-call note completion rate | ~45% (industry benchmark) | ≥75% |
| Time to generate pre-call brief | 45 min (manual) | ≤5 min (AI-assisted) |
| Insight-to-strategy cycle time | 3–4 weeks (manual aggregation) | ≤7 days (AI dashboard) |
| Integration onboarding time (Veeva) | N/A (bespoke) | ≤30 min (self-service wizard) |
| Compliance audit report generation | Manual, days | ≤2 min (automated) |
| Customer NPS (MSL users) | TBD at launch | ≥45 |

### Out of Scope (Phase 1 & 2)

- AI MSL / Digital Human replacements (Syneos/Sageforce.ai model) — ADVANCE AI augments MSLs, not replaces them
- Generic pharma CRM functionality (territory management, call planning) — partner with or integrate into existing CRMs
- Clinical trial management or patient recruitment (separate product category from MSL support)
- Payer contracting or reimbursement analytics beyond formulary status in MSL context
- Direct HCP-facing patient apps or consumer health tools

---

*Requirements based on market analysis conducted 2026-10-26. All competitor claims sourced from public vendor pages, press releases, and industry analyst reports. Internal validation with MSL users and Medical Affairs customers required before development begins.*
