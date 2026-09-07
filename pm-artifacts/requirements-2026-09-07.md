# Requirements Package: MSL Pre-Call Intelligence & Integration Hub

**Date:** 2026-09-07  
**Prepared for:** ADVANCE AI Product Team  
**Feature Opportunity:** Unified MSL Pre-Call Intelligence Layer with Third-Party Data Integration  
**Role Context:** Product Manager, Third-Party Integrations & MSL Products

---

## Feature Opportunity

**Identified Gap:** MSLs today navigate 3–5 disconnected tools (CRM, literature databases, KOL profiling platforms, payer access tools, RWE dashboards) before every HCP engagement. No single platform delivers a compliant, audit-trail-native, CRM-embedded pre-call intelligence brief that synthesizes all these signals. ADVANCE AI's dual mandate — third-party integrations + MSL product ownership — makes this the natural first-mover opportunity.

**Strategic Rationale:**
- The five core MSL AI workflows (literature monitoring, KOL insights, pre-meeting briefs, MI response drafting, congress coverage) are validated by field research but served by separate tools.
- RAG-based compliance-safe content generation is now the procurement standard for Medical Affairs AI.
- Veeva CRM and Salesforce are the dominant MSL workflow environments; embedding intelligence here eliminates adoption friction.
- Mid-market biotechs (Series B through commercial launch) are underserved by MMIT/IQVIA pricing and represent a high-growth segment.

---

## User Stories

### Story 1: MSL Pre-Call Scientific Brief
**As an** MSL preparing for an HCP engagement,  
**I want** a single-click, CRM-triggered scientific brief that summarizes the HCP's recent publications, congress presentations, and stated clinical interests alongside my product's current evidence landscape,  
**so that** I can walk into every meeting with a personalized, scientifically current conversation plan without spending 45+ minutes across multiple tools.

#### Acceptance Criteria

**Given** an MSL is viewing an HCP record in Veeva CRM or Salesforce,  
**When** they trigger "Generate Pre-Call Brief" (via button or embedded agent),  
**Then** the system retrieves and synthesizes: the HCP's last 12 months of publications (PubMed/EMBASE), their therapeutic area focus, the current product label and approved medical communications, and relevant RWE summaries — and returns a formatted brief in under 60 seconds.

**Given** the brief is generated,  
**When** it contains any AI-synthesized content,  
**Then** every claim includes a traceable source citation, a confidence indicator, and a human-review flag if the source was published within 30 days.

**Given** the brief is viewed,  
**When** the MSL marks it as used for an HCP interaction,  
**Then** the system logs a full audit trail (user, timestamp, content version, sources used) accessible to Medical Affairs compliance leads.

---

### Story 2: Integration Configuration for Medical Affairs Ops Teams
**As a** Medical Affairs Operations Manager,  
**I want** a self-service integration configuration panel that connects ADVANCE AI to our organization's Veeva Vault, approved content libraries, and RWE data feeds without requiring engineering resources,  
**so that** we can go live with MSL AI tooling within a 2-week onboarding window and maintain data source governance independently.

#### Acceptance Criteria

**Given** an admin user with Medical Affairs Ops permissions,  
**When** they access the Integration Hub dashboard,  
**Then** they can view, connect, and configure pre-built connectors for: Veeva CRM, Veeva Vault MedComms, Salesforce Health Cloud, PubMed, EMBASE, and a generic secure SFTP/API endpoint for proprietary RWE data — all without writing code.

**Given** a connector is configured,  
**When** a data sync is triggered (manual or scheduled),  
**Then** the system validates data schema compatibility, reports sync success/failure with field-level error detail, and surfaces a data freshness timestamp on all downstream MSL briefs.

**Given** a data source is deactivated or credentials expire,  
**When** an MSL attempts to generate a brief,  
**Then** the system clearly flags which data sources are unavailable and generates a partial brief from active sources only, with an explicit provenance gap warning.

---

### Story 3: KOL Scientific Profile and Engagement Tracker
**As an** MSL managing a KOL territory,  
**I want** a continuously updated scientific profile for each KOL that tracks their publication trajectory, congress activity, clinical trial involvement, and previous MSL interaction outcomes,  
**so that** I can prioritize engagement, identify inflection points in their scientific interest, and build a longitudinal relationship record that persists across MSL team transitions.

#### Acceptance Criteria

**Given** an MSL opens a KOL record,  
**When** the profile page loads,  
**Then** it displays: a 24-month publication timeline with therapeutic area tagging, a list of clinical trials where the KOL is listed as PI or co-investigator (pulled from ClinicalTrials.gov), a congress presentation history (last 3 years), and a sentiment-neutral summary of their public scientific position on key disease area topics — all updated within the prior 7 days.

**Given** an MSL logs a completed HCP interaction,  
**When** they tag key discussion topics and outcomes,  
**Then** those topics are mapped to the KOL's scientific profile, surfacing alignment or divergence from the KOL's published positions, and the interaction is stored with full audit trail for Medical Affairs oversight.

**Given** a KOL's publication or trial activity changes significantly,  
**When** the system detects a new publication, PI listing, or congress abstract submission,  
**Then** the assigned MSL receives a configurable alert (email, CRM notification, or in-app) within 24 hours of detection.

---

### Story 4: Compliant Medical Information Response Drafting
**As an** MSL who has received an unsolicited medical information request from an HCP,  
**I want** a RAG-powered drafting assistant that generates a response grounded exclusively in approved label content and approved medical communications,  
**so that** I can respond accurately and quickly while maintaining full off-label guardrails and audit compliance required by Medical Affairs.

#### Acceptance Criteria

**Given** an MSL opens a new Medical Information Request in the platform,  
**When** they describe the HCP's question in natural language,  
**Then** the system retrieves only from the configured approved content corpus (label, approved MSL materials, Medical Affairs-approved RWE summaries) and generates a draft response with source citations for every factual claim.

**Given** a draft response is generated,  
**When** the content corpus does not contain material to answer the question,  
**Then** the system explicitly states the query is outside the approved content scope, suggests escalation to the Medical Information team, and does not hallucinate or extrapolate beyond the approved corpus.

**Given** the MSL edits and submits the response,  
**When** the submission is confirmed,  
**Then** the system logs: original request text, generated draft, MSL edits made, final submitted text, HCP identifier (anonymized where required), and timestamp — all exportable for regulatory inspection.

---

### Story 5: Cross-Platform Analytics for Medical Affairs Leadership
**As a** Head of Medical Affairs,  
**I want** a real-time dashboard that aggregates MSL engagement metrics, scientific topic trends across KOL conversations, and integration data quality scores across all connected third-party systems,  
**so that** I can identify gaps in our scientific engagement strategy, ensure data quality across our tool stack, and report field intelligence to internal stakeholders without manual data aggregation.

#### Acceptance Criteria

**Given** a Medical Affairs leadership user opens the Analytics Dashboard,  
**When** the dashboard loads,  
**Then** it displays: MSL engagement volume by territory and therapeutic area (rolling 90 days), top 10 scientific topics discussed by frequency, integration health scores for all connected data sources, and average pre-call brief generation latency — all filterable by time period, product, and geography.

**Given** an integration health score falls below a configurable threshold (default: 85%),  
**When** the system detects the degradation,  
**Then** it automatically alerts the Medical Affairs Ops admin via email and surfaces a warning banner in the MSL brief UI, preventing reliance on stale data without blocking MSL workflows.

---

## One-Page Product Spec: MSL Pre-Call Intelligence Hub

### Problem Statement

MSLs spend 30–60 minutes per HCP engagement gathering scientific context from 3–5 disconnected systems. This manual aggregation is error-prone, inconsistent across the team, leaves no audit trail, and creates compliance exposure when MSLs inadvertently reference unapproved content. Medical Affairs leadership has no visibility into what scientific content is being used in field engagements. ADVANCE AI's integration mandate makes this the highest-leverage problem to solve: we own the data connections, so we can own the synthesis layer.

### Proposed Solution

Build a **MSL Pre-Call Intelligence Hub** as an embedded agent experience within Veeva CRM and Salesforce, powered by:

1. **Integration Layer:** Pre-built, no-code connectors to Veeva CRM, Veeva Vault MedComms, Salesforce Health Cloud, PubMed, EMBASE, ClinicalTrials.gov, and configurable RWE data feeds.
2. **RAG Engine:** Retrieval-augmented generation grounded exclusively in the organization's approved content corpus, with hard guardrails preventing out-of-corpus synthesis.
3. **Brief Generator:** Single-click pre-call brief combining HCP scientific profile, current evidence landscape, and approved messaging — returned in <60 seconds.
4. **Audit Engine:** Full provenance logging for every brief generated, content used, and MSL action taken — exportable for regulatory inspection.
5. **KOL Intelligence:** Continuous background monitoring of KOL publication and congress activity with configurable MSL alerts.

**Delivery approach:** Start with Veeva CRM embedded agent (Phase 1, Q4 2026), then expand to Salesforce Health Cloud (Phase 2, Q1 2027) and standalone web app for non-CRM users (Phase 3, Q2 2027).

### Success Metrics

| Metric | Baseline | 6-Month Target | 12-Month Target |
|---|---|---|---|
| Average MSL pre-call prep time | 45 min | 15 min | 8 min |
| Brief adoption rate (briefs generated / MSL-HCP interactions logged) | 0% | 40% | 75% |
| Audit trail coverage (interactions with full provenance log) | 0% | 100% | 100% |
| Integration connector uptime SLA | — | 99.5% | 99.9% |
| Customer NPS (MSL users) | — | >40 | >55 |
| Mid-market customers onboarded (<500-person pharma companies) | — | 3 | 10 |

### Out of Scope (v1)

- Promotional content generation (hard boundary — Medical Affairs only, not Sales)
- Autonomous MSL agent that engages HCPs without human initiation
- Integration with non-standard or proprietary CRM systems beyond Veeva and Salesforce
- Patient-facing tools or direct-to-patient communications
- Drug discovery or clinical trial design features
- Automatic regulatory submission preparation

---

*This requirements package is grounded in the market analysis dated 2026-09-07. All feature decisions should be validated against current compliance requirements in target markets before engineering commitment.*
