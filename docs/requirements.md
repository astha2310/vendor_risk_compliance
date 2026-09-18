# Vendor Risk Compliance — Requirements

## 1. Problem

The procurement team currently manages vendor security reviews using Excel spreadsheets, email, and manually stored documents. This makes it difficult to track vendor assessments, security evidence, approvals, and remediation activities in one place. The proposed Vendor Risk Compliance solution will use Microsoft Power Platform, Dataverse, SharePoint, Power Automate, Teams, and Power BI to centralize the vendor risk management process.

## 2. Users

- Requester — submits new vendors and provides required information.
- Assessor — reviews vendor assessments, evidence, and findings.
- Admin — manages approvals, security roles, and compliance oversight.

## 3. Process

1. Requester submits a new vendor.
2. The vendor is assigned an assessment.
3. The Assessor reviews the assessment questions and vendor evidence.
4. Assessment responses are scored based on control weights.
5. The system calculates the vendor risk score and risk tier.
6. The assessment is submitted for approval.
7. High-risk vendors require a second approval from the Admin.
8. Findings are created for security or compliance issues.
9. Overdue findings generate automated reminders.
10. Approved vendors are monitored and reviewed based on their next review date.

## 4. Current Pain Points

1. Vendor information is spread across Excel files and email.
2. Security evidence is difficult to organize and locate.
3. Assessment scoring is performed manually.
4. Approval status is difficult to track.
5. Remediation findings can become overdue without timely follow-up.

## 5. User Stories

1. As a Requester, I want to submit a vendor so that the security review process can begin.
2. As a Requester, I want to track the status of my vendor so that I know where it is in the process.
3. As an Assessor, I want to view vendor information and evidence so that I can perform a security assessment.
4. As an Assessor, I want to answer assessment questions so that a risk score can be calculated.
5. As an Assessor, I want to create findings so that vendor security issues can be tracked.
6. As an Admin, I want to approve or reject assessments so that vendor risk decisions are documented.
7. As an Admin, I want high-risk vendors to require a second approval so that higher-risk decisions receive additional review.
8. As a compliance user, I want dashboards and reports so that I can monitor vendor risk and overdue findings.

## 6. Risk Scoring

Each assessment question is assigned a weight from 1 to 5. Answers are recorded as Yes, Partial, or No and are used to calculate the assessment score.

Risk tiers:

- Low: score under 30
- Medium: score from 30 to 60
- High: score over 60

High-risk vendors require a second approval from an Admin before the assessment can be approved.

## 7. Key Requirement

The solution must provide a centralized and traceable process for vendor intake, security assessment, evidence management, risk scoring, approvals, findings remediation, and reporting.