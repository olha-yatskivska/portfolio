# Bug report 

## 1. Bug Identification

| Field | Details |
| :-- | :-- |
| Bug ID | BUG-05 |
| Title/Summary | [signup] Missing translation key `button.labels.go` in `interviewTranslationService` triggers console errors during component rendering |
| Date Reported | 12/10/2026 |
| Reported By | Yatskivska |
| Assigned To | Frontend/Localization Team |

---

## 2. Classification

| Field | Details |
| :-- | :-- |
| Severity | ☐ Critical ☐ High ☒ Medium ☐ Low |
| Priority | ☐ P0 ☐ P1 ☐ P2 ☒ P3  |
| Type | ☐ Functional ☐ Performance ☒ UI/UX ☐ Security ☐ Documentation |
| Status | ☒ New ☐ Assigned ☐ In Progress ☐ Fixed ☐ Verified ☐ Closed |

---

## 3. Environment Details

| Field | Details |
| :-- | :-- |
| Operating System: |       Windows 11 Pro |
| Browser/Application: |    Google Chrome 154 |
| Device Type:  |           Laptop |
| Application Version: |    Production Build (12/10/2026) |
| Build Number:  |          Current Live Version (12/10/2026) |
| Test Environment:  |      ☐ Dev ☐ QA ☐ Staging ☒ Production [https://survalyzer.com](https://survalyzer.com) |
| Network:       |          WiFi |

---

## 4. Description

#### Brief Description
* During survey/interview component initialization, `interviewTranslationService.getText("button.labels.go")` fails to locate the corresponding translation key in the default text dictionary. This results in an unhandled logger error: `['No translation:', 'button.labels.go']` being printed to the console.

#### Detailed Description

* In `survalyzer-survey.js`, during execution of `updateTexts()`, the application attempts to retrieve the button label text via `this.getGoButtonMessage = this.interviewTranslationService.getText("button.labels.go")`. Inspecting the default translation dictionary object (`this._defaultText`) shows the `button.labels.go` is missing. Consequently, `getText()` triggers `this._logger.error("No translation:", t)`, polluting the browser console with error stack traces during component rendering.

---

## 5. Steps to Reproduce

Preconditions:

 * Access to [https://survalyzer.com/signup](https://survalyzer.com/signup) with browser Developer Tools open
   
Steps:

1. Navigate to [https://survalyzer.com/signup](https://survalyzer.com/signup) 
2. Open Chrome DevTools (F12) and switch to the Console tab
3. Pause on script execution or inspect console logs during survey script loading (`survalyzer-survey.js`).
4. Observe the console error logged by `survalyzer-survey.js:6197: No translation: button.labels.go`
   

Reproducibility:

* ☒ Always (100%)
* ☐ Often (75-99%)
* ☐ Sometimes (25-74%)
* ☐ Rarely (1-24%)
* ☐ Cannot Reproduce

---

## 6. Expected Result 

* `interviewTranslationService` should contain the `button.labels.go` key-value pair in its dictionary , allowing `getText()` to return the localized string cleanly without console errors.

---

## 7. Actual Result

* The translation dictionary lacks `button.labels.go. getText("button.labels.go")` evaluates to fallback/undefined and logs an error in the console: `['No translation:', 'button.labels.go']`

---

## 8. Impact Analysis
 User Impact:
* ☐  Blocks user workflow
* ☒  Partially blocks user workflow (potential fallback string or blank button text shown)
* ☒  Workaround available (system falls back or proceeds with default handling)
* ☐  No workaround available

Affected Features: Localization/i18n Service, Survey UI Button Rendering.
  
Affected Users: All users loading survey components on the platform.

---

## 9. Attachments

### Screenshots/Images
 * [Screenshot 1](./Screenshot_1_BUG-05.png): DevTools Sources panel highlighting `this.interviewTranslationService.getText("button.labels.go")` in `updateTexts()`
 * [Screenshot 2](./Screenshot_2_BUG-05.png): Debugger inspection of `this._defaultText` dictionary missing `button.labels.go` key.
 * [Screenshot 3](./Screenshot_3_BUG-05.png): Screenshot 3: Console log stack trace showing `No translation: button.labels.go`.
   


### Additional Files
 * Stack Trace Log: [survalyzer.com-1791909601272.log](./survalyzer.com-1791909601272.log)
 * Error Reports N/A
 * Network Traces N/A
 * Database Dumps N/A
 

---

## 10. Additional Information 

Root Cause (if known): Missing key entry in `this._defaultText` localization catalog within `survalyzer-survey.js`

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
