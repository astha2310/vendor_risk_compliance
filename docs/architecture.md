# Architecture — Vendor Risk Compliance

This diagram shows how the pieces of the system fit together. It renders automatically as a picture when viewed on GitHub.

```mermaid
flowchart TB
    subgraph Users["People"]
        Requester["Requester"]
        Assessor["Assessor"]
        Admin["Admin"]
    end

    subgraph Apps["Power Apps"]
        Canvas["Canvas App:\nVendor Intake and Assessment"]
        ModelDriven["Model-Driven App:\nVRC Admin Console"]
    end

    subgraph Data["Microsoft Dataverse"]
        Vendor[("Vendor")]
        Control[("Control\n(15 questions)")]
        Assessment[("Assessment")]
        Response[("Assessment Response")]
        Finding[("Finding")]
        AppUser[("App User")]
    end

    subgraph Automation["Power Automate"]
        ApprovalFlow["VRC_AssessmentApproval\n(triggers on Risk Tier change)"]
        ReminderFlow["VRC_OverdueReminders\n(daily schedule)"]
    end

    subgraph Notify["Notifications"]
        Email["Outlook Email\n(Approval requests + reminders)"]
        Teams["Microsoft Teams\n(Vendor Risk Compliance channel)"]
    end

    subgraph Evidence["SharePoint"]
        Library["Vendor Evidence\ndocument library"]
    end

    subgraph Reporting["Reporting"]
        Charts["Power Apps native charts\n(Risk Tier, Findings by Owner)"]
    end

    Requester -->|submits vendor| Canvas
    Canvas -->|writes| Vendor

    Assessor -->|runs assessments,\nlogs findings| ModelDriven
    Admin -->|approves, administers| ModelDriven

    ModelDriven --> Vendor
    ModelDriven --> Control
    ModelDriven --> Assessment
    ModelDriven --> Response
    ModelDriven --> Finding
    ModelDriven --> AppUser

    Assessment -->|Risk Tier changes| ApprovalFlow
    ApprovalFlow --> Email
    ApprovalFlow --> Teams
    ApprovalFlow -->|updates Status| Assessment

    Finding -->|checked daily| ReminderFlow
    ReminderFlow --> Email

    ModelDriven -.->|linked evidence docs| Library

    Assessment --> Charts
    Finding --> Charts
    ModelDriven --> Charts
```

## Environment topology (ALM)

```mermaid
flowchart LR
    Dev["Development Environment\n(unmanaged solution)"]
    Export["Export as\nManaged Solution\n(v1.0.0.2)"]
    Test["VRC Test Environment\n(managed solution imported)"]

    Dev -->|Export| Export
    Export -->|Import| Test
```

Development happens in the primary environment as an unmanaged (freely editable) solution. When a version is ready to move forward, it's exported as a managed solution and imported into the separate "VRC Test" environment, where environment-specific settings (like the Approver Email environment variable and connection references) are reconfigured rather than hard-coded into the flow logic.
