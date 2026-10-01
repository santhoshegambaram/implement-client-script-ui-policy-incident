# Implement Client Script & UI Policy (Incident)

Comprehensive ServiceNow implementation project demonstrating client-side scripting and UI policies on the **Incident (`incident`)** table. This project enforces data integrity, automates dynamic form behaviors, and validates record changes across form views and list views.

---

## Project Overview

- **Platform:** ServiceNow
- **Target Table:** Incident (`incident`)
- **Key Capabilities:** UI Policies, UI Policy Actions, Client Scripts (`onChange`, `onSubmit`, `onCellEdit`), and Form Behavior Validation.
- **Repository:** [santhoshegambaram/implement-client-script-ui-policy-incident](https://github.com/santhoshegambaram/implement-client-script-ui-policy-incident)

---

## Implementation Milestones

### Milestone 1: Create UI Policy on Incident
Configured a client-side UI Policy on the Incident table to dynamically control field behavior based on specific condition triggers without writing custom code.

- **Objective:** Dynamically evaluate conditions on the incident record to alter field states (visible, mandatory, read-only).
- **Screenshots:**
  - *UI Policy Definition:*  
    ![UI Policy Setup](./Screenshots/Screenshot%202026-09-29%20184027.png)
  - *Condition & Scope Configuration:*  
    ![UI Policy Condition](./Screenshots/Screenshot%202026-09-29%20184335.png)

---

### Milestone 2: Create UI Policy Action – Urgency
Defined related UI Policy Actions tied to the base policy to enforce field-level requirements when conditions evaluate to true.

- **Objective:** Configure field parameters for `Urgency` (and associated impact/priority fields) to dynamically become mandatory, visible, or read-only.
- **Screenshots:**
  - *UI Policy Action Configuration:*  
    ![UI Policy Action](./Screenshots/Screenshot%202026-09-29%20184711.png)
  - *Action Behavior Verification:*  
    ![UI Policy Action Verification](./Screenshots/Screenshot%202026-09-29%20185509.png)

---

### Milestone 3: Create onChange Client Script
Implemented an `onChange` client script running in the browser when a designated field value changes.

- **Objective:** Monitor field modifications in real-time, executing client-side logic (e.g., dynamically updating related fields, clearing stale data, or displaying contextual alerts using `g_form`).
- **Screenshots:**
  - *onChange Script Creation:*  
    ![onChange Setup](./Screenshots/Screenshot%202026-09-29%20190038.png)
  - *Script Logic Implementation:*  
    ![onChange Logic](./Screenshots/Screenshot%202026-09-29%20190400.png)

---

### Milestone 4: Create onSubmit Client Script (Save Validation)
Developed an `onSubmit` client script to validate form integrity before an Incident record is saved or updated.

- **Objective:** Intercept the form submission event, verify business-critical input criteria, and return `false` with a descriptive error message (`g_form.addErrorMessage`) if data validation fails.
- **Screenshots:**
  - *onSubmit Script Setup & Validation Logic:*  
    ![onSubmit Script](./Screenshots/Screenshot%202026-09-29%20190853.png)

---

### Milestone 5: Create onCellEdit Client Script
Configured an `onCellEdit` client script applied to list views of the Incident table.

- **Objective:** Control and validate inline cell editing directly from the incident list view to ensure data policies cannot be bypassed outside of standard form views.
- **Screenshots:**
  - *onCellEdit Script Configuration:*  
    ![onCellEdit Configuration](./Screenshots/Screenshot%202026-09-29%20191957.png)

---

### Milestone 6: Testing and Verification
End-to-end testing across both form view and list view to ensure policies and scripts execute properly without performance bottlenecks or script exceptions.

- **Test Scenarios Executed:**
  1. Triggered UI Policy by matching condition criteria; confirmed target fields adjust visibility and mandatory states.
  2. Modified tracked field to trigger `onChange` script; confirmed client response and field recalculation.
  3. Submitted invalid data; confirmed `onSubmit` script halted record submission and flagged appropriate fields.
  4. Performed inline edits on the incident list; confirmed `onCellEdit` enforced validation before saving.
- **Screenshots:**
  - *Incident Form Dynamic Behavior Test:*  
    ![Form Testing](./Screenshots/Screenshot%202026-09-29%20193503.png)
  - *Validation Output & Final Result:*  
    ![Final Test Results](./Screenshots/Screenshot%202026-09-29%20194139.png)

---

## Repository Structure

```text
.
├── README.md
└── Screenshots/
    ├── Screenshot 2026-09-29 184027.png
    ├── Screenshot 2026-09-29 184335.png
    ├── Screenshot 2026-09-29 184711.png
    ├── Screenshot 2026-09-29 185509.png
    ├── Screenshot 2026-09-29 190038.png
    ├── Screenshot 2026-09-29 190400.png
    ├── Screenshot 2026-09-29 190853.png
    ├── Screenshot 2026-09-29 191957.png
    ├── Screenshot 2026-09-29 193503.png
    └── Screenshot 2026-09-29 194139.png

Key Learnings & ServiceNow Best Practices
UI Policy vs. Client Script Priority: Used UI Policies whenever possible for UI state manipulation (mandatory, read-only, visibility) since they execute faster and do not require code maintenance.

Client Script Optimization: Restricted scripts to run only when values change (isLoading checks) and minimized DOM-heavy operations by adhering strictly to the g_form API.

List View Integrity: Paired form-level validation with onCellEdit scripts to prevent data contamination from users editing records directly within list controls.