[Back](./)

# Test Matrix for Input field "Number of People"

## Target Application: [Pairwise Testing Web App](https://pairwise-testing.netlify.app/)       


> To create this test matrix, I utilized [Test Matrix Template](https://docs.google.com/spreadsheets/d/1aibTRwH8TQT3JxSCYpMs6LWy-EzLxQo5QEkTkILl1jA/edit?gid=950235574#gid=950235574) inspired by "Lessons Learned in Software Testing" (C. Kaner, J.Bach, B. Pattichord).


## Questions for the Team (BA, PO, QA Lead, Dev)

| Identifier | Questions  | Traceability |
| :--- | :--- | :--- |
| **Q01** | Should character rejection be consistent? Currently, some special symbols trigger an error message, while others are blocked from being typed entirely | TC-N-NP-08 |
| **Q02** | Should we sanitize unsupported input automatically (convert to empty/0), or display a validation error?  [BUG-02](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/bug-reports/BUG-02.md)  |  TC-N-NP-13, TC-N-NP-19 | 
| **Q03** | Should we restrict the input length to a maximum of 3 characters at the UI level?  =>  Clarify, then BUG: Error! Please enter a number | TC-N-NP-18 |
| **Q04** | Regarding SQL injection prevention: Since the backend isn't ready, should the frontend actively sanitize this payload, or simply block non-numeric characters?   | TC-N-NP-26 |
| **Q05** | Currently, validation only triggers upon form submission (clicking "Find Recipe"). Should we implement inline validation (e.g., red borders, tooltips on blur/typing) to improve UX and catch errors earlier? | 

---

> **Note:** All high-priority test cases covering default value and BVA will be combined with [pairwise test techniques](./pairwise.md) and automated via Playwright.                                                                                                                                                                                                                                                                                                                                          
---                                                                                                                                      
                                                                                                                                  
| TC Identifier         | Suite    | Description                                                                 | Test Data                            | Expected Result                                                               | Priority | Result  | Automated |
|----------------|----------|-----------------------------------------------------------------------------|--------------------------------------|--------------------------------------------------------------------------------------|----------|---------|-----------|
| TC-P-NP-01 | Positive | Valid value                                                                 | 10                                   | Success Message                                                                          | Medium   | Passed  | No        |
| TC-P-NP-02 | Positive | LB                                                                          | 1                                    | Success Message                                                                          | High     | Passed  | Yes       | 
| TC-P-NP-03 | Positive | UB                                                                          | 100                                  | Success Message                                                                          | High     | Passed  | Yes       |                      
| TC-P-NP-04 | Positive | Leading spaces                                                              |(space)10                             | Success Message, number without spaces                                                   | Medium   | Passed  | No        |            
| TC-P-NP-05 | Positive | Many leading spaces                                                         |(spaces)                 12           | Success Message, number without spaces                                                   | Medium   | Passed  | No        |
| TC-P-NP-06 | Positive | Inner spaces                                                                | 1(space)0                            | Success Message, number without spaces                                                   | Medium   | Passed  | No        |
| TC-P-NP-07 | Positive | Modifiers (Ctrl+V) with valid data                                          | 55                                   | Success Message                                                                          | Medium   | Passed  | No        |                      
| TC-P-NP-08 | Positive | Input Stepper LB                                                            | 1                                    | Success Message                                                                          | Medium   | Passed  | No        |
| TC-P-NP-09 | Positive | Input Stepper UB                                                            | 100                                  | Success Message                                                                          | Medium   | Passed  | No        |
| TC-N-NP-01 | Negative | Default/empty                                                               | None                                 | Mandatory, Error Message                                                                 | Medium   | Passed  | Yes       |                      
| TC-N-NP-02 | Negative | LB-1 via Input Stepper                                                      | 0                                    | Error! Please fill out this field.                                                       | Medium   | Passed  | Yes       |                      
| TC-N-NP-03 | Negative | UB+1 via Input Stepper                                                      | 101                                  | Impossible max 100                                                                       | High     | Passed  | Yes       |                      
| TC-N-NP-04 | Negative | LB-1                                                                        | 0                                    | Error! Value must be greater than or equal to 1.                                         | High     | Passed  | Yes       |                      
| TC-N-NP-05 | Negative | UB+1                                                                        | 101                                  | Error! Value must be less than or equal to 100.                                          | High     | Passed  | Yes       |                      
| TC-N-NP-06 | Negative | Outside of UB number of digits or characters in BD(integer, varchar, float) | 256                                  | Error! Value must be less than or equal to 100.                                          | Medium   | Passed  | No        |                      
| TC-N-NP-07 | Negative | Negative                                                                    | -1                                   |  Error! Value must be greater than or equal to 1.                                        | Medium   | Passed  | No        |
| TC-N-NP-08 | Negative | `e`                                                                         | e                                    | Error! Please enter a number                                                             | Low      | Passed/Q01 | No     |
| TC-N-NP-09 | Negative | Leading zero                                                                | 06                                   | Error Message or save without 0                                                          | Medium   | Failed/[BUG-01](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/bug-reports/BUG-01.md): save with 0  | No        |
| TC-N-NP-10 | Negative | Many leading zeros                                                          | 0000000000015                        | Error Message  or save without 0                                                         | Medium   | Failed/[BUG-01](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/bug-reports/BUG-01.md): save with 0 | No        | 
| TC-N-NP-11 | Negative | Leading + sign                                                              | +4                                   | Error Message or save without + sign                                                     | Medium   | Failed/[BUG-02](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/bug-reports/BUG-02.md): save with +  | No        |  
| TC-N-NP-12 | Negative | Many leading + signs                                                        | ++++++++++++77                       | Error! Please enter a number <br> or save without + sign.                                | Medium   | Skipped/Q03  | No        |                 
| TC-N-NP-13 | Negative | Non-printing char (Ctrl+char)                                               | U+20B                                | Error Message or save only digits                                                        | Low      | Failed/Q02/[BUG-02](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/bug-reports/BUG-02.md) | No        |           
| TC-N-NP-14 | Negative | O/S file name ("\ * . :")                                                   | \ * . :,                             |  Error! Please enter a number.                                                           | Low      | Passed  | No        |                      
| TC-N-NP-15 | Negative | ASCII 255 (often interpreted as end of file)                                | ˙                                    | Can't add                                                                                | Low      | Passed  | No        |                      
| TC-N-NP-16 | Negative | Uppercase characters                                                        | A                                    | Can't add                                                                                | Low      | Passed  | No        |
| TC-N-NP-17 | Negative | Lowercase                                                                   | b                                    | Can't add                                                                                | Low      | Passed  | No        |                      
| TC-N-NP-18 | Negative | Modifiers (Ctrl+V) too many numbers                                         | [String of 500 digits]               | Error! Value must be less than or equal to 100. <br> + cut for three integer | Medium   | Skipped/Q03 | No        | 
| TC-N-NP-19 | Negative | Modifiers (Ctrl+V) too many numbers+letters                                 | [String of 500 digits+letters]       |                                                                                          | Medium   | Skipped/Q02 | No        |
| TC-N-NP-20 | Negative | Unicode Traps ( `𝟏𝟐𝟑𝟒𝟓` (Math bold))                                        | 𝟑𝟒                                  | Can't add                                                                                | Low      | Passed  | No        |  
| TC-N-NP-21 | Negative | Non-digit (/ ASCII 47)                                                      | /                                    | Can't add                                                                                | Low      | Passed  | No        |    
| TC-N-NP-22 | Negative | Non-digit (: ASCII 58)                                                      | :                                    | Can't add                                                                                | Low      | Passed  | No        |   
| TC-N-NP-23 | Negative | Wrong data type (decimal into integer)                                      | 6.7                                  | Error! Please enter a valid value. <br> The two nearest valid values are 6 and 7.        | Medium   | Passed  | No        |     
| TC-N-NP-24 | Negative | Wrong data type (decimal into integer)                                      | 5.0                                  | Error! Please enter a whole number                                                       | Medium   | Failed/[BUG-03](https://github.com/olha-yatskivska/qa-study-hub/blob/main/theory/istqb-analyst/03/black-box/practice/ep-bva-pairwise/bug-reports/BUG-03.md) | No        | 
| TC-N-NP-25 | Negative | Emoji                                                                       | ✅                                  | Can't add                                                                                 | Low      | Passed  | No        | 
| TC-N-NP-26 | Negative | SQL Injection                                                               | 1 OR 1=1                             | Didn't return all rows from db                                                           | Medium   | Skipped/Q04 | No        | 

 *Review full step-by-step executions via [Detailed Test Cases](./detailed-test-cases-ep-bva.md) generated by custom utility tool.*

 ---
 
 See also: 

* **[Pairwise Testing](https://olha-yatskivska.github.io/pairwise.html)** - Summary of the core concepts from ISTQB Advanced Test Analyst.

* **[Pairwise Testing Tools](https://olha-yatskivska.github.io/pairwise-tools.html)** - Collection of Online, Desktop and Console Tools

* **Back to main Page**
