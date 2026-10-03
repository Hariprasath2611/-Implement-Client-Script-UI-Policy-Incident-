# ServiceNow Incident Management: Client Script & UI Policy Automation

A structured implementation of ServiceNow Client Scripts and UI Policies designed to streamline incident management workflows, improve form-level data integrity, enforce field-level governance, and automate critical calculations.

---

## 📌 Project Overview

In ServiceNow Incident Management, agents frequently face inconsistencies when mandatory fields are not contextually enforced or when calculations (such as Incident Priority based on Impact and Urgency) require manual intervention. 

This project configures and tests client-side logic to:
- Dynamically control field visibility and mandatory status using **UI Policies**.
- Calculate and adjust priorities in real-time without round-trip server latency using **Client Scripts**.
- Enforce strict validation rules prior to form submission (e.g., verifying resolution fields upon closing or resolving an incident).

---

## 🎯 Objectives

1. **Improve Data Quality**: Prevent invalid submissions and incomplete records by dynamically toggling field requirements based on Incident State.
2. **Automate Priority Calculation**: Dynamically compute and assign Incident Priority based on changes to Impact and Urgency (`onChange` Client Script).
3. **Streamline Agent Workflows**: Reduce cognitive load on support agents by hiding or displaying contextual fields only when needed (e.g., On Hold Reason, Resolution Code, Resolution Notes).
4. **Enforce Governance at Submission**: Validate that essential business fields are completed prior to state progression (`onSubmit` Client Script).

---

## 📂 Project Structure

The project is organized into structured project development phases:

```text
├── 1. Ideation Phase/
│   ├── Brainstorming- Idea Generation- Prioritizaation.pdf
│   ├── Define Problem Statements.pdf
│   └── Empathy Map Canvas.pdf
├── 2. Requirement Analysis/
│   ├── Data Flow Diagrams and User Stories - Shortcut.lnk
│   ├── Solution Requirements - Shortcut.lnk
│   └── Technology Stack - Shortcut.lnk
├── 3. Project Design Phase/
│   ├── Problem - Solution Fit/
│   │   └── Problem - Solution Fit v1.pdf
│   ├── Proposed Solution/
│   │   └── Proposed Solution.pdf
│   └── Solution Architecture/
│       └── Solution Architecture.pdf
├── 4. Project Planning Phase/
│   ├── Planning logic.pdf
│   └── Project Planning.pdf
├── 5. Project Development Phase/
│   ├── Performance Testing/
│   │   ├── Artificial Intelligence.pdf
│   │   ├── GenAI Functional & Performance Testing.pdf
│   │   ├── Machine Learning.pdf
│   │   ├── Power BI.pdf
│   │   ├── Salesforce.pdf
│   │   ├── Tableau .pdf
│   │   └── User Acceptance Testing FSD.pdf
│   └── User Acceptance Testing/
│       └── UAT Report.pdf
└── 6. Project Documentation/
    ├── Final Report.pdf
    └── FSD Documentation Format.pdf
```

---

## ⚙️ Technical Architecture & Implementation

### 1. UI Policies (Form Behavior & Field State)
- **Resolved State Policy**: When `State` is set to **Resolved**, fields `Resolution code` (`close_code`) and `Resolution notes` (`close_notes`) become mandatory and visible.
- **On Hold Policy**: When `State` is set to **On Hold**, the `On Hold Reason` (`hold_reason`) field becomes mandatory and visible.

### 2. Client Scripts (Dynamic Logic & Validation)
- **Priority Calculation (`onChange` on Impact / Urgency)**: 
  - Listens for changes to `impact` and `urgency`.
  - Computes the matrix value and updates the `priority` field dynamically on the client form.
- **Form Submission Guard (`onSubmit`)**:
  - Verifies that all conditional prerequisites are met before committing transactions to the server.
  - Halts submission with descriptive user alert banners if required data is missing.

---

## 🧪 User Acceptance Testing (UAT)

| Test ID | Scenario | Expected Result |
| :--- | :--- | :--- |
| **TC-001** | Impact / Urgency Modification | Incident Priority recalculates and updates instantly on the client side. |
| **TC-002** | State transition to `Resolved` | Resolution code and Resolution notes become mandatory. |
| **TC-003** | Submit incident as `Resolved` without notes | Form submission is blocked with an informative error message. |
| **TC-004** | Submit incident as `Resolved` with valid details | Incident record resolves successfully and saves. |
| **TC-005** | State transition to `On Hold` | `On Hold Reason` field becomes mandatory. |
| **TC-006** | Form Regression Check | Default incident creation and navigation flows function normally without regression. |

---

## 🚀 Key Benefits

- **Efficiency**: Reduces time spent correcting improperly submitted incident tickets.
- **Consistency**: Guarantees adherence to ITIL incident resolution standards.
- **User Experience**: Provides immediate visual cues and real-time feedback to service desk engineers.
