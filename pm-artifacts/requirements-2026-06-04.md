# ADVANCE AI — Requirements Package
**Date:** 2026-06-04  
**Feature Opportunity:** Medical Intelligence Integration Hub for MSL Teams  
**Linked Analysis:** [market-analysis-2026-06-04.md](market-analysis-2026-06-04.md)

---

## Feature Opportunity: Real-Time Field Insight Capture & Routing

### Why This Opportunity

The market analysis identified a consistent, high-value gap: MSL field insights are systematically lost or delayed. Meeting notes sit in static CRM fields, KOL rosters are off by 30%+, and insight-to-strategy latency runs weeks. No competitor has solved the full loop — from structured field capture to intelligent enterprise routing — in a compliance-native, integration-ready platform.

This feature directly addresses the ADVANCE AI PM charter: **third-party integrations** (connecting to Veeva, Salesforce, EHR systems) and **MSL products** (tooling for the MSL persona). It also aligns with McKinsey's estimate of $3–5B annual Medical Affairs efficiency gains available from GenAI, and with the market's shift from copilot to agentic AI.

The feature is scoped as a **Medical Intelligence Integration Hub** — an MSL-facing workflow layer that captures field insights in a structured, AI-assisted format and routes them in real time to the right enterprise consumers (medical strategy, commercial, clinical development, regulatory).

---

## User Stories

### Story 1 — Structured Insight Capture After KOL Meetings

**As an** MSL completing a Key Opinion Leader engagement,  
**I want** to quickly log my meeting insights in a guided, AI-assisted form that auto-suggests categories, sentiment, and follow-up actions,  
**So that** my observations are captured accurately and consistently without adding significant documentation burden to my field time.

#### Acceptance Criteria

```
Given I have completed a KOL meeting and open the insight capture screen,
When I begin entering free-text notes,
Then the AI should surface 3–5 suggested insight categories (e.g., "unmet need," "competitive mention," "label concern," "trial interest") based on the note content.

Given the AI has suggested categories,
When I accept or override one or more suggestions,
Then my selections and the final note are saved with a structured schema (timestamp, HCP ID, therapy area, insight type, sentiment, verbatim) to the central insights store.

Given the insight is saved,
When a compliance trigger keyword is detected (e.g., adverse event mention, off-label discussion),
Then the system automatically flags the insight for compliance review and notifies the relevant compliance officer within 15 minutes.
```

---

### Story 2 — Automated Insight Routing to Enterprise Stakeholders

**As a** Medical Affairs strategy lead,  
**I want** field insights from all MSLs to be automatically classified and routed to relevant teams (clinical development, commercial, regulatory, medical information) based on content,  
**So that** strategic signals from the field are visible to decision-makers within hours, not weeks.

#### Acceptance Criteria

```
Given an MSL has submitted a tagged field insight,
When the platform classifies the insight type (e.g., clinical evidence gap, competitor intel, HCP sentiment),
Then the insight is automatically routed to the pre-configured stakeholder group for that type within 30 minutes of submission.

Given a routed insight is received by a stakeholder,
When the stakeholder views and acknowledges it,
Then the submitting MSL receives confirmation that their insight reached the intended audience, closing the feedback loop.

Given 10 or more insights on the same topic or HCP segment are received within a 7-day window,
When the system detects the pattern,
Then an auto-generated trend summary is surfaced to the Medical Affairs lead as a priority signal.
```

---

### Story 3 — EHR-Embedded MSL Request Button for HCPs

**As an** HCP managing a complex patient case,  
**I want** to request real-time scientific support from the relevant MSL directly from within my EHR workflow,  
**So that** I can access the most current clinical evidence and off-label safety data without leaving my point-of-care system.

#### Acceptance Criteria

```
Given an HCP is viewing a patient record in a connected EHR system,
When they click the embedded "Request MSL Support" action,
Then a support request is created in ADVANCE AI, pre-populated with the HCP's NPI, specialty, and (de-identified) therapeutic context, and the assigned MSL is notified within 2 minutes.

Given the MSL receives the request notification,
When they accept the engagement,
Then the HCP receives an in-EHR acknowledgement with the MSL's name, response SLA, and a secure async channel for follow-up.

Given the HCP interaction is complete,
When the MSL closes the engagement,
Then the full interaction summary is automatically logged as a structured field insight in the platform, attributed to the HCP, and flagged for any compliance review triggers.
```

---

### Story 4 — Integration Connector for Veeva / Salesforce CRM Sync

**As a** Medical Affairs operations manager,  
**I want** MSL field insights captured in ADVANCE AI to automatically sync to our existing Veeva Vault CRM (or Salesforce Life Sciences Cloud) records,  
**So that** the field team does not have to enter data twice and our CRM remains the system of record for downstream reporting.

#### Acceptance Criteria

```
Given an MSL submits a completed field insight in ADVANCE AI,
When the platform detects an active Veeva or Salesforce integration for the customer's tenant,
Then the insight is translated to the target CRM's data model and synced within 5 minutes, with a conflict-resolution log if a duplicate record exists.

Given a CRM sync completes,
When the MSL views the insight in ADVANCE AI,
Then the record displays a "Synced to [CRM name]" status badge with a timestamp and a deep-link to the CRM record.

Given the integration is configured for bidirectional sync,
When a field is updated in the CRM (e.g., HCP contact details changed),
Then the corresponding record in ADVANCE AI is updated within 15 minutes, with the source of change logged in the audit trail.
```

---

### Story 5 — Compliance-Auditable Insight Trail

**As a** pharma compliance officer,  
**I want** every field insight — from initial capture through routing, review, and CRM sync — to have a complete, immutable audit trail,  
**So that** I can demonstrate regulatory compliance (21 CFR Part 11, GDPR) during audits without manual reconstruction of records.

#### Acceptance Criteria

```
Given any field insight record exists in the system,
When I access the audit trail for that record,
Then I can see every state transition (created, edited, flagged, reviewed, routed, synced, archived) with timestamps, actor identities, and change diffs.

Given a compliance audit is initiated,
When I export the audit trail for a specified date range and MSL roster,
Then I receive a structured, tamper-evident report (PDF + JSON) within 10 minutes, covering all relevant records.

Given a record is flagged for compliance review,
When the reviewing officer closes the review with a decision (cleared/escalated),
Then the decision, rationale, and reviewer identity are permanently appended to the record and cannot be deleted or modified.
```

---

## One-Page Product Spec: Medical Intelligence Integration Hub

### Problem Statement

Medical Affairs teams are generating significant field intelligence through MSL engagements — but this intelligence is routinely lost, delayed, or siloed. MSLs spend 30–40% of their admin time on manual documentation. KOL rosters are off by 30%+ due to stale data. Field insights take weeks to reach the strategic teams who need them. The platforms MSLs use daily (CRM, EHR, literature tools) do not talk to each other, creating duplication and compliance risk. The result: Medical Affairs functions as a cost center rather than the strategic intelligence asset it could be.

### Proposed Solution

Build the **Medical Intelligence Integration Hub** as a core capability of the ADVANCE AI platform — an MSL-facing workflow layer with four components:

1. **AI-assisted structured insight capture** — guided post-meeting logging with auto-categorization, sentiment detection, and compliance flagging
2. **Intelligent routing engine** — rules-based + AI-classified routing of insights to the right enterprise stakeholders (medical strategy, clinical development, commercial, regulatory) in real time
3. **EHR integration layer** — embedded HCP-to-MSL request widgets in connected EHR systems, enabling point-of-care scientific support requests that auto-generate structured field records
4. **CRM bidirectional sync** — pre-built connectors to Veeva Vault CRM and Salesforce Life Sciences Cloud, eliminating double-entry and maintaining CRM as system of record

All components share a single compliance-auditable data layer with immutable audit trails meeting 21 CFR Part 11 and GDPR requirements.

### Success Metrics

| Metric | Baseline (Current) | Target (6 months post-launch) |
|---|---|---|
| MSL documentation time per field interaction | ~25 min | ≤ 10 min |
| Insight-to-stakeholder routing latency | Days to weeks | < 1 hour (P90) |
| KOL data accuracy (vs. validated external source) | ~70% (industry avg.) | ≥ 90% |
| CRM data duplication rate | High (manual) | < 2% |
| Compliance audit prep time | ~3 days (manual) | < 30 min (automated export) |
| MSL NPS for platform | Baseline TBD | ≥ 8.0 / 10 |

### Out of Scope

- Replacing the customer's existing CRM (Veeva or Salesforce) — ADVANCE AI integrates with, not replaces, the CRM
- Direct HCP-facing patient communication or telehealth functionality
- Clinical trial enrollment or CTMS functionality
- Drug safety / pharmacovigilance case processing (PV workflows are flagged to existing PV systems, not managed in-platform)
- Custom EHR development for non-standard EHR systems in the first release; GA scope targets Epic, Cerner (Oracle Health), and Veeva Vault integrations only
