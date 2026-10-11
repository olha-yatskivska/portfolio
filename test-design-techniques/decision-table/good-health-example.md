[Back to Main Page](../../README.md)

[Back](./)

# Good Health example

The insurance company GoodHealth has launched a new health insurance product - for all customers both new and existing - with the following specification:    
R01: Standard premium fee is 500€.    
R02: A bonus program offers customers buying the health insurance product with a 25€ discount to the standard premium fee to accept participating in the medical tests even if they are not participating.     
R03: The customers get a 25€ discount to the standard premium for each one of four medical tests (BMI, blood pressure, glucose, and cholesterol) that they take as part of the yearly medical test    
R04: plus an extra 75€ if they take all the tests.

| # | Question | Assumption |
| :-- | :-- | :-- |
| Q01 | Can a customer accept participation but take zero tests? Do they still receive the 25 € acceptance discount? | A01: Yes - Rule16 / Collapsed Rule 5 covers this |
| Q02 | Can a customer take medical tests without accepting the bonus program participation? | A02: No - acceptance is mandatory |
| Q03 | Is the "all four tests" bonus (75€) applied automatically, or does the customer need to complete them in the same visit/period? | A03: Automatically upon completion of all four |



## Non-collapsed decision table but with the limitation
Test cases = 2 * 2 * 2 * 2 * 2 = 32 (numbers of rules)
> Note: When C1=F (customer declines participation), all 16 combinations produce the same outcome: 0€ discount, all other conditions N/A. Instead of enumerating 32 rules, we show 16 (C1=T) + 1 consolidated rule (C1=F) = 17 rows, cutting the table nearly in half. 
 
| Conditions                                     | Parameters | Rule01 | Rule02 | Rule03 | Rule04 | Rule05 | Rule06 | Rule07 | Rule08 | Rule09 | Rule10  | Rule11  | Rule12  | Rule13  | Rule14  | Rule15  | Rule16  | Rule17    |
|------------------------------------------------|------------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|---------|---------|---------|---------|-----------|
| C1: Accept participating in the medical tests  | T, F       | T      | T      | T      | T      | T      | T      | T      | T      | T      | T       | T       | T       | T       | T       | T       | T       | F         |
| C2: BMI                                        | T, F       | T      | T      | T      | T      | T      | T      | T      | T      | F      | F       | F       | F       | F       | F       | F       | F       | N/A       |
| C3: Blood pressure                             | T, F       | T      | T      | T      | T      | F      | F      | F      | F      | T      | T       | T       | T       | F       | F       | F       | F       | N/A       |
| C4: Glucose                                    | T, F       | T      | T      | F      | F      | T      | T      | F      | F      | T      | T       | F       | F       | T       | T       | F       | F       | N/A       |
| C5: Cholesterol                                | T, F       | T      | F      | T      | F      | T      | F      | T      | F      | T      | F       | T       | F       | T       | F       | T       | F       | N/A       |
| **Actions**                                    |            |        |        |        |        |        |        |        |        |        |         |         |         |         |         |         |         |           |
| Tests taken                                    |            | 4      | 3      | 3      | 2      | 3      | 2      | 2      | 1      | 3      | 2       | 2       | 1       | 2       | 1       | 1       | 0       |           |              
| A1: Discount, €                                |            | 200    | 100    | 100    | 75     | 100    | 75     | 75     | 50     | 100    | 75      | 75      | 50      | 75      | 50      | 50      | 25      |           |

---

## Traceability Matrix 

| Collapsed Rule | Derived from | Actions |
| :-- | :-- | :-- |
| Rule01 | Full: 1 | All tests taken |
| Rule02 | Full: 2, 3, 5, 9 | Any 3 of 4 tests taken - 4 combinations |
| Rule03 | Full: 4, 6, 7, 10, 11, 13 | Any 2 of 4 tests taken - 6 combinations |
| Rule04 | Full: 8, 12, 14, 15 | Any 1 of 4 tests taken - 4 combinations |
| Rule05 | Full: 16 | Accept participation, but doesn't participate |
| Rule06 | Full: 17-32 | The customer doesn't accept participation |

## Collapsed Decision Table 
  
| Conditions                                     | Parameters | Rule01 | Rule02 | Rule03 | Rule04  | Rule05 | Rule06  |
|------------------------------------------------|------------|--------|--------|--------|---------|--------|---------|
| C1: Accept participating in the medical tests  | T, F       | T      | T      | T      | T       | T      | F       |
| C2: BMI                                        | T, F       | T      | T/F    | T/F    | T/F     | F      | N/A     |
| C3: Blood pressure                             | T, F       | T      | T/F    | T/F    | T/F     | F      | N/A     |
| C4: Glucose                                    | T, F       | T      | T/F    | T/F    | T/F     | F      | N/A     |
| C5: Cholesterol                                | T, F       | T      | T/F    | T/F    | T/F     | F      | N/A     |
| **Actions**                                    |            |        |        |        |         |        |         |
| Tests taken                                    |            | 4      | 3      | 2      | 1       |  0     | N/A     |
| A1: Discount,  €                               |            | 200    | 100    | 75     | 50      | 25     | 0       |

## Legend:
* T/F = the specific tests don't matter, but the count of True values must equal 'Tests taken'. E.g., Rule03 (2 tests) = any 2 of C2–C5 are True.
* N/A  - not applicable

---

## Test suite based on Collapsed Decision Table 
> Note: Because Rule02-04 each collapse multiple concrete combinations (e.g., Rule02 covers 4 different '3-of-4-tests' combinations), a tester can rotate the specific combination each run to counter the 'tests wear out' principle. For automation, randomize the True-positions from the full 32-rule table."


| Test cases | Traceability                 |   Test Data                                                      | Expected Result                                                              |
|------------|------------------------------|------------------------------------------------------------------|------------------------------------------------------------------------------|
| TC01       |  Rule01, R01, R02, R03, R04  | Accept participation; all 4 tests taken,  an extra 75€           | 25€ + 25€ + 25€ + 25€ + 25€ + 75€ = 200€ discount, 500€ - 200€ = 300€ fee    | 
| TC02       |  Rule02, R01, R02, R03       | Accept participation; BMI, Blood pressure, Glucose tests taken   | 25€ + 25€ + 25€ + 25€ = 100€ discount, 500€ - 100€ = 400€ fee                | 
| TC03       |  Rule03, R01, R02, R03       | Accept participation; BMI, Cholesterol tests taken               | 25€ + 25€ + 25€ = 75€ discount, 500€ - 75€ = 425€ fee                        |
| TC04       |  Rule04, R01, R02, R03       | Accept participation; Cholesterol tests taken                    | 25€ + 25€ = 50€ discount, 500€ - 50€ = 450€ fee                              |
| TC05       |  Rule05, R01, R02            | Accept participation, but doesn't participate                    | 25€ discount, 500€ - 25€ = 475€ fee                                          |
| TC06       |  Rule06, R01                 | The customer doesn't accept participation                        | 500€ fee                                                                     |


---

See also:

* **[Decision Table Testing Practice](./README.md)** -  More examples of designing test cases.
* **[Decision Table Testing](https://olha-yatskivska.github.io/decition-table.html)** -  Summary of the core concepts from ISTQB Advanced Test Analyst.
* **[Decision Table Template](https://olha-yatskivska.github.io/template-decision-table.html)**
* **[Back to Main Page](./)**


