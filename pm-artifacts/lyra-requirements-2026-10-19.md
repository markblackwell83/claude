# Lyra Health: International Requirements Package

**Date:** 2026-10-19
**Prepared for:** Lead International Product Manager, Lyra Health
**Source:** [Lyra market analysis 2026-10-19](lyra-market-analysis-2026-10-19.md)

---

## Feature Opportunity

**Market Configuration Layer for the international rollout of the AI guide and member journey**

The market analysis identified three connected gaps:

1. Lyra plans to expand its clinically vetted AI guide beyond the US through the end of 2026. Each new market needs a localised language, cultural framing, local crisis pathways and regional regulation. Doing that as separate custom builds for each market will not scale.
2. Competitors such as Modern Health, TELUS Health and ComPsych win multinational deals by publishing how many countries and languages they cover and how fast members get access. Lyra does not publish comparable figures for each market.
3. Lyra's international delivery, which includes the footprint acquired with ICAS World, risks relying on manual workarounds outside the core platform. That makes outcomes harder to measure consistently.

**Opportunity:** build a **Market Configuration Layer**. For each market it holds the settings that can change: language and locale, clinical content and crisis pathways, regulatory and consent rules, provider network routing, and AI guide availability. New markets can then be launched through configuration with clinical governance sign-off, rather than through custom engineering. The same layer also produces measures for each market, such as language coverage and time to first session, so they can be shared with members and employer buyers.

This fits the role's focus on localising core capabilities, integrating regional requirements into the core platform, reducing manual workarounds and tracking international cohorts.

---

## User Stories and Acceptance Criteria

### Story 1: International member

**As a** member outside the US, **I want** the AI guide and care journey in my language, with crisis resources for my country, **so that** I can get support I trust without having to translate or adapt US-centred guidance myself.

**Acceptance criteria**

- **Given** a member whose employer contract and profile indicate a supported market, **when** they open the AI guide, **then** the guide responds in their preferred supported language and uses that market's locale formats for dates, times and phone numbers.
- **Given** a member in a supported market expresses risk indicators, **when** the guide escalates, **then** it shows that market's approved local crisis lines and emergency numbers, not US resources such as 988.
- **Given** a member's preferred language is not yet clinically approved for the AI guide, **when** they open the guide, **then** they are told clearly which languages are available and offered a direct route to human support in their language where one exists.
- **Given** any member-facing AI guide content in a localised market, **when** it is shown, **then** it has passed the market's clinical content review and carries an approved version reference.

### Story 2: Clinical Governance lead

**As a** Clinical Governance lead, **I want** to review and approve each market's clinical content, crisis pathways and AI guide behaviour before go-live, **so that** every launch meets local clinical and safety standards.

**Acceptance criteria**

- **Given** a market configuration in draft, **when** it is submitted for launch, **then** it cannot be activated until Clinical Governance has approved the crisis pathways, clinical content and AI guide settings for that market.
- **Given** an approved configuration, **when** any clinical content or crisis pathway changes, **then** the change creates a new version that needs re-approval, and the previous approved version stays live until then.
- **Given** a live market, **when** an auditor requests evidence, **then** the system produces an audit trail of approvals, approvers, dates and versions for that market.

### Story 3: Global benefits lead at an employer

**As a** global benefits lead at a multinational employer, **I want** clear, current information on which countries and languages are supported and how quickly employees can access care, **so that** I can confidently choose Lyra as a single global provider.

**Acceptance criteria**

- **Given** an employer with employees in several countries, **when** the account team prepares a proposal, **then** they can produce a coverage summary for those countries showing supported languages, AI guide availability and the median time to first session over the last 90 days.
- **Given** a market where coverage is partial, **when** the summary is produced, **then** it clearly marks partial coverage and lists the alternative support available, rather than overstating coverage.
- **Given** a live client, **when** the benefits lead views their reporting, **then** they can see adoption and time-to-first-session by country.

### Story 4: Operations and platform teams

**As a** member of an operations or platform team, **I want** to launch a new market through configuration rather than custom code, **so that** we cut manual workarounds and engineering effort for each new market.

**Acceptance criteria**

- **Given** a new market, **when** operations creates its configuration (locale, languages, regulatory and consent rules, provider routing, crisis pathways), **then** it can be tested in a staging environment without code changes for any setting the layer supports.
- **Given** a requirement the layer cannot yet support, **when** it is logged, **then** it is captured as a platform enhancement request with the affected markets, rather than built as a one-off fork.
- **Given** a market with data residency or consent requirements, **when** member data is created, **then** it is stored and processed according to that market's configured rules, and consent is captured in the local language before any processing.

### Story 5: Provider

**As a** provider in a local network, **I want** members referred to me only when they match my languages, credentials and the care types I'm licensed for in my country, **so that** I can deliver appropriate care without mismatched referrals.

**Acceptance criteria**

- **Given** a member in a configured market, **when** the matching service recommends providers, **then** it only returns providers licensed in that market, with matching language capability and an appropriate scope of practice.
- **Given** no suitable local provider is available within the market's target time, **when** matching runs, **then** the member is offered approved alternatives (for example a provider who speaks their language and is licensed to practise there via telehealth) and the gap is logged for network operations.

---

## One-Page Product Spec

### Problem statement

Lyra's AI guide and member journey were built mainly for the US. Expanding to more countries through the end of 2026 means localising language, clinical content, crisis pathways, consent and data handling, and provider routing for every market. Without a shared approach, each launch becomes a custom engineering project. Clinical governance happens case by case, and the business cannot prove coverage or speed of access to buyers. Competitors that publish country and language coverage are winning multinational deals on breadth, while Lyra's clinical advantage is harder to show outside the US.

### Proposed solution

A **Market Configuration Layer** in the core platform that:

1. **Stores market settings:** locale, supported languages, clinical content versions, crisis pathways, consent and data residency rules, provider routing, and AI guide availability.
2. **Builds in clinical governance:** markets can only go live, and content can only change, after Clinical Governance approval, with full versioning and an audit trail.
3. **Routes the member experience:** the AI guide, enrolment, matching and crisis escalation all read from the market configuration rather than hard-coded US logic.
4. **Measures every market:** language coverage, AI guide availability, adoption and time to first session for each market, feeding internal dashboards and employer reporting.
5. **Logs gaps as enhancements:** any requirement the layer can't support is logged as a platform enhancement request, not built as a one-off fork.

Rollout should start with two or three priority markets where Lyra already has demand from global clients, before scaling to others.

### Success metrics

| Metric | Target (first 12 months) |
|---|---|
| Engineering effort to launch a new market | Reduce by 50% compared with the current baseline |
| Markets with the AI guide live in at least one local language | Agreed priority markets live by end of rollout plan |
| Median time to first session in international markets | Within 20% of the US median |
| Members using the AI guide in their own language (in live markets) | 80% or more |
| Manual workarounds logged by operations in live markets | Reduce by 50% |
| Crisis escalations routed to correct local resources | 100%, audited monthly |
| Multinational deals citing coverage as a loss reason | Downward trend, tracked through CRM loss reasons |

### Out of scope

- Building or contracting new provider networks. The layer routes to networks; Network Operations owns network growth.
- Machine translation of clinical content without clinical review. All member-facing clinical content needs human, clinically approved localisation.
- Medication management outside markets where it is already offered.
- Changes to US-specific insurance or claims workflows.
- New AI guide capabilities beyond localisation, such as new therapeutic modules.
