# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-08 |
| Title/Summary | [API/SEC] [PUT/booking/{id] returns `403 Forbidden` instead of `401 Unauthorized` when authentication token is missing |
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

When attempting to update a booking via `PUT/booking/{id}` without providing an authentication token (or authorization header/cookie), the server returns HTTP status `403 Forbidden` instead of `401 Unauthorized`.

#### Detailed Description 

Static review of the controller implementation reveals improper HTTP status code assignment for unauthenticated requests. According to HTTP standards (RFC 9110):

* `401 Unauthorized` indicates that the request lacks valid authentication credentials (missing or unauthenticated identity).

* `403 Forbidden` indicates that the server understands the user's authenticated identity, but that specific user lacks permission to access or modify the requested resource.

Returning `403 Forbidden` when credentials are completely missing misrepresents the authentication state and disrupts client-side authentication flow handling (such as triggering automated login redirects upon receiving a 401).


## 5. Steps to Reproduce

Preconditions:

Access to the backend repository source code

Steps:

1. Perform a static review of the `PUT/booking/{id}` controller route and authentication middleware.
2. Observe the HTTP status code returned when a request is executed without passing an authentication token or cookie header.
   
Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

When a request to `PUT/booking/{id}` lacks authentication credentials, the API should return an HTTP `401 Unauthorized` status code.

---

## 7. Actual Result

The API returns an HTTP `403 Forbidden` status code when no authentication token is provided.

## 8. Impact Analysis
 
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available
* ☐ Affected Features: Authentication Middleware, Booking Update API, Security Response Mapping

Affected Users: API client applications and frontend interceptors that rely on `401 Unauthorized` status codes to detect missing authentication sessions and initiate re-authentication workflows.


### Screenshots/Images

N/A


### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A

---

## 10. Additional Information   
Root Cause (if known): Incorrect status code mapping in the authentication guard middleware when handling missing session tokens.

### Links & Traceability:

* Requirement ID: N/A
* Standard Ref: RFC 9110 Section 15.5.2 (401 Unauthorized) & Section 15.5.4 (403 Forbidden)
* Regression Info: No
* Related Issues: [REQ-BUG-03](REQ-BUG-03), [REQ-BUG-04](REQ-BUG-04), [REQ-BUG-07](REQ-BUG-07)
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
