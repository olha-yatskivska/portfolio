# Bug Report 

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-09 |
| Title/Summary |[rvo.survalyzer] Input field placeholder displays untranslated Dutch text when English locale is requested |
| Date Reported | 14/10/2026 |
| Reported By | Yatskivska |
| Assigned To | Frontend/Localization Team |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☐ Medium ☒ Low |
| Priority | ☐ P0 ☐ P1 ☐ P2 ☒ P3 |
| Type | ☐ Functional ☐ Performance ☒ UI/UX ☐ Security ☐ Documentation  |
| Status | ☒ New ☐ Assigned ☐ In Progress ☐ Fixed ☐ Verified ☐ Closed |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 Pro |
| Browser/Application: |    Google Chrome 154 |
| Device Type:  |           Laptop |
| Application Version: |    Production Build |
| Build Number:  |          Current Live Version |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production ([https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd)) |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description

The StartInterview API response incorrectly maps the English language code ("en") to Dutch placeholder text ("Voer hier uw antwoord in.") on survey text inputs.

#### Detailed Description

Inspecting the network traffic during survey initialization on [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd) reveals a localization mapping defect. Under the StartInterview Fetch/XHR response payload, the placeholder configuration array contains an incorrect association where "languageCode": "en" is paired with the Dutch string "text": "Voer hier uw antwoord in." instead of the expected English equivalent. This causes English-speaking respondents to see Dutch prompt text inside active input fields.

## 5. Steps to Reproduce

Preconditions:
* Access to `https://rvo.survalyzer.eu/jeoqgyqlwd`.
* Browser installed with Developer Tools available.

Steps:

1. Navigate to [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd).
2. Open Chrome DevTools and select the Network tab.
3. Filter requests by Fetch/XHR
4. Reload the page (Ctrl + R) and select the StartInterview request row.
5. Click on the Response tab and expand the placeholder JSON array. (`403 Forbidden`).

Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

The StartInterview API response should correctly map language codes to their respective translations, ensuring "languageCode": "en" serves English placeholder text (e.g., "Type your answer here.").
---

## 7. Actual Result

The API response pairs "languageCode": "en" with the Dutch string "Voer hier uw antwoord in."

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☒  Partially blocks user workflow
* ☒  Workaround available (users can still type regardless of placeholder text)
* ☐  No workaround available

Affected Features: Internationalization (i18n) Engine, API Localization Payload.

Affected Users: English-speaking survey respondents accessing the tenant endpoint.

---

## 9. Attachments

### Screenshots/Images

 * [Screenshot 1](./Screenshot_1_BUG-09.png): Network XHR response showing StartInterview payload mapping "languageCode": "en" to Dutch text "Voer hier uw antwoord in."
### Additional Files


### Additional Files
 * Network Traces: [StartInterview cURL](./cURL.md), [StartInterview JSON Response](Response.md)
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A

---

## 10. Additional Information   
Root Cause (if known): Misconfigured database seed or translation dictionary mapping table where Dutch localization strings were incorrectly assigned to the "en" language key.


* Requirement ID: N/A
* Regression Info: N/A
* Related Issues: [BUG-05](../BUG-05) (Missing i18n Translation Key)
* Notes: Demonstrates a backend-level localization mapping error rather than a pure frontend rendering issue.
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


