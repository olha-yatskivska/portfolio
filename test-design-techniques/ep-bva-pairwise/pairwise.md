[Back to Main Page](../../README.md)

[Back](./)

# Pairwise Testing: Practical Example



## Target Application: [Pairwise Testing Web App](https://pairwise-testing.netlify.app/)       


Combinatorial tools were evaluated in the [Pairwise Testing Tools Comparison Spreadsheet](https://docs.google.com/spreadsheets/d/1iwLri_iummO5VbK9NMeDdRIPQQAvaEdBTxWiUUDPObo/edit?usp=sharing): 

* Tab 1: Pairwise testing tools comparison: manual pairing vs automated combinatorial engines (PICT, AllPairs, pairwise.teremokgames)
* Tab 2: Allpairs pairing details: documents parameter pairing mechanics and trace identification across test cases.
* Tab 3: PICT negative testing: Defines the selected minimum coverage suite used for framework automation.


After evaluating Microsoft PICT was selected with its advaced modeling capabilities: 

* Parameter Weighting: Prioritizes higher-risk or more common business values
* Negative Combinations: Supports explicit invalid pairing without exploding the test suite size.  

---

### Parameter-Value Model Matrix



| Parameter           |   EP/BVA                                   |    Values                                            | 
| ------------------- | -------------------------------------------| ---------------------------------------------------- |
|  Number of People   | LB-1, LB, Analytical(Weighted), UB, UB+1   | 0 (Invalid), 1, 10 (Weight:10), 100, 101 (Invalid)   |
| Special Occasion    | Nominal & Default                          | None, Birthday, New Year, Easter, Christmas          |
| Diet Types          | Nominal & Multi-select                     | None, Low-Glycemic Index, Vegetarian, Gastris-Friendly, All check |
| Full Matched        | Boolean Toogle                             |  OFF, ON                                             |


---

PICT Model Specification 

```
Special Occasion: None, Birthday, New Year, Easter, Christmas, NA
Diet Types: None, Low-Glycemic Index Diet, Vegetarian Diet, Gastritis-Friendly Diet, All check, NA
Number of People: 0, 1, 10(10), 100, 101
Full Matched: OFF, ON, NA

IF [Number of People] = 0  OR  [Number of People] = 101 THEN [Special Occasion] =  "NA" AND [Diet Types] =  "NA" AND [Full Matched] =  "NA"
  ELSE [Special Occasion] <> "NA" AND [Diet Types] <> "NA" AND [Full Matched] <> "NA";
```

### Generated Pairwise Test Suite (27 Scenarios)

By applying pairwise combinatorial logic, total field combinations were reduced to 27 (25 positive + 2 negative) optimal test cases proving 100% 2-way parameter coverage: 

| Test cases | Special Occasion | Diet Types              | Number of People | Full Matched |
| ---------- | ---------------- | ----------------------- | ---------------- | ------------ |
| TC-01      | Birthday         | Vegetarian Diet         | 1                | OFF          |
| TC-02      | None             | All check               | 10               | OFF          |
| TC-03      | New Year         | None                    | 1                | ON           |
| TC-04      | New Year         | Vegetarian Diet         | 10               | ON           |
| TC-05      | Birthday         | Low-Glycemic Index Diet | 100              | ON           |
| TC-06      | Easter           | None                    | 100              | OFF          |
| TC-07      | None             | Low-Glycemic Index Diet | 10               | OFF          |
| TC-08      | Birthday         | None                    | 10               | ON           |
| TC-09      | None             | Vegetarian Diet         | 100              | ON           |
| TC-10      | Christmas        | Low-Glycemic Index Diet | 1                | ON           |
| TC-11      | New Year         | All check               | 100              | OFF          |
| TC-12      | Christmas        | All check               | 10               | OFF          |
| TC-13      | New Year         | Low-Glycemic Index Diet | 10               | ON           |
| TC-14      | Easter           | Low-Glycemic Index Diet | 10               | ON           |
| TC-15      | Easter           | Vegetarian Diet         | 1                | OFF          |
| TC-16      | Birthday         | Gastritis-Friendly Diet | 100              | OFF          |
| TC-17      | Christmas        | Gastritis-Friendly Diet | 100              | ON           |
| TC-18      | Christmas        | Vegetarian Diet         | 10               | OFF          |
| TC-19      | None             | Gastritis-Friendly Diet | 1                | OFF          |
| TC-20      | None             | None                    | 100              | ON           |
| TC-21      | Easter           | All check               | 1                | ON           |
| TC-22      | Birthday         | All check               | 10               | ON           |
| TC-23      | Christmas        | None                    | 10               | ON           |
| TC-24      | Easter           | Gastritis-Friendly Diet | 10               | ON           |
| TC-25      | New Year         | Gastritis-Friendly Diet | 10               | ON           |
| TC-26      | NA               | NA                      | 101              | NA           |
| TC-27      | NA               | NA                      | 0                | NA           |


*Review full step-by-step executions via [Detailed Test Cases](./detailed-test-cases-pairwise.md) generated by custom utility tool.*

---


## Production Refinements

* Production Expansion Roadmap: To transition this suite into production-ready test documentation, the following steps are planned:

  * Incorporate mandatory field default-state validations (e.g., empty "Number of People"). Added test case TC-N-28 to the [CSV file](./pairwise_data.csv).   

  * Map full Requirements Traceability Matrix (RTM) IDs across each test vector.

  * Build a decision table for output verification once backend recipe logic are delivered. 

* Implemented Automation Scope: For this test framework MVP, all generated pairs are categorized as high-priority regression tests. Assertions validate primary UI state outcomes (e.g. `Success Alert Visible` for valid combinations vs `Success Alert Hidden` for invalid boundaries). Expected result for negative test cases will change when Error Handling Strategy be known (pending Q1, Q6 clarification from [Test Matrix for Input field "Number of People"](./test-matrix.md)). 
 
---

See also:


* **[Pairwise Testing](https://olha-yatskivska.github.io/pairwise.html)** - Summary of the core concepts from ISTQB Advanced Test Analyst.

* **[Pairwise Testing Tools](https://olha-yatskivska.github.io/pairwise-tools.html)** - Collection of Online, Desktop and Console Tools

* **Back to main Page**


