# Vendor Risk Compliance — Requirements

## Problem

Vendor security and risk review currently runs through Excel trackers and email. Procurement or the business owner emails a spreadsheet questionnaire to a new vendor, waits for it to come back, then forwards it (along with a SOC 2 report, pen test summary, or policy documents) to whoever happens to be free to review it. There is no single source of truth for a vendor's status, no consistent way to score risk, and no reliable way to see which findings from past assessments are still open or overdue. Every step depends on someone remembering to follow up.

## Users

- **Requester** — business unit staff who need to bring on a new vendor. They submit the vendor for review and need visibility into where it stands.
- **Assessor** — security/compliance staff who run the actual risk assessment: complete the questionnaire, score it, and raise findings.
- **Admin** — the compliance lead. Has full visibility, gives the second approval on high-risk vendors, and owns overall reporting and remediation tracking.

## Process

1. A Requester submits a new vendor (name, type, data sensitivity, criticality, business owner).
2. An Assessor is assigned and completes a standardized questionnaire against the vendor, referencing uploaded evidence (contract, SOC 2 report, pen test summary, policy).
3. The system calculates a weighted risk score and assigns a risk tier (Low / Medium / High).
4. The assessment goes through an approval workflow. High-risk vendors require a second, senior approval.
5. Approved vendors move to active status with a scheduled next review date; rejected ones are sent back or closed out.
6. Any issues found during assessment become tracked findings with an owner and due date, followed up until remediated.

## Pain points

1. Vendor questionnaires and supporting evidence are scattered across email threads and shared drives, with no single system of record.
2. Risk scoring is subjective — two assessors can look at the same answers and land on different risk levels, because there's no standard weighting.
3. There's no visibility into open findings or their due dates, so remediation items quietly go overdue with nobody chasing them.
4. Approvals for high-risk vendors happen informally over email, with no enforced second sign-off and no audit trail of who approved what and when.
5. Leadership has no dashboard or report to see vendor risk posture at a glance — every status update is a manual ask.

## User stories

1. As a **Requester**, I want to submit a new vendor with basic details so that the review process can start without an email chain.
2. As a **Requester**, I want to see the current status of vendors I've submitted so that I don't have to ask someone for an update.
3. As an **Assessor**, I want to work through a standardized set of weighted questions per vendor so that scoring is consistent across assessors.
4. As an **Assessor**, I want the risk score and tier calculated automatically from my answers so that I don't have to compute it by hand and risk getting it wrong.
5. As an **Assessor**, I want to submit a completed assessment for approval so that it moves into a formal decision workflow instead of an email.
6. As an **Admin**, I want high-risk assessments automatically routed to me for a second approval so that extra scrutiny is enforced, not optional.
7. As an **Admin**, I want to track every open finding with an owner and due date so that remediation work doesn't get dropped.
8. As an **Admin** or **Assessor**, I want overdue findings to trigger an automatic reminder (and escalate if they go far enough overdue) so that nothing slips through unnoticed.

## Business rule

**High-risk vendors need a second approval.** Any assessment that scores in the High risk tier must be approved by the Assessor first and then by an Admin before the vendor's status can move to Approved. A single approval is never sufficient for a High-risk vendor.

## Risk tiers

- **Low** — score under 30
- **Medium** — score 30 to 60
- **High** — score over 60

## Naming standard

- Dataverse solution / publisher prefix: `vrc`
- Power Automate flow prefix: `VRC_` (e.g., `VRC_AssessmentApproval`, `VRC_OverdueReminders`, `VRC_CreateEvidenceFolder`)