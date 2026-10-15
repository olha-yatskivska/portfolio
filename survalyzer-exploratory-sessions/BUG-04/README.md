# Bug report 

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-04 |
| Title/Summary | [signup] Phone field placeholder displays unformatted raw digits instead of a spaced mask guide |
| Date Reported | 12/10/2026 |
| Reported By | Yatskivska |
| Assigned To | Frontend Development Team/BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☐ Medium ☒ Low |
| Priority | ☐ P0 ☐ P1 ☐ P2 ☒ P3  |
| Type | ☐ Functional ☐ Performance ☒ UI/UX ☐ Security ☐ Documentation |
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
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production [https://survalyzer.com](https://survalyzer.com) |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description
* The placeholder for the phone number input on the sign-up page displays an unformatted block of raw numbers (`41443456789`) rather than a clear mask guide.

#### Detailed Description

* On [https://survalyzer.com/signup](https://survalyzer.com/signup), the Phone number input placeholder attribute is set to `placeholder="41443456789"`.

* Inconsistency with Contact Form: On the Contact Survalyzer form [https://survalyzer.com/contact](https://survalyzer.com/contact), the phone field provides a formatted placeholder guide: `placeholder="+44 20 3398 5989"`.

* Usability Impact: UX best practices dictate that placeholder text should guide users with a clean mask structure (e.g., `+44 20 3398 5989"`, making it easier to parse expected input formats.
  
---

## 5. Steps to Reproduce

Preconditions:

 * User navigates to the sign-up page.
   
Steps:

1. Navigate to [https://survalyzer.com/signup](https://survalyzer.com/signup)
2. Scroll to the Phone number input field.
3. Inspect the placeholder text inside the empty input box.
4. Compare with the placeholder text on [https://survalyzer.com/contact](ttps://survalyzer.com/contact) (`+44 20 3398 5989`).
   

Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result 

* In alignment with the Contact form ([https://survalyzer.com/contact](ttps://survalyzer.com/contact)), the sign-up form placeholder should display a formatted pattern with spacing (e.g., `+41 44 345 67 89` or `+44 20 3398 5989`) to guide user entry.

---

## 7. Actual Result

* The sign-up placeholder shows a dense unformatted string: `41443456789`, whereas the Contact form shows `+44 20 3398 5989`.

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☐  Partially blocks user workflow
* ☒  Workaround available (user types number regardless)
* ☐  No workaround available

Affected Features: Registration UI/Form Usability.
Affected Users: All users filling out the trial sign-up form.

---

## 9. Attachments

### Screenshots/Images
 * [Screenshot 1](./Screenshot_1_BUG-04.png): Sign-up form showing unformatted phone placeholder (`41443456789`)
 * [Screenshot 2](./Screenshot_2_BUG-04.png): Contact Survalyzer form showing proper formatted placeholder (`+44 20 3398 5989`)
   


### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A
 

---

## 10. Additional Information 

Root Cause (if known): Hardcoded static string passed into the `data-dx_placeholder` configuration on the sign-up component.

### Links & Traceability:

* Requirement ID: N/A
* Regression Info: N/A
* Related Issues:  [BUG-01](../BUG-01) (Autofill Country Code Stripping), [BUG-03](../BUG-03) (Numerical Spinbutton Component), [BUG-02](../BUG-02) (Label Mismatch)

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
