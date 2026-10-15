# Bug report 

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-01 |
| Title/Summary | [signup] Phone Field UI Inconsistency and Country Code Loss During Browser Autofill |
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
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production [https://survalyzer.com](https://survalyzer.com) |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description

* The phone number input field on the sign-up page (`/signup`) is implemented inconsistently compared to other forms on the website (e.g., `/contact`).
* As a result, Google Chrome Autofill populates the input field without the saved international country code prefix (e.g., populating `123456789` instead of `+48123456789`).

#### Detailed Description

* **UI/UX Inconsistency:** On [https://survalyzer.com/contact](https://survalyzer.com/contact), the phone input uses a standard international telephone input structure with correct attributes (`type="tel"` / `autocomplete="tel"`), whereas [https://survalyzer.com/signup](https://survalyzer.com/signup) uses a single generic text input without standardized telephone autocomplete attributes.

* **Autofill Behavior:** When a user completes registration using Chrome Autofill, the saved telephone credentials (e.g., `+48123456789`) lose the international prefix and are filled as `123456789`.
  
* **System Impact:** Omitting country codes during registration leads to incomplete, unparseable, or invalid phone records in backend data stores, causing notification failures and registration friction for global users. (can't verify it on Production)
  

---

## 5. Steps to Reproduce

Preconditions:

 * Google Chrome is configured with a saved profile containing an autofill phone number with international code.

Steps:

1. Navigate to [https://survalyzer.com](https://survalyzer.com)
2. Click "Test for free" in the header navigation (or click "Get Started For Free" in the Solutions made for you block under Explore EX/CX solutions).
3. Scroll to the Phone Number input field on the sign-up form.
4. Trigger Google Chrome Autofill on the form or field.
5. Observe that the phone number populates without an international country code prefix.

Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result 

* To ensure consistent application UI/UX and proper browser integration, the sign-up form's phone field should align with the implementation pattern used on `survalyzer.com/contact`.
* When Chrome Autofill is triggered, the full international phone number (including the leading country code, e.g., `+48123456789`) should be correctly captured and preserved in the input field.

---

## 7. Actual Result

* The sign-up form phone input field fails to parse or retain the international country code during autofill, stripping the prefix and populating only the local phone number (e.g., `123456789`).

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☒  Partially blocks user workflow
* ☒  Workaround available (manual entry of country code)
* ☐  No workaround available

Affected Features: User Registration / Sign-Up Form, Phone Number Validation, Google Chrome Autofill Integration.
Affected Users: All international users registering via browser autofill.

---

## 9. Attachments

### Screenshots/Images
 * [Screenshot 1](./Screenshot_1_BUG-01.png): Sign-up page phone field missing dedicated country code picker
 * [Screenshot 2](./Screenshot_2_BUG-01.png): Contact form (`survalyzer.com/contact`) demonstrating the correct reference implementation
 * [Screenshot 3](./Screenshot_3_BUG-01.png): Chrome Autofill Settings demonstrating stored phone number with country code (`+48123456789`)
 * [Screen Recording / Animated GIF](Screen_Recording_BUG-01): Demonstrating Chrome Autofill dropping the `+48` country code on `/signup`


### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A
 
---

## 10. Additional Information   
Root Cause (if known): The `/signup` input element lacks proper HTML5 attribute markup (`type="tel"` and `autocomplete="tel"`), causing Chrome's autofill engine to default to standard string matching rather than telephone specification parsing.

### Links & Traceability:
* Target Alignment: `https://survalyzer.com/contact` (UI Reference)
* Requirement ID: N/A
* Regression Info: N/A
* Related Issues:  [BUG-01](../BUG-02) (Label Mismatch), [BUG-03](../BUG-03) (Numerical Spinbutton Component), [BUG-04](../BUG-04) (Unformatted placeholder for Phone field)
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

```
