# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-02 |
| Title/Summary | DeleteBooking endpoint documentation displays HTTP status 201 Created under Success 200 section |
| Date Reported | 11/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☐ Medium ☑ Low |
| Priority | ☐ P0 ☐ P1 ☐ P2 ☐ P3 | (To be assigned by BA/PO)
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
| Test Environment:  |      ☑ Dev ☑ QA ☐ Staging ☐ Production |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description  

The ```DeleteBooking``` documentation page lists a success response header of "Success 200", but the description and response snippet show ```HTTP/1.1 201 Created```. Additionally, the ```Url Parameter``` section incorrectly describes the ```id``` field as the ID for a booking you want to update rather than delete.

#### Detailed Description 

In the Restful-Booker API documentation under the Booking / DeleteBooking section, two documentation inconsistencies exist:

1. Under the Success 200 response block, the field description states "Default HTTP 201 response" and the sample response code block displays ```HTTP/1.1 201 Created```.
2. Under the Url Parameter section, the description for parameter ```id``` states "ID for the booking you want to update" instead of "delete".
---

## 5. Steps to Reproduce

Preconditions:

Access to the API documentation page [https://restful-booker.herokuapp.com/](https://restful-booker.herokuapp.com/)

Steps:

1. Open the API Documentation.
2. Navigate to the left navigation menu under Booking and Click on DeleteBooking
3. Scroll down to the Url Parameter section and inspect the description for ```id```. 
4. Scroll down to the Success 200 section and inspect the field description and the Response: code snippet.

Reproducibility:

* ☑ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result

Under DeleteBooking:

* The Success 200 section should state "Default HTTP 200 response" and display ```HTTP/1.1 200 OK``` (or ```204 No Content``` depending on endpoint specification).

* The Url Parameter description for ```id``` should read: "ID for the booking you want to delete".

---

## 7. Actual Result

Under DeleteBooking:

* The section header reads Success 200, but the description states "Default HTTP 201 response" and the response box shows ```HTTP/1.1 201 Created```.
* The Url Parameter id description states "ID for the booking you want to update".

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available
* ☐ Affected Features: API Documentation, Integration Testing Guidelines

Affected Users: External developers and test analysts integrating with the ```DeleteBooking``` endpoint.

---

## 9. Attachments

### Screenshots/Images
 * Screenshot 1: [Attach-REQ-BUG-02](./Attach-REQ-BUG-02.png) - Annotations pointing out the conflicting Success 200 vs 201 Created status and incorrect id description under DeleteBooking


### Additional Files
 * Console Logs N/A
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A




---

## 10. Additional Information   
Root Cause (if known): Template copy-paste error in the apidoc doc generation file from the UpdateBooking / CreateBooking sections.


### Links & Traceability:

* Requirement ID: API Documentation Specs - Booking Module
* Regression Info: No
* Related Issues: [SCH-BUG-01]()
* Notes: Check if DELETE returns 200 OK or 204 No Content in implementation to ensure documentation alignment.

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
