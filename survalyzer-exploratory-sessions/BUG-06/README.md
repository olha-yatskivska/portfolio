# Bug report 

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-06 |
| Title/Summary | Google Page 1 search result link directs users to an outdated survey without redirecting to the main homepage |
| Date Reported | 14/10/2026 |
| Reported By | Yatskivska |
| Assigned To | Frontend / SEO Team |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☒ Medium ☐ Low |
| Priority | ☐ P0 ☐ P1 ☒ P2 ☐ P3  |
| Type | ☒ Functional ☐ Performance ☒ UI/UX ☐ Security ☐ Documentation |
| Status | ☐ New ☐ Assigned ☐ In Progress ☐ Fixed ☐ Verified ☐ Closed |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 Pro |
| Browser/Application: |    Google Chrome 154 |
| Device Type:  |           Laptop |
| Application Version: |    Production Build (10/10/2026) |
| Build Number:  |          Current Live Version (10/10/2026) |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production  |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description

* A top organic Google search result (Page 1) points to an outdated survey URL [https://research2evolve.survalyzer.eu/odagcijshh](https://research2evolve.survalyzer.eu/odagcijshh)). Clicking this link leaves potential customers on a dead/inactive page rather than automatically redirecting them to the main platform homepage ([https://survalyzer.com](https://survalyzer.com))

#### Detailed Description

* When searching for 'Survalyzer' on Google, alongside the official homepage link, an expired tenant survey page also appears indexed on Page 1 of organic search results ([https://research2evolve.survalyzer.eu/odagcijshh](https://research2evolve.survalyzer.eu/odagcijshh)). While a valid main site link exists above it, prospective clients who click this secondary indexed link land on an inactive survey with no HTTP redirect or fallback navigation. This causes user drop-off, damages brand trust, and dilutes organic search authority.

## 5. Steps to Reproduce

Preconditions:

 * Open Google Search
   
Steps:

1. Search for `Survalyzer`
2. Locate the organic result pointing to [https://research2evolve.survalyzer.eu/odagcijshh](https://research2evolve.survalyzer.eu/odagcijshh) on Page 1. (10/10/2026)
3. Click on the search result link.
4. Observe the destination page behavior and address bar.

   

Reproducibility:

* ☒ Always (100%) before link change into a new questionnaire (for e.g., [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd))
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result 

* Navigating to an expired or inactive survey URL should perform a 301/302 redirect to the main domain ([https://survalyzer.com](https://survalyzer.com)) or show an interactive 404 page with a "Go to Main Site" CTA button.
* Language preference from Request headers REST API (Accept-Language: uk,en-US;q=0.9,en;q=0.8,pl;q=0.7) is respected in the SOAP XML response.


---

## 7. Actual Result

* The browser remains stuck on the inactive survey page without redirecting the user to [https://survalyzer.com](https://survalyzer.com).
* The backend ignores language preference and forces a hardcoded Dutch string ("Deze vragenlijst is gesloten.").


---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☒  Partially blocks user workflow
* ☒  Workaround available (user can manually enter [https://survalyzer.com](https://survalyzer.com) into the URL bar)
* ☐  No workaround available

Affected Features: Organic Search Traffic Capture, SEO URL Routing, Form Lifecycle Routing.
  
Affected Users: Potential customers finding Survalyzer via Google organic search, as well as external respondents clicking legacy links.

---

## 9. Attachments

### Screenshots/Images
 * [Screenshot 1 10/10/2026](./Screenshot_1_BUG-06.png): Google Page 1 search results showing indexed expired survey link ( [https://research2evolve.survalyzer.eu/odagcijshh](https://research2evolve.survalyzer.eu/odagcijshh)).
 * [Screen Recording (10/10/2026)/ Animated GIF](./Screen_Recording_BUG-06.gif): Demonstration of clicking the Page 1 link and landing on a dead/outdated survey page without redirection.
 * [Screenshot 2 14/10/2026](./Screenshot_2_BUG-06.png): Google Page 1 search results showing indexed a new link ([https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd)).
 * [Screenshot 3 14/10/2026](./Screenshot_3_BUG-06.png): Hardcoded Dutch string ("Deze vragenlijst is gesloten.")
 * [Screenshot 4 14/10/2026](./Screenshot_4_BUG-06.png): REST API request with header Accept-Language: uk,en-US;q=0.9,en;q=0.8,pl;q=0.7 
 * [Screenshot 5 14/10/2026](./Screenshot_5_BUG-06.png): SOAP XML body response ignores language preference

   

### Additional Files
 * Log Response [odagcijshh](./odagcijshh)
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A
 

---

## 10. Additional Information 

Root Cause (if known): Missing 301 Permanent Redirect rule or client-side route guard for expired tenant/survey endpoints.

### Links & Traceability:

* Requirement ID: N/A
* Regression Info: N/A
* Related Issues: N/A

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
