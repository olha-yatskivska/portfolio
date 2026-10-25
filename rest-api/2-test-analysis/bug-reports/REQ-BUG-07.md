# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-07 |
| Title/Summary | [API/SEC] [POST/auth] returns `200 OK` with `"Bad credentials"` payload on failed authentication instead of `401 Unauthorized` |
| Date Reported | 24/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☑ High ☐ Medium  ☐ Low |
| Priority | ☐ P0 ☑ P1 ☐ P2 ☐ P3  |
| Type | ☑ Functional ☐ Performance ☐ UI/UX ☑ Security ☑ Documentation |
| Status | ☑ New ☐ Assigned ☐ In Progress ☐ Fixed ☐ Verified ☐ Closed |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 |
| Browser/Application: |    Google Chrome 154/Visual Studio Code |
| Device Type:  |           Desktop |
| Application Version: |    v1.0.0 |
| Build Number:  |          apidoc 0.25.0/Source Code |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☑ Production |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description  

When submitting invalid login credentials to the `POST/auth` endpoint, the server responds with an HTTP status code `200 OK` containing "reason": `"Bad credentials"` in the response body instead of returning an HTTP `401 Unauthorized` error status code.

#### Detailed Description 

Static review of the authentication endpoint implementation and documentation reveals an HTTP status code handling inconsistency. When a client submits invalid credentials (such as an incorrect `username` or `password`), the authentication service returns a success status code (`200 OK`) while indicating an authentication failure solely within the response body string (`{"reason": "Bad credentials"}`).

Returning HTTP `200 OK` for failed login attempts violates standard REST API design practices (RFC 9110). Successful HTTP status codes confuse client application error handling logic, break API gateway security policies, and create inconsistencies across the overall error handling policy.

## 5. Steps to Reproduce

Preconditions:

Access to the backend repository source code

Steps:

1. Perform a static review of the `POST/auth` controller implementation handling credential validation.
2. Observe the HTTP status code returned in the error response path when invalid credentials are provided.
   
Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

Upon failed authentication, the API should return an HTTP `401 Unauthorized` status code with an appropriate error payload (e.g., `{"reason": "Bad credentials"}`).

---

## 7. Actual Result

The API returns an HTTP `200 OK` status code with a body payload indicating "reason": `"Bad credentials"`.

## 8. Impact Analysis
 
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available
* ☐ Affected Features: Authentication & Authorization Flow, API Gateway Security Filters, Client Error Handling

Affected Users: Client-side developers and API integrators who rely on standard HTTP response status codes to detect authentication failures.
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
* Standard Ref: RFC 9110 Section 15.5.2 (401 Unauthorized)
* Regression Info: No
* Related Issues: [REQ-BUG-03](REQ-BUG-03), [REQ-BUG-05](REQ-BUG-05), [REQ-BUG-06](REQ-BUG-06)
* Notes: HTTP 401 status codes ensures consistent security logging and interceptor behavior in frontend/mobile applications.
  
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
