## Session 2: Legacy Tenant Survey Lifecycle & State Transitions


* Session ID: ET-02

* Date: 14/10/2026

* Time-Box: 20 Minutes

* **Test Charter:** Investigate legacy survey tenant endpoints (rvo.survalyzer.eu) and analyze application behavior during survey state transitions (closed vs. active).

---

### Areas Explored:

1. Navigated through indexed tenant URLs ([https://research2evolve.survalyzer.eu/odagcijshh](https://research2evolve.survalyzer.eu/odagcijshh) and [https://rvo.survalyzer.eu/jeoqgyqlwd](https://rvo.survalyzer.eu/jeoqgyqlwd)) to observe how the system manages transition states when a survey moves from closed/inactive to active.

2. Inspected network traffic, cloud storage responses, DOM component bindings, and localization payloads encountered during the investigation.

---

### Session Results & Side-Discoveries:


[BUG-06](../BUG-06) Google Page 1 search result link directs users to an outdated survey without redirecting to the main homepage

[BUG-07](../BUG-07): Expired Azure SAS tokens (se=2020-12-11) caused 403 Forbidden font asset failures.

[BUG-08](../BUG-08): Survey question component exhibited a `<label for>` attribute mismatch.

[BUG-09](../BUG-09): Input field placeholder displays untranslated Dutch text when English locale is requested.
