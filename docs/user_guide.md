# User Guide — Vendor Risk Compliance

This guide explains how to use the Vendor Risk Compliance (VRC) system day to day, organized by role. If you're not sure which role you have, check with your VRC Admin.

## Roles at a glance

| Role | What you can do |
|---|---|
| **Requester** | Submit a new vendor for review using the self-service app |
| **Assessor** | Run assessments, log findings, track remediation, give first-level approval on high-risk vendors |
| **Admin** | Everything an Assessor can do, plus final approval on high-risk vendors, security and solution management |

---

## For Requesters: submitting a new vendor

Use the **"Vendor Intake and Assessment"** app for this — you don't need access to the full admin console.

1. Open the **Vendor Intake and Assessment** app.
2. Fill in the vendor's details: Vendor Name, Contact Email, Vendor Type, Criticality, and Data Sensitivity.
3. Click **Submit Vendor Request**.
4. You'll see a confirmation message once it's saved.
5. Click **View My Submissions** at any time to see the vendors you've submitted and their status.

An Assessor or Admin will pick up your submission from there and begin the formal assessment process.

---

## For Assessors: running an assessment

1. Open the **VRC Admin Console** app.
2. Go to **Assessments** → **New**.
3. Fill in:
   - **Assessment Number** — a unique identifier for this assessment
   - **Owner** — usually yourself
   - **Vendor** — the vendor being assessed
   - **Status** — start with "Draft" or "In Progress"
4. Work through the 15 control questions (found under **Controls**, each mapped to a Category and Framework — NIST CSF or ISO 27001:2022). Record each answer as an **Assessment Response** linked to this Assessment.
5. Once all 15 questions are answered, the weighted score determines the **Risk Tier** (Low / Medium / High) automatically.
6. Set **Status** to **Submitted** once the assessment is ready for review.

**Important:** the approval process is triggered by a change to the **Risk Tier** field specifically — not by changing Status alone. If you're re-submitting an assessment that's already at High risk, make sure the Risk Tier value actually changes (or is re-selected) to trigger a fresh approval cycle.

### Logging a finding

If an assessment surfaces an issue that needs to be tracked and fixed:

1. Go to **Findings** → **New**.
2. Give it a clear **Title** describing the issue (for example, "MFA not enforced for admin accounts").
3. Link it to the relevant Assessment and Vendor.
4. Set a **Remediation Owner** — the person responsible for fixing it. This is required for the automated reminder system to notify anyone about this finding, so don't leave it blank.
5. Set a **due date**.

A scheduled flow checks daily for overdue findings and emails a reminder to the Remediation Owner automatically.

---

## For Admins: approving high-risk vendors and managing the system

### The approval process

When an Assessor sets a vendor's Risk Tier to **High**, two things happen automatically:

1. An approval request email goes to the person configured as the **Approver** (this is stored as an environment variable, so it can be different per environment — ask your Admin who the current approver is if you're unsure).
2. A notification posts to the **Vendor Risk Compliance** Microsoft Teams channel so the team has visibility, even before the email is acted on.

High-risk assessments require **two levels of sign-off**: first from an Assessor, then from an Admin, before the assessment is considered finalized. Approve or reject directly from the email you receive, or from the **Approvals** area in Power Automate.

### Managing security roles

Security roles (VRC Admin, VRC Assessor, VRC Requester) are managed in the Power Platform admin center under this environment's settings, or from within the model-driven app's advanced settings. Assign the role that matches what each person should be able to do — see the "Roles at a glance" table above.

### Viewing reports

From the **Assessments** or **Findings** list views in the VRC Admin Console, click **Show Chart** to see a live visual breakdown — for example, the distribution of vendors by Risk Tier, or the count of open findings by Remediation Owner.

### Managing the solution (advanced / technical admins only)

The whole system is packaged as a Power Platform solution called "Vendor Risk Compliance." Changes should be made in the development environment, then exported as a Managed solution and imported into the test/production environment when ready — see the project's `README.md` for details on this process.
