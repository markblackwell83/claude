# Requirements Package: MSL Intelligence & Third-Party Integration Platform

**Date:** 2026-10-05  
**Feature Opportunity:** MSL Agentic Intelligence with Cross-Ecosystem Integration  
**Author:** PM Assistant (Senior Product Strategy)  
**Context:** Based on market-analysis-2026-10-05.md — ADVANCE AI, Product Manager for Third-Party Integrations & MSL Products

---

## Feature Opportunity: Identified from Market Analysis

**Opportunity:** MSL Scientific Insight Agent with Unified Third-Party Integration Layer

**Market Rationale:**
The competitive analysis reveals a clear gap at the intersection of MSL engagement tooling and cross-platform data orchestration. Incumbent platforms (Veeva, X-Fly) provide CRM and engagement tracking but do not synthesize scientific intelligence from field signals. Separately, market access tools (MMIT, Semalytix) surface payer and patient signals but do not reach the MSL workflow layer. No platform currently:
1. Delivers pre-built, maintained integrations across the major pharma data ecosystems (CRM, payer, EHR, RWE, CTMS) from a neutral orchestration position.
2. Uses those integrations to power purpose-built MSL agentic intelligence — proactive scientific question detection, HCP engagement scoring, and evidence gap mapping.

**Strategic Fit with Job Description:**
This opportunity directly spans the two domains the role owns: (1) third-party integrations — the connectors and data pipelines enabling the intelligence layer, and (2) MSL products — the agent-facing workflows and insight surfaces that create user value. Building both together creates a defensible compound moat: integration depth drives intelligence quality; intelligence quality drives integration adoption.

---

## User Stories

### Story 1: MSL Scientific Question Trend Detection

**As an** MSL field team manager,  
**I want** to see real-time trends in the scientific questions HCPs are raising across my region, grouped by indication and therapy area,  
**so that** I can proactively brief my team on emerging evidence gaps and align field messaging before quarterly review cycles.

#### Acceptance Criteria

**Scenario 1: Trend surface on dashboard**  
*Given* I am logged into ADVANCE AI as an MSL manager with at least 5 MSLs reporting to me,  
*When* I navigate to the MSL Intelligence dashboard and select "Scientific Question Trends" for the last 30 days,  
*Then* the system displays a ranked list of scientific topics (minimum 5) with frequency count, trend direction (rising/stable/declining), and sample verbatim questions — all drawn from CRM interaction logs.

**Scenario 2: Alert on emerging topic**  
*Given* a new scientific question category receives 3+ independent field mentions within a 7-day rolling window,  
*When* the system detects the threshold is crossed,  
*Then* the MSL manager receives an in-app notification and (if configured) an email alert within 24 hours, with a link to the trend detail view.

**Scenario 3: No data state**  
*Given* the connected CRM has no interaction logs in the selected period,  
*When* I load the Scientific Question Trends view,  
*Then* the system displays an empty-state message with guidance to sync CRM data and a link to integration settings.

---

### Story 2: Pre-Built CRM Integration Connector

**As a** platform administrator at a pharmaceutical company,  
**I want** to connect ADVANCE AI to our Veeva CRM (or Salesforce Health Cloud) in under 2 hours, with no custom engineering required,  
**so that** our MSL field data flows into ADVANCE AI without burdening our IT team or delaying product rollout.

#### Acceptance Criteria

**Scenario 1: OAuth-based connection setup**  
*Given* I am an ADVANCE AI admin with Veeva CRM system administrator credentials,  
*When* I navigate to Settings > Integrations > Veeva CRM and follow the OAuth authorization flow,  
*Then* the connection is established within 5 minutes, the sync status displays as "Connected," and the first historical data pull (up to 90 days) begins automatically.

**Scenario 2: Field mapping validation**  
*Given* the Veeva CRM connection is established,  
*When* the system performs the initial field mapping,  
*Then* all mandatory fields (HCP ID, interaction date, therapeutic area, notes/verbatims) are auto-mapped with >95% accuracy, and any unmapped fields are surfaced for manual review in an on-screen field-mapping UI.

**Scenario 3: Sync failure alerting**  
*Given* a previously established Veeva CRM connection loses API access (e.g., token expiry, permission change),  
*When* a scheduled sync fails,  
*Then* the admin receives an email and in-app alert within 1 hour identifying the failure reason, with a one-click re-authentication link.

---

### Story 3: HCP Engagement Scoring for MSL Prioritization

**As a** Medical Science Liaison,  
**I want** to see an AI-generated engagement score for each HCP in my territory, reflecting recency of interaction, scientific interest depth, and alignment to my product's key indication,  
**so that** I can prioritize high-value HCP visits and deprioritize relationships where engagement has plateaued.

#### Acceptance Criteria

**Scenario 1: Score display on HCP profile**  
*Given* I am an MSL viewing my territory's HCP list,  
*When* I open any HCP profile with at least 2 logged interactions,  
*Then* the profile displays an engagement score (0–100 scale), a score trend (up/down vs. prior 90 days), and the top 3 factors contributing to the score (e.g., "3 interactions in 30 days," "high scientific question volume," "key opinion leader publication activity").

**Scenario 2: Territory prioritization view**  
*Given* I navigate to "My Territory" in the MSL dashboard,  
*When* I apply the "Engagement Score" sort,  
*Then* HCPs are ranked highest-to-lowest by score, with the ability to filter by indication area, score tier (High/Medium/Low), and last interaction date.

**Scenario 3: Score recalculation on new data**  
*Given* a new CRM interaction is logged for an HCP,  
*When* the nightly data refresh completes,  
*Then* the HCP's engagement score is recalculated and the profile reflects the updated score by 6:00 AM local time the following day.

---

### Story 4: Unified MSL + Market Access Intelligence Briefing

**As a** Medical Affairs director,  
**I want** a weekly auto-generated briefing that combines MSL field insights (scientific questions, HCP engagement trends) with market access signals (payer policy changes, formulary updates for my product),  
**so that** I can identify cross-functional opportunities — for example, where strong HCP scientific interest aligns with formulary restrictions that need addressing.

#### Acceptance Criteria

**Scenario 1: Weekly briefing delivery**  
*Given* both a CRM integration and a market access data integration (MMIT or equivalent) are configured and active,  
*When* Monday morning arrives (8:00 AM user local time),  
*Then* the Medical Affairs director receives an automated email briefing summarizing: top 3 MSL field topics from the prior week, any payer policy changes affecting covered products, and a "cross-functional spotlight" section flagging HCP indication areas with concurrent formulary changes.

**Scenario 2: Briefing customization**  
*Given* I am a Medical Affairs director in briefing settings,  
*When* I configure my briefing preferences,  
*Then* I can select: delivery day/time, included products, included geographic regions, and whether to include market access data, MSL data, or both — and the briefing reflects those preferences within the next scheduled generation.

**Scenario 3: No market access integration active**  
*Given* the CRM integration is active but no market access integration is configured,  
*When* the briefing is generated,  
*Then* the briefing omits the market access section and displays a call-to-action: "Connect MMIT or a compatible market access source to unlock cross-functional insights."

---

### Story 5: Evidence Gap Mapping for MSL-Supported Publications

**As an** MSL,  
**I want** to see a visual map of evidence gaps in my indication area — based on aggregated HCP questions that lack corresponding approved publications or data packages —  
**so that** I can flag high-priority evidence gaps to the Medical Affairs team for publication planning or data generation initiatives.

#### Acceptance Criteria

**Scenario 1: Evidence gap map generation**  
*Given* at least 10 HCP interaction records with scientific question tags are available for a given indication,  
*When* I navigate to "Evidence Gap Map" for that indication,  
*Then* the system displays a categorized map of question clusters with: question volume, coverage status (Covered / Partially Covered / Gap), and linked approved publications where coverage exists.

**Scenario 2: Gap flagging workflow**  
*Given* I identify a question cluster marked as "Gap" in the Evidence Gap Map,  
*When* I click "Flag as Evidence Priority,"  
*Then* a structured evidence gap request is created and routed to the Medical Affairs team's review queue, with the question cluster summary, supporting verbatims, and my MSL territory data pre-populated.

**Scenario 3: Coverage status update**  
*Given* the Medical library integration is active and a new publication is approved and uploaded,  
*When* the system indexes the new publication content,  
*Then* any Evidence Gap Map entry whose question cluster is addressed by the new publication is updated from "Gap" to "Covered" within 48 hours, with a notification sent to any MSL who previously flagged that gap.

---

## One-Page Product Spec: MSL Intelligence Agent with Integration Layer

### Problem Statement

Medical Science Liaisons operate at the intersection of scientific communication and field intelligence — yet the tools they use today fragment these functions across disconnected systems. CRM platforms (Veeva, Salesforce) capture engagement activity but provide no intelligence layer. Market access tools surface payer signals but are inaccessible to field teams. The result: MSLs manually compile insights from multiple tools, Medical Affairs leadership lacks a cross-functional view, and field-generated scientific intelligence — one of the most valuable proprietary assets a pharma company has — is not systematically captured or actioned.

Simultaneously, pharmaceutical organizations struggle to integrate their existing data ecosystems with new AI platforms. Implementation timelines of 6-18 months for custom integrations delay time-to-value and create dependency on scarce IT resources.

### Proposed Solution

Build **ADVANCE AI MSL Intelligence Agent** — a purpose-built agentic AI layer for Medical Science Liaisons, powered by pre-built third-party integrations with the major pharma data ecosystems.

**Core components:**
1. **Integration Hub** — Pre-built, maintained connectors for Veeva CRM, Salesforce Health Cloud, MMIT, and IQVIA; OAuth-based setup in <2 hours; nightly sync with anomaly alerts.
2. **MSL Intelligence Agent** — AI agent that continuously analyzes field interaction data to surface: scientific question trends by indication, HCP engagement scores, and evidence gap maps.
3. **Unified Briefings** — Auto-generated weekly Medical Affairs briefings combining MSL field signals with market access/payer intelligence.
4. **Evidence Gap Workflow** — Structured pipeline for MSLs to flag evidence gaps, routed to publication planning queues.

### Success Metrics

| Metric | Baseline | Target (6 months post-launch) |
|---|---|---|
| Integration setup time | 6-18 months (custom) | <2 hours (self-serve) |
| MSL time spent on manual data compilation per week | ~4 hours | <1 hour |
| Scientific question trends surfaced per month | 0 (not tracked) | ≥10 per indication |
| Cross-functional briefing open rate | N/A | ≥60% |
| Evidence gap flags routed to Medical Affairs per quarter | Manual / ad hoc | ≥20 structured requests |
| Customer NPS (MSL users) | Baseline TBD at launch | ≥45 |

### Out of Scope (v1)

- Direct EHR read/write integration (HIPAA complexity; phased to v2)
- Real-time CRM sync (nightly batch sufficient for v1 intelligence use cases)
- Patient-level data ingestion (patient voice layer is a v2 feature, dependent on Semalytix-style pipeline or equivalent)
- Regulatory submission workflow automation (separate product surface; not MSL-layer)
- Non-pharma/MedTech market expansion
- Custom integration build service (SI partnerships are the path for non-standard connectors)
