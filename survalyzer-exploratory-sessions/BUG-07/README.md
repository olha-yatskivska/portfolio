# Bug Report 

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-07 |
| Title/Summary |[rvo.survalyzer] Survey question <label for> attribute fails to match input id, triggering DevTools accessibility error |
| Date Reported | 14/10/2026 |
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
| Application Version: |    Production Build |
| Build Number:  |          current Live Version |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production ([rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd)) |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description

The `<label>` element for the "Size of your startup/scale-up in FTE" question contains a for attribute referencing a UUID that does not match any input field id in the DOM. This triggers a Chrome DevTools accessibility error (`"Incorrect use of <label for=FORM_ELEMENT>"`) and breaks screen reader element association.

#### Detailed Description

* Inspecting the HTML markup on [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd) reveals that `<label class="rt-sr-only" id="label-q16" for="f392c467-7d06-33f6-2c06-e545a545e87c">` targets an unmapped UUID. 
* Chrome DevTools raises an active accessibility issue: `"Incorrect use of <label for=FORM_ELEMENT>"`. This violates WCAG 2.1 accessibility guidelines and prevents screen readers from announcing field labels properly.

## 5. Steps to Reproduce

Preconditions:

Browser installed with Developer Tools available.

Steps:

1. Navigate to [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd).
2. Open Chrome DevTools.
3. Navigate to the Issues tab or inspect the "Size of your startup/scale-up in FTE:" element.
4. Observe the issue entry: `"Incorrect use of <label for=FORM_ELEMENT>"`.

Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

The `<label>` element's for attribute must match the exact id attribute of its corresponding `<input>` element to satisfy WCAG 2.1 SC 1.3.1 (Info and Relationships) and enable proper screen reader navigation.

---

## 7. Actual Result

The for attribute references an unmapped UUID (`f392c467-7d06-33f6-2c06-e545a545e87c`), generating an active DevTools accessibility violation.

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

 * [Screenshot 1](./Screenshot_1_BUG-07.png): DevTools Issues panel highlighting `Incorrect use of <label for=FORM_ELEMENT>`


### Additional Files
 * Console Logs [`Incorrect use of <label for=FORM_ELEMENT>`](./Concole_Log_BUG-07.md)
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A


---

## 10. Additional Information   
Root Cause (if known): Dynamic ID mismatch during Angular custom survey component rendering where the parent component generates a UUID for the outer <label> that is not bound to the inner text input field.


### Links & Traceability:

* Requirement ID: WCAG 2.1 SC 1.3.1 (Info and Relationships)
* Regression Info: No
* Related Issues: [BUG-02](../BUG-02) (Phone Field Label Mismatch on Sign-Up Form)
* Notes: Proves a systemic component architecture defect across Survalyzer's Angular form builder, where `<label for>` attributes fail to map to child input IDs in both registration and survey modules.

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


