# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-06 |
| Title/Summary | [API/DOC/FUN] `POST/booking` returns non-standard `418 I'm a Teapot` instead of `400 Bad Request`/`406 Not Acceptable` when invalid `Accept` header is provided |
| Date Reported | 24/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☑ Medium  ☐ Low |
| Priority | ☐ P0 ☑ P1 ☑ P2 ☐ P3 | (To be assigned by BA/PO) |
| Type | ☑ Functional ☐ Performance ☐ UI/UX ☐ Security ☑ Documentation |
| Status | ☑ New ☐ Assigned ☐ In Progress ☐ Fixed ☐ Verified ☐ Closed |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 |
| Browser/Application: |    Google Chrome 154/Visual Studio Code |
| Device Type:  |           Desktop |
| Application Version: |    v1.0.0 |
| Build Number:  |          apidoc 0.25.0 /Source Code |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☑ Production |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description  

When sending a POST/booking request with an invalid or unsupported Accept header (e.g., Accept: `audio/ogg`), the API returns HTTP status `418 I'm a Teapot` instead of a standard HTTP client error code (`400 Bad Request` or `406 Not Acceptable`).

#### Detailed Description 

N/A

## 5. Steps to Reproduce

Preconditions:

Access to the backend repository source code/API documentation handler.

Steps:

1. Perform a static review of the `POST/booking` controller route handling the `Accept` header.
2. Observe the returned HTTP status code configuration when an unsupported format (e.g., Accept: `audio/ogg`) is passed.

   
Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

The API should return HTTP status `406 Not Acceptable` (or `400 Bad Request`) along with a structured error payload detailing that the requested media type is not supported.

---

## 7. Actual Result

The application lacks input validation and throws an unhandled error, returning an HTTP `500 Internal Server Error` response.

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available
* ☐ Affected Features: API Header Validation, Error Handling

Affected Users: External API integrators and automated test suites expecting RFC-compliant HTTP error status codes.
### Screenshots/Images
N/A


### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A

---

## 10. Additional Information   
Root Cause (if known): Hardcoded/Easter egg response logic in the controller content negotiation handler.

### Links & Traceability:

* Requirement ID: N/A
* Standard Ref: RFC 9110 Section 12.5.1 (406 Not Acceptable)
* Regression Info: No
* Related Issues: [REQ-BUG-03](REQ-BUG-03), [REQ-BUG-05](REQ-BUG-05)
* Notes: Standardizing HTTP status codes ensures that 4xx errors denote client issues and 5xx errors represent genuine unhandled server failures.
  
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
