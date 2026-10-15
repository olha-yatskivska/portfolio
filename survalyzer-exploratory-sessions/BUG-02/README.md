# Bug Report 
## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-02 |
| Title/Summary | [signup] Phone field `<label for>` attribute fails to match input id, triggering DevTools accessibility error  |
| Date Reported | 12/10/2026 |
| Reported By | Yatskivska |
| Assigned To | Frontend Development Team |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☒ Medium ☐ Low |
| Priority | ☐ P0 ☐ P1 ☒ P2 ☐ P3 |
| Type | ☐ Functional ☐ Performance ☒ UI/UX ☐ Security ☐ Documentation ☒ Accessibility  |
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
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production ([survalyzer.com](https://survalyzer.com)) |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description

The `<label>` element for the phone number field contains a for attribute that does not correspond to any valid input id in the DOM. This triggers an accessibility error in DevTools and breaks browser autofill and screen reader support.

#### Detailed Description

* Inspecting the HTML markup on [https://survalyzer.com/signup](https://survalyzer.com/signup) reveals that `<label id="label-phone" for="b4dd48ff-cc74-1ace-7c0b-241257bb603a4">` does not match any element id on the page. 

* Chrome DevTools raises the issue: `"Incorrect use of <label for=FORM_ELEMENT>"`. This prevents assistive technologies (screen readers) from associating the label with the input and impairs browser autofill mechanisms.

---

## 5. Steps to Reproduce

Preconditions:

Browser installed with Developer Tools available.

Steps:

1. Navigate to [https://survalyzer.com/signup](https://survalyzer.com/signup).
2. Open Chrome DevTools.
3. Navigate to the Issues tab or inspect the Phone Number element.
4. Observe the issue entry: `"Incorrect use of <label for=FORM_ELEMENT>"`.

Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

The `<label>'s` `for` attribute must match the exact id attribute of the corresponding `<input>` element to ensure full WCAG 2.1 SC 1.3.1 accessibility compliance and proper autofill behavior.

---

## 7. Actual Result

The `for` attribute references an unmapped string (`"b4dd48ff-cc74-1ace-7c0b-241257bb603a4"`), generating an active DevTools accessibility violation

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☒  Partially blocks user workflow
* ☒  Workaround available (sighted users can manually click into the input box)
* ☐  No workaround available

Affected Features: Accessibility (Screen Readers), Browser Autofill.

Affected Users: Visually impaired users using screen readers, and users relying on browser password/form autofill.

---

## 9. Attachments

### Screenshots/Images

 * [Screenshot 1](./Screenshot_1_BUG-02.png): DevTools Issues panel highlighting `Incorrect use of <label for=FORM_ELEMENT>`


### Additional Files
 * Console Logs [`Incorrect use of <label for=FORM_ELEMENT>`](./Consol_Log_BUG-02.md)
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A


---

## 10. Additional Information   
Root Cause (if known): Dynamic ID mismatch during Angular custom component rendering. The outer `<label>` receives a generated ID (`"b4dd48ff-cc74-1ace-7c0b-241257bb603a4`) that is not passed down or mapped to the inner `<input>` element's `id` attribute.


### Links & Traceability:

* Requirement ID: WCAG 2.1 SC 1.3.1 (Info and Relationships)
* Regression Info: No
* Related Issues: [BUG-01](../BUG-01) (Autofill Country Code Stripping), [BUG-03](../BUG-03) (Numerical Spinbutton Component), [BUG-04](../BUG-04) (Unformatted placeholder for Phone field), [BUG-08](../BUG-08) (Survey Question Label Mismatch)
* Notes: This broken label association directly impairs Chrome's Autofill engine from identifying the input field, contributing to [BUG-01](../BUG-01).


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


