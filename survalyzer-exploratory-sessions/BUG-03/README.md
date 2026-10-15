# Bug report

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-03 |
| Title/Summary | [signup] Phone number field is configured as a numerical spinbutton instead of a string input |
| Date Reported | 12/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☒ Medium ☐ Low |
| Priority | ☐ P0 ☐ P1 ☒ P2 ☐ P3  |
| Type | ☒ Functional ☐ Performance ☒ UI/UX ☐ Security ☐ Documentation |
| Status | ☒ New ☐ Assigned ☐ In Progress ☐ Fixed ☐ Verified ☐ Closed |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 Pro |
| Browser/Application: |    Google Chrome 154 |
| Device Type:  |           Laptop |
| Application Version: |    Production Build (12/10/2026) |
| Build Number:  |          Current Live Version (12/10/2026) |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production [https://survalyzer.com](https://survalyzer.com)  |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description

* The Phone Number input component on the sign-up page is defined using numerical attributes (`role="spinbutton"`, `inputmode="decimal"`) rather than string-type telephone semantics.
  
#### Detailed Description

* Inspecting the DOM for the Phone Number field on [https://survalyzer.com/signup](https://survalyzer.com/signup) shows that it uses `<rui-number>` with attributes `role="spinbutton"`, `inputmode="decimal"`, `aria-valuemin="-9999999999999"`, and `aria-valuemax="9999999999999`".

* Inconsistency with Contact Form: The Contact Survalyzer form [https://survalyzer.com/contact](https://survalyzer.com/contact) correctly implements `<input type="tel" name="telephone1">`.

Architectural Mismatch: Phone numbers are formatted identifier strings (which require leading zeros, spaces, and + symbols), not mathematical numbers. Using a numerical spinbutton on the sign-up page causes input stripping and breaks browser autofill compatibility.

---

## 5. Steps to Reproduce

Preconditions:

 * Browser installed with Developer Tools available.
   
Steps:

1. Navigate to [https://survalyzer.com/signup](https://survalyzer.com/signup).
2. Right-click the Phone number input field and select Inspect.
3. Review the HTML tag and attribute declarations in the Elements panel.
4. Compare with the Elements panel for the Phone field on [https://survalyzer.com/contact](https://survalyzer.com/contact).


Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result 

* The sign-up form should align with the Contact form ([survalyzer.com/contact](https://survalyzer.com/contact)) by implementing standard telephone input semantics (`<input type="tel"> or inputmode="tel"`).

---

## 7. Actual Result

* The sign-up input is rendered as a mathematical number component (`role="spinbutton"`, `inputmode="decimal"`), whereas the Contact form correctly uses `type="tel"`.

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☐  Partially blocks user workflow
* ☒  Workaround available (users can type numbers without special characters)
* ☐  No workaround available
* ☐ Affected Features: Phone Input Formatting, Cross-Module Form Architecture.
  
Affected Users: All users entering phone details during registration.

---

## 9. Attachments

### Screenshots/Images
 * [Screenshot 1](./Screenshot_1_BUG-03.png): Elements tab highlighting `role="spinbutton"` and `inputmode="decimal"` on sign-up phone field
 * [Screenshot 2](./Screenshot_2_BUG-03.png): Elements tab on [survalyzer.com/contact](https://survalyzer.com/contact) showing correct `<input type="tel">` implementation
   

### Additional Files

 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A


---

## 10. Additional Information 

Root Cause (if known): 

### Links & Traceability:

* Requirement ID: N/A
* Regression Info: N/A
* Related Issues:  [BUG-01](../BUG-01) (Autofill Country Code Stripping), [BUG-04](../BUG-04) (Unformatted placeholder for Phone field), [BUG-02](../BUG-02) (Label Mismatch)

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

```

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

```
