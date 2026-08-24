# ADVANCE AI — Requirements Package
**Feature:** Neutral MSL Insight Orchestration Layer (working name: **Insight Bridge**)
**Date:** 2026-08-24
**Author:** Product Manager, Third-Party Integrations & MSL Products
**Related:** `market-analysis-2026-08-24.md` — Opportunity A (integration orchestration) and Opportunity B (compliance-grade agentic MSL)

---

## Feature Opportunity

The market analysis surfaces two converging gaps that no single vendor is closing today:

1. **The split CRM landscape.** Pharma customers now maintain two credible CRM architectures (Veeva Vault CRM Medical vs. Salesforce LSC4CE) and are pulling in specialist data (MMIT-class market access, Semalytix-class patient voice, TrialHub-class feasibility). No vendor is a first-class citizen inside both CRMs while also brokering specialist data at the point of MSL interaction.
2. **The compliance envelope.** Buyers want agentic MSL workflows but disqualify vendors that cannot show retrieval grounding, prompt-version logs, human-in-the-loop checkpoints, and MLR-ready evidence packs.

**Insight Bridge** is the productization of both: a CRM-neutral orchestration layer that pipes third-party evidence (market access, patient voice, trial feasibility, EHR via FHIR) into whichever CRM the MSL is already working in, and wraps every AI action in a compliance envelope the customer's Medical/Legal/Regulatory team will actually sign off on.

This directly serves the role we are staffing for: "third-party integrations and MSL products," "supporting sales conversations about integration capabilities," and "partnering with compliance on regulatory requirements."

---

## User Stories

### US-1 — MSL pre-meeting brief across data sources
**As an** MSL preparing for a KOL visit,
**I want** a single AI-generated brief that pulls the KOL's recent publications, congress activity, formulary status of my product across their payers, and the latest global patient-voice signals for the indication,
**so that** I walk into the meeting with a scientifically precise, market-aware point of view without stitching five tools together the night before.

### US-2 — CRM-neutral write-back of MSL interactions
**As an** MSL working inside my company's chosen CRM (Vault CRM Medical **or** Salesforce LSC4CE),
**I want** Insight Bridge to write my interaction summary, next-best-action, and cited evidence back into the CRM record I already own,
**so that** I never have to duplicate-enter data and my Medical Affairs leadership sees a consolidated view regardless of which CRM they audit.

### US-3 — Compliance-grade grounding and audit trail
**As a** Medical Affairs Compliance Lead,
**I want** every AI-generated output to expose its retrieval sources, the exact prompt/model version used, and every human-in-the-loop decision,
**so that** I can defend the workflow to internal MLR review and external inspectors without commissioning a bespoke audit.

### US-4 — Third-party data partner onboarding
**As a** Product Manager for third-party integrations,
**I want** a self-service connector SDK and certification path for market-access, patient-voice, and trial-feasibility data partners,
**so that** we can onboard new data sources (e.g. MMIT-class, Semalytix-class, TrialHub-class) in weeks rather than negotiating a bespoke integration each time.

### US-5 — Sales-supporting integration story
**As an** Account Executive in an enterprise sales cycle,
**I want** a live demo environment that shows Insight Bridge running end-to-end against a customer's stated CRM and two of their preferred data sources,
**so that** I can close the "does it work with what we already have?" objection in the first technical evaluation call.

---

## Acceptance Criteria (Given / When / Then)

### AC for US-1 — Pre-meeting brief
- **Given** an MSL has a scheduled interaction with a KOL in the CRM, **when** they open the KOL record inside Insight Bridge, **then** a pre-meeting brief is generated within 15 seconds containing: KOL's last 10 relevant publications, congress presentations in the last 12 months, formulary/coverage status for the MSL's product across the KOL's affiliated payers, and a summary of patient-voice signals for the indication with source citations.
- **Given** the brief is generated, **when** any citation is clicked, **then** the source (PubMed record, congress abstract, MMIT-class policy, Semalytix-class report) opens in a side panel with the exact retrieved passage highlighted.
- **Given** an evidence source is unavailable at generation time (e.g. a data-partner API is down), **when** the brief is rendered, **then** the affected section shows an explicit "source unavailable — no synthesis attempted" placeholder rather than a fabricated summary.

### AC for US-2 — CRM-neutral write-back
- **Given** a customer has connected either Vault CRM Medical or Salesforce LSC4CE, **when** an MSL saves an interaction summary in Insight Bridge, **then** the summary, next-best-action, and full citation list are written to the corresponding CRM interaction record within 30 seconds.
- **Given** the write-back succeeds, **when** the record is opened in the native CRM UI, **then** the interaction summary, next-best-action, and a link back to the Insight Bridge audit view are visible without additional CRM configuration by the customer.
- **Given** a write-back fails (auth, schema, network), **when** the failure is detected, **then** the MSL sees a non-blocking error, the summary is preserved in Insight Bridge, and the failed write is queued for retry with exponential backoff; no data is silently dropped.

### AC for US-3 — Compliance grounding and audit
- **Given** any AI-generated output is produced, **when** the audit console is opened for that output, **then** it shows: retrieval sources with document IDs and timestamps, the prompt template ID and version, the model ID and version, any human edits or approvals with reviewer identity and timestamp, and a monotonically increasing event log ID.
- **Given** a Compliance Lead requests an evidence pack for an interaction, **when** they click "Export MLR pack," **then** a signed, timestamped PDF+JSON bundle is produced within 60 seconds containing every artifact in the audit console for that interaction.
- **Given** a model or prompt template is updated, **when** the change is deployed, **then** the version delta is recorded in a change log accessible to the Compliance Lead, and prior audit records continue to resolve to their original versions.

### AC for US-4 — Partner connector SDK
- **Given** a new third-party data partner, **when** they use the connector SDK, **then** they can implement a certified connector (authentication, entity mapping, rate-limit handling, source-citation contract) end-to-end in ≤10 engineering days per the SDK's reference implementation.
- **Given** a partner submits a connector for certification, **when** the automated certification suite runs, **then** it validates auth flow, schema mapping, citation contract, PII handling, and error semantics; a certification report is produced automatically.
- **Given** a customer enables a certified partner connector, **when** they turn it on in the admin console, **then** the new data source is available to MSLs inside pre-meeting briefs within 5 minutes without requiring a redeploy.

### AC for US-5 — Sales demo environment
- **Given** an AE is preparing for a technical evaluation, **when** they request a demo environment via the sales portal, **then** a fully provisioned demo tenant with either Vault CRM Medical or Salesforce LSC4CE and two selected data partners is available within 2 business hours.
- **Given** the demo environment is provisioned, **when** the AE walks through the end-to-end MSL flow (record open → brief → interaction → write-back → audit export), **then** each step completes with representative sample data and no manual patching.

---

## One-Page Product Spec — Insight Bridge (MVP)

### Problem statement
Medical Science Liaisons in 2026 are asked to bring scientifically precise, market-aware, patient-informed conversations into every KOL interaction — but their tooling is fragmented across a CRM (Vault or Salesforce), a payer/formulary data source, a patient-voice source, a trial-feasibility source, and PubMed/congress trackers. Assembling the picture manually is slow, error-prone, and compliance-fragile; the ungrounded GenAI shortcut is disqualifying for MLR. As a result, MSLs either under-prepare or over-invest hours per meeting, and Medical Affairs leadership cannot produce a defensible audit trail of the AI's role in scientific exchange.

### Proposed solution
**Insight Bridge** is a CRM-neutral orchestration layer that (a) integrates natively with Vault CRM Medical and Salesforce LSC4CE, (b) brokers third-party market-access, patient-voice, and trial-feasibility data via a certified connector SDK, and (c) wraps every agentic MSL workflow — pre-meeting briefs, interaction summaries, next-best-action — in a compliance envelope (retrieval-only grounding, prompt/model versioning, human-in-the-loop checkpoints, MLR-ready evidence packs). MVP scope: US-1 through US-5 above, with Vault and Salesforce connectors and three certified data-partner categories (market access, patient voice, trial feasibility).

### Success metrics
- **Adoption.** ≥70% of pilot MSLs use Insight Bridge for at least 3 KOL interactions per week by end of the 90-day pilot.
- **Time-to-brief.** Median wall-clock time from "open KOL record" to "brief ready" ≤20 seconds across pilot tenants.
- **Compliance defensibility.** 100% of AI-generated outputs export a complete MLR pack on demand; zero MLR failures attributed to Insight Bridge grounding in the first 6 months of GA.
- **Integration reach.** 2 CRM platforms and 3 certified data-partner categories live at GA; ≥5 additional certified connectors within 6 months.
- **Sales velocity.** ≥30% reduction in enterprise technical-evaluation cycle time for opportunities where Insight Bridge is in scope.
- **MSL productivity.** ≥40% reduction in self-reported pre-meeting prep time in pilot survey.

### Out of scope (MVP)
- Building a full replacement CRM (Insight Bridge integrates with, not replaces, Vault/Salesforce/IQVIA OCE).
- Direct HCP-facing chat interfaces (all agentic outputs remain MSL-facing with human-in-the-loop).
- Autonomous MLR approval (Insight Bridge produces MLR pre-flight checks and evidence packs; final approval remains with human MLR reviewers).
- Commercial rep workflows and promotional-content generation (Medical Affairs / MSL only for MVP).
- Non-English UI localization (targeted for a Phase 2 release; data-partner content in other languages is still surfaced through the brief).
- Custom fine-tuned model training per customer (MVP relies on retrieval-grounded prompting over a shared, versioned model roster).

### Key open questions for follow-up
- Should the MVP include an IQVIA OCE Scientific connector, or defer to Phase 2 to keep the release surface tight?
- What is the minimum data-partner set required to be credible to a top-20 pharma buyer — one per category, or two per category for competitive optionality?
- What is the right split between managed-service partner onboarding and pure self-service SDK for our first 10 connectors?
