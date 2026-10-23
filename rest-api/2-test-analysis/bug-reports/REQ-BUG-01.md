# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-01 |
| Title/Summary | Ping HealthCheck endpoint documentation displays HTTP status 201 Created under Success 200 section|
| Date Reported | 11/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☑ Medium ☐ Low |
| Priority | ☐ P0 ☐ P1 ☐ P2 ☐ P3 |
| Type | ☐  Functional ☐ Performance ☐ UI/UX ☐ Security ☑ Documentation |
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

The ```GET /ping``` API documentation specifies a "Success 200" response, but the documented sample response block incorrectly displays ```HTTP/1.1 201 Created```

#### Detailed Description

In the Restful-Booker API documentation under the **Ping - HealthCheck** section, the section header and field table indicate a standard ```Success 200``` response. However, the code snippet example for the response displays ```HTTP/1.1 201 Created```. Furthermore, the description field labels "OK" as a "Default HTTP 201 response", introducing conflicting HTTP status codes.

---

## 5. Steps to Reproduce

Preconditions:

Access to the API documentation page [https://restful-booker.herokuapp.com/](https://restful-booker.herokuapp.com/)

Steps:

1. Open the API Documentation.
2. Navigate to the left side menu under Ping and click on HealthCheck.
3. Scroll down to the Success 200 section.   
4. Observe the field description and the example response payload/header. 

Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

* Under the Success 200 section, the response example should display ```HTTP/1.1 200 OK```, matching the status header and HTTP standard for health check endpoints.

---

## 7. Actual Result

* The section header reads Success 200, but the description states *"Default HTTP 201 response"* and the sample response box shows ```HTTP/1.1 201 Created```.

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available
* ☐ Affected Features: API Documentation, Integration Testing Guidelines

Affected Users: External developers and test engineers integrating with the Ping / HealthCheck API.

---

## 9. Attachments

### Screenshots/Images
 * Screenshot 1: [Attach-REQ-BUG-01](./Attach-REQ-BUG-01.png) - Highlighting the discrepancy between "Success 200" and "HTTP/1.1 201 Created" in the documentation.


### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A


---

## 10. Additional Information   
Root Cause (if known): Likely a copy-paste error or misconfiguration in the apidoc source annotations where a 201 status code template was reused for a health check GET request. 

### Links & Traceability:

* Requirement ID: API Doc Specification - HealthCheck Endpoint
* Regression Info: No
* Related Issues: [SCH-BUG-01]()
* Notes: Standard health check (GET /ping) endpoints should return 200 OK.

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
