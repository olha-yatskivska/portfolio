# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-03 |
| Title/Summary | [API-DOC] Ambiguous error handling: Missing expected failure schemas and HTTP status codes |
| Date Reported | 11/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☑  High ☐ Medium  ☐ Low |
| Priority | ☐ P0 ☐ P1 ☑ P2 ☐ P3 | (To be assigned by BA/PO) |
| Type | ☑  Functional ☐ Performance ☐ UI/UX ☐ Security ☑ Documentation |
| Status | ☑ New ☐ Assigned ☐ In Progress ☐ Fixed ☐ Verified ☐ Closed |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 |
| Browser/Application: |    Google Chrome 154 |
| Device Type:  |           Desktop |
| Application Version: |    v1.0.0 |
| Build Number:  |          apidoc 0.25.0 |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☑ Production |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description  

The [Restful Booker API Documentation](https://restful-booker.herokuapp.com/apidoc/index.html) lacks expected failure schemas, error response payloads, and HTTP status codes across all documented endpoints.

#### Detailed Description 

Without documented negative responses and error handling specifications, there is an ambiguity around expected HTTP status codes (such as 400 Bad Request, 401 Unauthorized, 403 Forbidden, or 404 Not Found) and error response stuctures. This forces developers and QA engineers to guess expected failure behaviour rather than testing against a defined API contract.  

## 5. Steps to Reproduce

Preconditions:


Steps:

1. Open the API Documentation: [https://restful-booker.herokuapp.com/apidoc/index.html/](https://restful-booker.herokuapp.com/apidoc/index.html)
2. Navigated through the endpoints (e.g., CreateToken, CreateBooking, GetBooking, HealthCheck)
3. Observe the documented response blocks for each endpoint. 
   
Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

For each endpoint, after the Success section, there are should be an error handling section 

---

## 7. Actual Result

For each endpoint there is only the Success section

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available
* ☐ Affected Features: API Documentation, Integration Testing Guidelines

Affected Users: External developers, API integration partners, and Testers designing negative test suites.

---

## 9. Attachments

### Screenshots/Images



### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A




---

## 10. Additional Information   
Root Cause (if known): 


### Links & Traceability:

* Requirement ID: API Documentation Specs - Booking Module
* Regression Info: No
* Related Issues: 
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
