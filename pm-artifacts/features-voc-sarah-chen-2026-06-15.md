# Feature Descriptions — Derived from VoC: Dr. Sarah Chen (MSL)
**Date:** 2026-06-15
**Source:** Simulated customer interview, ADVANCE AI Voice of the Customer
**Persona:** Dr. Sarah Chen — MSL, Novex Biopharma (UK-based, Pacific NW territory)

---

## F1 — Post-Call AI Summary Generation

Automatically generate a structured meeting summary from an ADVANCE AI-analysed field conversation (in-person or remote), covering key topics discussed, HCP questions raised, clinical insights captured, and agreed follow-up actions.

**Problem solved:** MSLs currently reconstruct meeting content from memory hours after the call, degrading accuracy and costing 15–25 minutes per interaction.

**Applies to:** Remote (video) and in-person meetings where ADVANCE AI analysis is active.

**Key constraint:** Summary must be available for MSL review before any data leaves the platform.

---

## F2 — MSL Review & Edit Before CRM Sync

Present the AI-generated meeting summary to the MSL in a review interface — with the ability to edit, annotate, or reject individual fields — before any content is written to the CRM.

**Problem solved:** MSLs will not trust or adopt AI-generated CRM entries without a review step. Auto-sync without review is a non-starter for professional and compliance reasons.

**UX requirement:** Review should take under 5 minutes. Optimise for confirmation, not re-entry — the MSL should be approving, not rewriting.

---

## F3 — Veeva CRM Auto-Sync (Post-Review)

Push reviewed and approved meeting summaries directly into the correct Veeva CRM fields, mapped to the relevant HCP record, without requiring the MSL to re-enter data manually.

**Problem solved:** MSLs currently maintain shadow documentation (iPhone Notes, personal docs) and perform manual double-entry into Veeva. This workflow is time-consuming, compliance-risky, and produces lower-quality records.

**Integration requirement:** Field mapping must align with the customer's Veeva data model. Conflict handling required for records modified in Veeva between meeting and sync.

---

## F4 — AI vs. Human Attribution in CRM Records

Permanently label each element of a CRM record to indicate whether it was AI-generated (by ADVANCE AI), MSL-edited, or MSL-authored — with this attribution visible in the record and preserved in the audit trail.

**Problem solved:** MSLs need to be able to demonstrate, in a compliance audit, which parts of a record they wrote and which parts were system-generated. An unattributed AI-generated record creates regulatory exposure.

**Compliance note:** Attribution must be immutable — it cannot be removed or overwritten after sync.

---

## F5 — Consistent, Transparent Compliance Flagging

Apply a consistent, rules-based compliance review to all AI-generated summaries before they reach the MSL review step — surfacing potential flags (adverse event mentions, off-label discussion, restricted terminology) with a visible explanation of why the flag was triggered.

**Problem solved:** MSLs report that current CRM compliance flagging is inconsistent and opaque — the same language triggers a flag for one MSL but not another. This erodes trust and causes MSLs to self-censor legitimate clinical content.

**Requirement:** Flagging logic must be auditable and explainable. "Black box" flagging is not acceptable to compliance-aware users.

---

## F6 — Recording Consent & Data Retention Management

Provide a configurable consent workflow for HCP recording — including in-call consent capture, storage of consent record, and the ability for HCPs (or pharma companies) to request deletion of underlying recordings.

**Problem solved:** MSLs are not recording remote meetings because they cannot answer basic consent and retention questions when HCPs ask. Without a clear, company-sanctioned consent framework, MSLs default to not recording — which prevents ADVANCE AI analysis entirely.

**Requirement:** Consent records must be linked to the meeting record and preserved in the audit trail. Retention periods must be configurable per customer (to accommodate GDPR and local regulations).

---

## F7 — Verbatim Insight Preservation

Capture and surface the HCP's near-verbatim language in the AI summary — preserving clinical nuance before it is compressed into CRM field formatting.

**Problem solved:** MSLs currently translate HCP statements into language that fits CRM field constraints and avoids compliance flags. This translation degrades the quality of insights that reach medical strategy. Higher-fidelity capture means the signal reaching leadership reflects what HCPs actually said.

**Implementation note:** Verbatim excerpts should be clearly distinguished from AI-generated summaries in the review interface and CRM record.