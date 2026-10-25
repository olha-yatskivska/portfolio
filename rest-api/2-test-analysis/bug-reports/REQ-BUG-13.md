# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-13 |
| Title/Summary | [API/SEC] [DELETE/booking/{id}] returns `405 Method Not Allowed` when deleting a non-existent booking ID instead of `404 Not Found` or `401/403` |
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

When attempting to delete a non-existent booking record via `DELETE/booking/{id}` (e.g., using a non-existent ID such as `99999`), the API returns HTTP status `405 Method Not Allowed` instead of evaluating authorization (`401 Unauthorized`/`403 Forbidden`) or returning `404 Not Found` for an authorized request.

#### Detailed Description 

Static review of the route definition and controller implementation reveals improper HTTP status code assignment for deletion operations on non-existent targets. According to HTTP standards (RFC 9110):
* `405 Method Not Allowed` indicates that the target endpoint path does not support the HTTP verb (`DELETE`). Since `DELETE` is an allowed HTTP method for `/booking/{id}`, returning `405` is semantically incorrect.
* If the request lacks valid authentication or proper permissions, security middleware must reject the request first with `401 Unauthorized` or `403 Forbidden`.
* If the request is properly authorized but no booking exists with the specified ID, the endpoint must return `404 Not Found`.

Returning `405 Method Not Allowed` misleads client applications into treating the `DELETE` method as unsupported on the endpoint rather than correctly handling authentication or missing resource states.


## 5. Steps to Reproduce

Preconditions:

Access to the backend repository source code

Steps:

1. Perform a static review of the `DELETE/booking/{id}` controller route and path parameter handling.
2. Observe the HTTP status code logic executed when a delete request targets a non-existent booking ID (e.g., `DELETE/booking/99999`).
   
Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

For requests targeting a non-existent booking ID:
* If unauthenticated or unauthorized: Return `401 Unauthorized` or `403 Forbidden`.
* If authorized: Return `404 Not Found` (indicating the resource does not exist).

---

## 7. Actual Result

The API returns HTTP status `405 Method Not Allowed` when performing a `DELETE` request on a non-existent booking ID.

## 8. Impact Analysis
 
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available

Affected Features: Endpoint Routing Layer, Resource Resolution Middleware, Error Handling Logic
Affected Users: Developers and automated API integration clients receiving inaccurate HTTP routing errors when handling resource deletion failures.
## 9. Attachments

Screenshots/Images
N/A

### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A

---

## 10. Additional Information   
Root Cause (if known): 

Links & Traceability:

* Requirement ID: N/A
* Standard Ref:RFC 9110 Section 15.5.6 (404 Not Found) & Section 15.5.7 (405 Method Not Allowed)
* Regression Info: No
* Related Issues: [REQ-BUG-03](REQ-BUG-03), [REQ-BUG-08](REQ-BUG-08), [REQ-BUG-09](REQ-BUG-09)
* Notes: 
  
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
