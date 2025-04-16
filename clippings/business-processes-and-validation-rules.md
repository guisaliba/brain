---
title: "Business Processes and Validation Rules"
source: "https://chat.deepseek.com/a/chat/s/53c077f9-5afe-4c04-b361-cf9d6c4da258"
author:
published:
created: 2025-04-15
description:
tags:
  - "clippings"
---
If Ouvidoria child records cannot use the status despite it being in their BP, the blockage is likely due to:

1. **Existing Validation Rules**: A rule blocking `Validation Grant` for child cases.
2. **Automation (Flows/Processes)**: Removing `Validation Grant` from picklist options for child cases.
3. **Page Layouts**: Hiding the `Status` field or `Validation Grant` value for child cases.

---

### **Solution: Enable Validation Grant for Child Cases**

#### **Step 1: Confirm the Status is in Ouvidoria BP**

- Go to **Setup > Object Manager > Case > Business Processes**.
- Verify `Validation Grant` is added to the Ouvidoria BP.

#### **Step 2: Check for Existing Restrictions**

- **Validation Rules**: Search for rules targeting `Status` or `ParentId` for Ouvidoria records.
	- Example of a problematic rule:
``` java
AND(
  ISPICKVAL(Status, "Validation Grant"),
  NOT(ISBLANK(ParentId))
)
```
*Modify/delete this rule if it exists.*

- **Flows/Processes**: Check for automation that filters/removes `Validation Grant` for child cases.
- **Page Layouts**: Ensure the `Status` field (with `Validation Grant` visible) is assigned to the Ouvidoria layout.

#### **Step 3: Create a Validation Rule (If Needed)**

If you need to **conditionally allow** `Validation Grant` for child cases (e.g., only if the parent meets criteria), use a rule like:

``` java
AND(
  ISPICKVAL(Status, "Validation Grant"),
  NOT(ISBLANK(ParentId)), // Child case
  $RecordType.DeveloperName \= "Ouvidoria",
  // Optional: Add parent-based conditions (e.g., parent must be in "Approved" status)
  NOT(ISPICKVAL(Parent.Status, "Approved"))
)
```

This rule would block `Validation Grant` **unless** the parent case is "Approved". Adjust the logic based on your needs.

#### **Step 4: Test in Sandbox**

- Create a parent Ouvidoria case.
- Create a child case under it (same Ouvidoria record type).
- Verify if `Validation Grant` is available and selectable.

---

### **Common Fixes Based on Scenarios**

| **Scenario** | **Fix** |
| --- | --- |
| Existing validation rule blocks it | Delete or modify the rule to exclude child Ouvidoria cases. |
| Flow/Process removes the status | Edit the automation to retain `Validation Grant` for Ouvidoria child cases. |
| Page Layout hides the status | Add `Validation Grant` to the page layout’s Status picklist for Ouvidoria record type. |

---

### **Why Your Approach Will Work**

- **Business Process**: Since `Validation Grant` is already in the Ouvidoria BP, child cases inherit it by default (same record type = same BP).
- **No Extra Metadata**: No need for new record types or BPs.
- **Declarative**: Uses validation rules to enforce parent/child logic (if needed).

---

### **Final Checks**

1. **User Training**: Inform users that `Validation Grant` is now available for child cases.
2. **Audit Existing Automation**: Ensure no conflicting rules/processes are undoing your changes.
3. **Backup**: Test in a sandbox before deploying to production.

By addressing the root cause (existing restrictions), you’ll allow child Ouvidoria cases to use `Validation Grant` seamlessly.