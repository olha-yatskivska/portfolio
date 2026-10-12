# QA Test Analysis and Design Portfolio


* Detail-oriented **Middle QA Engineer** with 5+ years of commercial experience in fast-paced Agile (Scrum/Kanban) environments.
* Specialized in AdTech **Web/SaaS applications**, **REST API** testing, test design techniques, and **root-cause defect analysis** using system logs and **SQL**.
* **Certified in ISTQB CTFL** with foundational skills in **Playwright**, Pytest, and Python.

---

I want to show a deep focus on **black-box test design techniques**. Nowadays, when you can simply generate any app or artifact for repetitive work using **LLMs** - such as detailed test cases, test conditions, requirements, reports, and automation scripts - the main challenge is how to **minimize this testware explosion**. 

The answer lies in mastering core test design:

* Optimized Coverage: Combining techniques to determine the set of test cases needed for minimum test coverage before expanding based on **risk-based analysis**.
  
* **AI-Assisted** Efficiency: Utilizing custom **AI tooling**, such as my vibe-coded Detailed Test Case Generator [[TestFlow Analyst Studio]](https://github.com/olha-yatskivska/detailed-test-cases-generator) (built via **Google AI Studio**), to rapidly convert combinatorial models into fully structured, high-value test scenarios.


This portfolio is built based on the **ISTQB Advanced Test Analyst syllabus**. Future plans include adding new test design techniques from the latest ISTQB Advanced Test Analyst (v4.0) syllabus, such as metamorphic, guided, and adaptive random testing.

---

> My notes on preparation for the ISTQB Advanced Test Analyst exam can be found on my [Personal QA Library site](https://olha-yatskivska.github.io/)


---



| Folder                                                                                        | What you can find inside                                                                                                                                      | Status | Source of test example requirement |
| --                                                                                            |  --                                                                                                                                                         |  --    |  ---                        |
| [Classification Tree Technique](./test-design-techniques/classification-tree)                 | Practical example mapping multi-variable input domains to systematically reduce test combinations while maintaining high-risk coverage. |  DONE  | Course ISTQB Advanced Test Analyst from the Trainer Alexandra Kovalova |
| [Tricky Decision Table Terms](./test-design-techniques/decision-table)                         |  Clear-cut examples and boundary clarifications for complex business logic rules to prevent combinatorial explosion.                                          |  DONE | Course ISTQB Advanced Test Analyst from the Trainer Alexandra Kovalova |
| [Pairwise + EP/BVA Testing: Practical Example](./test-design-techniques/ep-bva-pairwise)       | Practical combination of single-field EP/BVA, Microsoft PICT 2-wise combinatorial reduction, Playwright (Pytest) data-driven CSV test execution               |  FIX    | Myself generated. TO FIX:  discrepancies for GitHub version and for local version for Allure Report generation |
| [State Transition Testing: Practical Examples](./test-design-techniques/state-transition-diagrams) | Practical state-transition diagrams and transition tables to validate complex application lifecycles, negative paths, and sequence-dependent behavior.    |  DONE    | [Topic support guide from Cambridge State-transition diagrams](https://www.cambridgeinternational.org/images/285020-topic-4.2.3-state-transition-diagrams-9608-.pdf) | Real-world business scenarios mapping user interactions, alternative flows, and system behaviors for comprehensive acceptance validation.
| [Use Case Testing: Practical Examples](./test-design-techniques/use-case-testing)            |    Real-world business scenarios mapping user interactions, alternative flows, and system behaviors for comprehensive acceptance validation.                 |  DONE    | Course ISTQB Advanced Test Analyst from the Trainer Alexandra Kovalova
| [API testing restful-booker app](./rest-api)                                                  | End-to-end Mini STLC implementation featuring a [test-planning](./rest-api/1-test-planning), [test analysis](./rest-api/2-test-analysis), [test design](./rest-api/3-test-design), test implementation - [Postman API collections](./rest-api/4-test-implementation), test execution, and test completion.  |  IN PROGRESS      | [API documentation](https://restful-booker.herokuapp.com/apidoc/index.html#api-Booking-GetBookings) [Repository restful-booker](https://github.com/olha-yatskivska/restful-booker)  forked from mwinteringham/restful-booker |
