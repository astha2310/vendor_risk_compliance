# User Acceptance Testing (UAT) Plan — Vendor Risk Compliance

## Purpose

This document records the test scenarios used to verify that the Vendor Risk Compliance application behaves as designed before being considered complete. Each scenario was executed manually against the live application and Dataverse environment.

## Scope

Testing covered: core data entry, the automated approval workflow (including its Microsoft Teams integration), the overdue reminder workflow, the self-service canvas app, built-in reporting charts, and the managed-solution deployment to a second environment.

## Test environment

- Primary environment: development environment, unmanaged solution
- Secondary environment: "VRC Test," managed solution import (see Test 8)
- Tester: Astha Patel (Admin role)

## Test scenarios

### Test 1 — Create a Vendor record

**Steps:** Open the VRC Admin Console app → Vendors → New → fill in Vendor Name and required fields → Save.

**Expected result:** Vendor record saves without error and appears in the Vendors list.

**Result:** Pass. Vendor record created and saved successfully.

### Test 2 — Create an Assessment record

**Steps:** Open Assessments → New → set Assessment Number, Owner, Vendor, Risk Tier, Status → Save.

**Expected result:** Assessment record saves and is linked to the correct Vendor.

**Result:** Pass.

### Test 3 — Risk-tier-triggered approval flow (email)

**Steps:** On an existing Assessment, change Risk Tier to High and Status to Submitted → Save. Check the flow's run history in Power Automate.

**Expected result:** The `VRC_AssessmentApproval` flow triggers a new run, sends an approval request email to the configured approver, and the run shows "Running" while awaiting a decision. Approving the request in email updates the Assessment.

**Result:** Pass — with one important finding. The flow trigger is configured to fire only when the **Risk Tier** field changes value, not when Status changes alone. Changing Status without also changing Risk Tier does **not** start a new run. This was confirmed by testing both cases side by side: a Status-only change produced no new run in the run history; a Risk Tier change (e.g., Medium → High) reliably produced a new run every time. This is documented behavior, not a defect — but it's an important operational note for anyone re-testing an assessment that's already at High.

### Test 4 — Overdue Reminders flow

**Steps:** Confirm the `VRC_OverdueReminders` scheduled flow runs daily and correctly skips Findings with no Remediation Owner set (a safety condition built into the flow).

**Expected result:** Findings past their due date with a named Remediation Owner generate a reminder email; Findings with a blank Remediation Owner are skipped without error.

**Result:** Pass.

### Test 5 — Microsoft Teams notification on high-risk approval

**Steps:** Trigger the approval flow (per Test 3) on an Assessment whose Risk Tier changes to High, using an existing record. Check the "Vendor Risk Compliance" Teams channel.

**Expected result:** A message posts to the Teams "General" channel at the same time the email approval request goes out.

**Result:** Pass. Message posted successfully: "A high-risk vendor assessment has been submitted and is awaiting approval. Please check your email or the VRC Admin Console to review it." Confirmed the message posted using the environment variable-driven approver configuration (see Test 7).

### Test 6 — Self-service canvas app (Vendor Intake and Assessment)

**Steps:** Open the canvas app → fill in a test vendor's Name, Contact Email, Vendor Type, Criticality, and Data Sensitivity → Submit → View My Submissions.

**Expected result:** A success notification appears, the form clears, and the new vendor appears in the submissions list.

**Result:** Pass. Test vendor "Test Vendor App Check" submitted successfully and confirmed both in the app's own submissions list and directly in the underlying Vendor table (sorted by Created On), proving the canvas app writes to the same live Dataverse table used by the rest of the system rather than a disconnected data source.

### Test 7 — Environment variable used in flow (Approver Email)

**Steps:** Create an "Approver Email" environment variable. Update the `VRC_AssessmentApproval` flow's "Assigned to" field to reference the variable instead of a hard-coded email address. Publish the flow and re-test the approval trigger.

**Expected result:** The flow uses the value stored in the environment variable rather than a fixed value in the flow definition.

**Result:** Pass. Confirmed again during the managed solution import into the VRC Test environment (Test 8), where Power Platform explicitly prompted for a value for this environment variable during import — proving it is a genuine per-environment configuration point rather than logic buried inside the flow.

### Test 8 — Managed solution deployment to a second environment

**Steps:** Export the "Vendor Risk Compliance" solution as Managed (v1.0.0.2) from the development environment. Switch to the "VRC Test" environment. Import the managed solution, re-establishing connections (Outlook, Teams, Dataverse, Approvals) and supplying a value for the Approver Email environment variable.

**Expected result:** Import completes successfully; the solution appears under "Managed" solutions in VRC Test with the correct version number.

**Result:** Pass. "Solution 'Vendor Risk Compliance' imported successfully." Verified under the Managed filter in the target environment, version 1.0.0.2.

### Test 9 — Built-in reporting charts

**Steps:** Open Assessments list → Show Chart. Open Findings list → Show Chart.

**Expected result:** Charts render against live data.

**Result:** Pass. Assessments chart ("Risk Tier by Risk Tier") correctly showed a pie chart of High/Medium/Low counts (8/2/2 at time of test). Findings chart ("Remediation Owner") correctly showed a bar chart of finding counts grouped by owner.

## Summary

All 9 test scenarios passed. One behavioral note was documented (Test 3: the approval flow triggers on Risk Tier changes specifically, not Status changes) rather than being treated as a defect, since it reflects the flow's intended trigger configuration.
