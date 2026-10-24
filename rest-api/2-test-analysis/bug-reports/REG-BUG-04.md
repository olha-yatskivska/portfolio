# Bug Report Form

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | REQ-BUG-04 |
| Title/Summary | [SEC/DOC] UMissing Property-Level Authorization on GET /booking: Sensitive PII (`firstname`/`lastname`) Exposed Without Authentication |
| Date Reported | 23/10/2026 |
| Reported By | Yatskivska |
| Assigned To | BA/PM |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☑ Critical ☐ High ☐ Medium  ☐ Low |
| Priority | ☑ P0 ☐ P1 ☐ P2 ☐ P3 | (To be assigned by BA/PO) |
| Type |  Functional ☐ Performance ☐ UI/UX ☑ Security ☑ Documentation |
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

The `GET/booking` endpoints (both in documentation and code) permit unauthenticated access to sensitive Personally Identifiable Information (PII) such as `firstname` and `lastname`. While non-sensitive booking details (e.g., `bookingdates`: `checkin`/`checkout`) should remain publicly queryable without authentication, sensitive identity properties are returned without validating user authorization or role-based access permissions.

#### Detailed Description 

Static review of the API documentation and source code reveals an absence of Object/Property-Level Access Control on `GET/booking` endpoints. Unauthenticated requests are allowed to query or retrieve full booking details including customer names (`firstname` and `lastname`).

Under proper security design:

* Unauthenticated Users: Should be permitted to perform GET /booking requests to view public metadata (e.g., check-in and check-out dates) without access to customer names.
* Authenticated Regular Users: Should only receive PII that belongs specifically to their own user account.
* Admin Users: Should have authorized access to view all booking details and customer PII across all users.

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

`GET/booking` endpoints should remain accessible without authentication, but with fine-grained property and role-based filtering:
* Unauthenticated/Public Access: Returns only non-sensitive metadata (e.g., checkin, checkout, booking status). Customer identity fields (firstname, lastname) must be omitted or masked.
* Authenticated Standard User: Returns PII (firstname, lastname) only for bookings owned by that authenticated user.
* Authenticated Admin User: Returns full booking payloads including customer PII for all records.

---

## 7. Actual Result

The API contract and code return customer names (`firstname`, `lastname`) unconditionally on `GET/booking` endpoints, exposing sensitive PII to unauthenticated public requests.

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☑  Partially blocks user workflow
* ☑  Workaround available
* ☐  No workaround available
* ☐ Affected Features: Role-Based Access Control (RBAC), Data Privacy & Masking, Booking Retrieval Service

Affected Users: All registered users whose customer identity details are exposed to unauthenticated public callers.

---

## 9. Attachments

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

* Requirement ID: API Security Specs - Data Protection & Role-Based Access Control
* Vulnerability Type: OWASP API3:2023 - Broken Object Property Level Authorization (BOPLA)
* Regression Info: No
* Related Issues: 
* Notes: Requires partial field masking/dynamic response filtering based on user session role.
  
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
