##  Bug Tracking & Defect Summary

Here is a quick look at my testing notes from two 20-minute exploratory sessions on the Survalyzer platform. 

* [**Session 1**](./Test_Charters/Session_1.md) checking out the sign-up form and UI [https://survalyzer.com/signup](https://survalyzer.com/signup)
* [**Session 2**](./Test_Charters/Session_2.md) looking into tenant survey links: [https://research2evolve.survalyzer.eu/odagcijshh](https://research2evolve.survalyzer.eu/odagcijshh) and [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd).

### Session Results & Defects Logged, 
*(covering UI/UX issues, broken links, accessibility, and localization)*

| Bug ID | Title / Summary | Type / Module | Severity | Priority | Status | Detailed Report |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| **BUG-01** | [signup] Phone Field UI Inconsistency and Country Code Loss During Browser Autofill | Functional / UX (Registration) | Medium | **P2** | `NEW` | [View Report](./BUG-01) |
| **BUG-02** | [signup] Phone field `<label for>` attribute fails to match input id, triggering DevTools accessibility error | Accessibility / DOM (WCAG) | Medium | **P2** | `NEW` | [View Report](./BUG-02) |
| **BUG-03** | [signup] Phone number field is configured as a numerical spinbutton instead of a string input | Architecture / DOM (`<rui>`) | Medium | **P2** | `NEW` | [View Report](./BUG-03) |
| **BUG-04** | [signup] Phone field placeholder displays unformatted raw digits instead of a spaced mask guide | UI/UX (Input Masking) | Low | **P3** | `NEW` | [View Report](./BUG-04) |
| **BUG-05** | [signup] Missing translation key button.labels.go in interviewTranslationService triggers console errors during component rendering | i18n/Frontend Localization | Medium | **P2** | `NEW` | [View Report](./BUG-05) |
| **BUG-06** | Google Page 1 search result link directs users to an outdated survey without redirecting to the main homepage | SEO/ Routing/Lifecycle | Medium | **P2** | `NEW` | [View Report](./BUG-06) |
| **BUG-07** | [rvo.survalyzer] Survey question attribute fails to match input id, triggering DevTools accessibility error | DevOps / Cloud Storage | Medium | **P2** | `NEW` | [View Report](./BUG-07) |
| **BUG-08** | [rvo.survalyzer] Expired Azure SAS tokens cause HTTP 403 Forbidden asset errors for custom fonts | Survey Form Builder| Low | **P3** | `NEW` | [View Report](./BUG-08) |
| **BUG-09** | [rvo.survalyzer] Input field placeholder displays untranslated Dutch text when English locale is requested |  UI Localization/i18n | Low | **P3** | `NEW` | [View Report](./BUG-09) |

---

