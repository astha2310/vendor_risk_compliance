# Vendor Risk Assessment Questions

15 questions covering all five NIST CSF functions (Identify, Protect, Detect, Respond, Recover) and all four ISO 27001:2022 control themes (Organizational, People, Physical, Technological).

Each answer is Yes / Partial / No.

Weight is 1 (minor) to 5 (critical).

This table maps directly to the Controls table in Dataverse:

- Control ID
- Question
- Framework
- Category
- Weight

When you get to Step 21, this table can be copied into Excel for the web and imported into Dataverse.

| Control ID | Question | Framework | Category | Weight |
|---|---|---|---|---:|
| C01 | Does the vendor maintain an up-to-date inventory of the systems and data that will process our information? | NIST CSF | Identify | 3 |
| C02 | Has the vendor completed a risk assessment covering the services they will provide to us within the last 12 months? | NIST CSF | Identify | 4 |
| C03 | Does the vendor enforce multi-factor authentication for all access to systems that store or process our data? | NIST CSF | Protect | 5 |
| C04 | Does the vendor encrypt our data both at rest and in transit? | NIST CSF | Protect | 5 |
| C05 | Does the vendor apply least-privilege / role-based access control to limit who can reach our data? | NIST CSF | Protect | 4 |
| C06 | Does the vendor maintain continuous monitoring or logging to detect unauthorized access to systems handling our data? | NIST CSF | Detect | 4 |
| C07 | Does the vendor conduct vulnerability scanning and penetration testing at least annually? | NIST CSF | Detect | 4 |
| C08 | Does the vendor have a documented incident response plan and commit to notifying us within a defined timeframe (e.g., 72 hours) of a breach affecting our data? | NIST CSF | Respond | 5 |
| C09 | Has the vendor tested its incident response plan (tabletop exercise or similar) within the last 12 months? | NIST CSF | Respond | 3 |
| C10 | Does the vendor maintain a documented business continuity / disaster recovery plan covering the services provided to us? | NIST CSF | Recover | 3 |
| C11 | Does the vendor perform regular, tested backups of our data with documented restoration procedures? | NIST CSF | Recover | 3 |
| C12 | Does the vendor maintain an information security policy that management reviews and approves at least annually? | ISO 27001 | Organizational | 3 |
| C13 | Does the vendor provide security awareness training to employees at least annually? | ISO 27001 | People | 2 |
| C14 | Does the vendor maintain physical security controls to protect facilities, equipment, and systems that store or process our data? | ISO 27001 | Physical | 3 |
| C15 | Does the vendor maintain appropriate technological security controls for endpoints, networks, and access to systems handling our data? | ISO 27001 | Technological | 5 |

## Scoring

Each assessment response is scored as follows:

- Yes = full weight
- Partial = half of the assigned weight
- No = 0 points

Do not round individual response scores.

For example:

- Weight 5 + Yes = 5 points
- Weight 5 + Partial = 2.5 points
- Weight 5 + No = 0 points
- Weight 4 + Yes = 4 points
- Weight 4 + Partial = 2 points
- Weight 4 + No = 0 points

The maximum possible raw score is 51.

### Total Score

Total Score = ROUND((Raw Score / 51) * 100, 0)

The final normalized score is therefore between 0 and 100.

### Risk Tiers

- Low: score under 30
- Medium: score from 30 to 60
- High: score over 60

## Business Rule

High-risk vendors need a second approval.

Any assessment that scores in the High risk tier must be approved by the Assessor first and then by an Admin before the vendor's status can move to Approved.

A single approval is never sufficient for a High-risk vendor.

## Answer Options

Every assessment question uses the following three answer options:

- Yes
- Partial
- No

## Control Weighting

Weights represent the relative importance of each control:

- 1 = Minor
- 2 = Low
- 3 = Moderate
- 4 = High
- 5 = Critical

The current control weights total 51.

## Framework Coverage

### NIST CSF

The questions cover all five NIST CSF functions used in this project:

- Identify
- Protect
- Detect
- Respond
- Recover

### ISO 27001:2022

The questions cover all four ISO 27001:2022 control themes used in this project:

- Organizational
- People
- Physical
- Technological