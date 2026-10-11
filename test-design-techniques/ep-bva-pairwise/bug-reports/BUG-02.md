[Back to Main Page](../../README.md)

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-02 |
| Title/Summary | Success message appears after submitting the form when "+" sign is in the field "Number of People" |
| Date Reported | 17.09.2026 |
| Reported By | QA |
| Assigned To | BA |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | Medium  |
| Priority | ☐ P0 ☐ P1 ☐ P2 ☐ P3 |
| Type |  Functional |
| Status | Assigned |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 Pro |
| Browser/Application: |    Chrome 152.0 |
| Device Type:  |           Laptop |
| Application Version: |    v1.0.1 |
| Build Number:  |          Build 2026.09.15 |
| Test Environment:  |      Dev |
| Network:       |          WiFi |

---

## 4. Description

**Brief Description**    

Success message appears after submitting the form when "+" sign is in the field "Number of People"

**Detailed Description**

* The "Number of People" field accepts non-numeric characters like the + sign without frontend validation or sanitization.
* This is a potential risk for future backend integration, as the server will likely expect a pure integer rather than a string containing special characters. 

---

## 5. Steps to Reproduce

Preconditions:

User is on the "Your Recipes for Today" page.

Steps:

1. Enter "+4" into the "Number of People" field.
2. Click the "Find Recipes" button.


Reproducibility:

* Always (100%)


---

## 6. Expected Result

System displays Error Message 

---

## 7. Actual Result

Success Message appears and value saves with + sign '+4'

---

## 8. Impact Analysis
User Impact:
* Workaround available: delete + sign and re-save



---

## 9. Attachments

### Screenshots/Images
 * [Screenshot](./Screenshot%202026-09-17%20124644.png)
 * [Video Recording](./chrome_5WuB3p2loY.gif)



### Additional Files


---
## 10. Additional Information   

### Links & Traceability:
* [TC-N-NP-11](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/test-matrix.md)
* Related Issues:  [TC-N-NP-13](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/test-matrix.md) (Non-printing char (Ctrl+char))
* Related Question: [Q01](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/test-matrix.md) 


---
## 11. Resolution Tracking

| Field | Details |
| :-- | :-- |
| Fixed By | [Developer Name] |
| Date Fixed | [DD/MM/YYYY] |
| Fix Version | [e.g., v2.5.2] |
| Verified By | [QA Engineer Name] |
| Date Verified | [DD/MM/YYYY] |
| Closed Date | [DD/MM/YYYY] |

---
## Severity & Priority Definitions

### Severity Levels:

* Critical: System crash, data loss, complete feature failure
* High: Major functionality broken, significant impact
* Medium: Non-critical functionality affected, workaround exists
* Low: Minor issues, cosmetic problems, no workaround needed

### Priority Levels:

* P0: Fix immediately before release
* P1: Fix before next release
* P2: Fix in upcoming sprint
* P3: Fix when time permits

