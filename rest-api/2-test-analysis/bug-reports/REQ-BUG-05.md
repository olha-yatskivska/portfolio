# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-05 |
| Title/Summary | [API/DOC/FUN] [GET/booking] Missing input validation for date filters resulting in `500 Internal Server Error` instead of `400 Bad Request` |
| Date Reported | 24/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☑ High ☐ Medium  ☐ Low |
| Priority | ☐ P0 ☑ P1 ☐ P2 ☐ P3 | (To be assigned by BA/PO) |
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

When executing `GET/booking` query requests using invalid or malformed date formats for date filter parameters (`checkin` and `checkout`), the system fails to validate client inputs, returning an unexpected `500 Internal Server Error` instead of a properly handled `400 Bad Request` client error response.

#### Detailed Description 

Static review of the endpoint definitions and source code reveals that input validation on query parameters (`checkin` and `checkout`) is absent or unhandled. When a client passes invalid date strings (e.g., non-ISO formats like DD-MM-YYYY, text strings, or invalid calendar values), the application throws an unhandled server-side parsing exception, resulting in an HTTP `500 Internal Server Error`.

As an API contract standard, malformed or invalid client parameters must be intercepted by request validation middleware and return an HTTP `400 Bad Request` with an appropriate error message explaining the invalid input.

## 5. Steps to Reproduce

Preconditions:

Access to the API documentation page and source code repository.

Steps:

1. Open the API Documentation: [https://restful-booker.herokuapp.com/apidoc/index.html/](https://restful-booker.herokuapp.com/apidoc/index.html) or navigate to the backend routing/controller source code.
2. Inspect the endpoint definitions for GET/booking and its filter variants (`firstname `, `lastname`, `checkin`, `checkout`, and combined parameters).
3. Observe that firstname and lastname are exposed in response bodies and filter parameters without checking for a valid authentication token or enforcing Role-Based Access Control (RBAC).
   
Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

The API should validate client input parameters. When an invalid date format is supplied, the API must respond with an HTTP `400 Bad Request` status code and a clear error payload (e.g., `{"error": "Invalid date format. Expected YYYY-MM-DD"}`).

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
* ☐ Affected Features: Booking Filter API, Request Validation Layer, Error Handling

Affected Users: Missing parameter type/format validation middleware prior to executing database queries or date-parsing logic.

### Screenshots/Images
N/A


### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A

---

## 10. Additional Information   
Root Cause (if known): Missing property-level authorization filters and Role-Based Access Control (RBAC) middleware in response serialization logic.


### Links & Traceability:

* Requirement ID: N/A
* Regression Info: No
* Related Issues: [REQ-BUG-03](REQ-BUG-03), [REQ-BUG-04](REQ-BUG-04)
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
