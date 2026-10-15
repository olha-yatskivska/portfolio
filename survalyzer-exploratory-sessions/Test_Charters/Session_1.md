## Session 1: Registration Flow & UI Consistency


* Session ID: ET-01

* Date: 10/10/2026

* Time-Box: 20 Minutes

* **Test Charter:** Explore the Survalyzer sign-up form to map entry points, evaluate UI component consistency, and inspect browser developer tools for active console errors.

---

### Areas Explored:

1. Entry Points & Navigation: Ways users arrive at the sign-up workflow from organic search and navigation menus.
   * [https://survalyzer.com](https://survalyzer.com) Main content/"Test for free" button
   * [https://survalyzer.com](https://survalyzer.com) Main menu/"Test for free" button
   * [https://survalyzer.com](https://survalyzer.com) -> Solutions -> EX Employee Experience -> Explore EX solutions -> "Get Started For Free" button
   * [https://survalyzer.com](https://survalyzer.com) -> Solutions -> EX Employee Experience -> Explore EX solutions -> Explore Employee Surveys -> "Get Started For Free" button
   * [https://survalyzer.com](https://survalyzer.com) -> Solutions -> CX Customer Experience -> Explore CX solutions -> "Get Started For Free" button
   * [https://survalyzer.com](https://survalyzer.com) -> Solutions -> CX Customer Experience -> Explore CX solutions -> Discover More -> "Get Started For Free" button
   * [https://marketplace.microsoft.com/el-gr/product/survalyzerag1598361881171.survalyzer?tab=overview](https://marketplace.microsoft.com/el-gr/product/survalyzerag1598361881171.survalyzer?tab=overview) -> Details+support -> Test Survalyzer for free 
   
   
2. UI Component Consistency: Visual alignment, form element wrapping, input field masking, and numerical semantics.
3. Console Diagnostics: Active warning and error inspection in Chrome DevTools during form interaction.

---

### Session Results & Defects Logged:

[BUG-01](../BUG-01): [signup] Phone Field UI Inconsistency and Country Code Loss During Browser Autofill

[BUG-02](../BUG-02): [signup] Phone field attribute fails to match input id, triggering DevTools accessibility error

[BUG-03](../BUG-03): [signup] Phone number field is configured as a numerical spinbutton instead of a string input

[BUG-04](../BUG-04): [signup] Phone field placeholder displays unformatted raw digits instead of a spaced mask guide

[BUG-05](../BUG-05): [signup] Missing translation key button.labels.go in interviewTranslationService triggers console errors during component rendering

Side-Discovery ([BUG-06](../BUG-06) Google Page 1 search result link directs users to an outdated survey without redirecting to the main homepage): While exploring brand search entry points, discovered an indexed legacy survey link pointing to an outdated tenant subdomain, bridging the investigation into [Session 2](./Session_2.md). 
