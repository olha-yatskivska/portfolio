# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-11 |
| Title/Summary | [API/SEC] [DELETE/booking/{id}] returns `403 Forbidden` instead of `401 Unauthorized` when authentication token is missing |
| Date Reported | 24/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☑ Medium  ☐ Low |
| Priority | ☐ P0 ☐ P1 ☑ P2 ☐ P3  |
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

When attempting to delete a booking via `DELETE/booking/{id}` without providing an authentication token (or authorization header/cookie), the server responds with HTTP status `403 Forbidden` instead of `401 Unauthorized`.

#### Detailed Description 

Static review of the controller implementation and security route specifications reveals improper HTTP status code assignment for unauthenticated deletion requests. According to HTTP standards (RFC 9110):
* `401 Unauthorized` must be returned when a request lacks valid authentication credentials (missing identity).
* `403 Forbidden` must be reserved for requests where identity is established/authenticated, but the user lacks sufficient rights to perform the deletion.

Returning `403 Forbidden` when credentials are missing conceals the actual authentication requirement, preventing automated API clients and frontend interceptors from properly catching unauthenticated requests and initiating login redirects.

## 5. Steps to Reproduce

Preconditions:

Access to the backend repository source code

Steps:

1. Perform a static review of the `DELETE/booking/{id}` controller route and authentication middleware.
2.Observe the HTTP status code returned when executing a delete request without supplying an authentication token or cookie header.
   
Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

When a request to `DELETE/booking/{id}` lacks authentication credentials, the API should return an HTTP `401 Unauthorized` status code.

---

## 7. Actual Result

The API returns an HTTP `403 Forbidden` status code when no authentication token is provided.

## 8. Impact Analysis
 
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available

Affected Features: Authentication Guard Middleware, Booking Deletion API, Security Response Mapping
Affected Users: API client applications, automated security suite runners, and frontend apps that rely on 401 Unauthorized status codes to detect missing session authentication.

N/A

### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A

---

## 10. Additional Information   
Root Cause (if known): 

* Requirement ID: N/A
* Standard Ref: RFC 9110 Section 15.5.2 (401 Unauthorized) & Section 15.5.4 (403 Forbidden)
* Regression Info: No
* Related Issues: [REQ-BUG-03](REQ-BUG-03), [REQ-BUG-08](REQ-BUG-08), [REQ-BUG-09](REQ-BUG-09)
* Notes: Standardizing HTTP status codes across all destructive methods (DELETE, PUT, PATCH) ensures uniform error handling across the entire API suite.
  
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
