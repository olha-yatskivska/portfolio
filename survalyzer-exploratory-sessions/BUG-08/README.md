# Bug Report 

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-08 |
| Title/Summary |[rvo.survalyzer] Expired Azure SAS tokens cause HTTP 403 Forbidden asset errors for custom fonts |
| Date Reported | 14/10/2026 |
| Reported By | Yatskivska |
| Assigned To | DevOps Team |

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

Navigating to the active tenant survey (`https://rvo.survalyzer.eu/jeoqgyqlwd`) causes custom font assets to fail to load with HTTP `403 Forbidden` errors due to invalid or revoked Azure Blob Storage SAS tokens.

#### Detailed Description

* Static typography files (`ROsanswebtextregular.ttf`, `ROsanswebtextbold.woff`) fetched from Azure Blob Storage (`files.survalyzer.eu`) fail to load with HTTP `403 Forbidden` (`net::ERR_ABORTED 403`).
* Reviewing the network request headers reveals that the embedded Shared Access Signature (SAS) token parameters (`sv=2019-07-07`, `sig=...`) fail authentication on the storage server, breaking custom font rendering and generating browser console error logs.

## 5. Steps to Reproduce

Preconditions:
* Access to `https://rvo.survalyzer.eu/jeoqgyqlwd`.
* Browser installed with Developer Tools available.

Steps:

1. Navigate to [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd).
2. Open Chrome DevTools.
Switch to the **Network** tab, filter by **Font** (or **All**), and reload the page (`Ctrl + R`).
4. Select the failed font requests (`ROsanswebtextbold.woff` / `ROsanswebtextregular.ttf`).
5. Inspect the **Headers** panel to confirm the HTTP status code (`403 Forbidden`).

Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

All custom font assets should load cleanly with HTTP 200 OK via valid, auto-renewed cloud storage SAS tokens.
---

## 7. Actual Result

Static font files return HTTP 403 Forbidden (net::ERR_ABORTED 403), causing the browser to fall back to generic system fonts and logging errors to the console.

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☒  Partially blocks user workflow
* ☒  Workaround available (browser falls back to default system typography and user can complete the survey)
* ☐  No workaround available

Affected Features: ustom Branding & Typography, Static Asset Delivery, Application Logging Health.

Affected Users: All external survey respondents visiting the  [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd) tenant endpoint.

---

## 9. Attachments

### Screenshots/Images

 * [Screenshot 1](./Screenshot_1_BUG-08.png): Network tab showing `403 Forbidden` status on Azure SAS font requests and expired SAS expiry timestamp.

### Additional Files


### Additional Files
 * [Console Logs & Network Traces](./Concole_Network.md)
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A

---

## 10. Additional Information   
Root Cause (if known): Azure Blob Storage Token Expiration: Hardcoded Azure SAS token with expired timestamp (se=2020-12-11).


* Requirement ID: 
* Regression Info: Yes (SAS token expired on 11/12/2020)
* Related Issues: N/A
* Notes: N/A
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


