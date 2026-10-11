[Back to Main Page](../../README.md)

[Back](./)

# Train ticket example

Train ticket purchasing requirements:
* R01: If you want to take a train after 9PM you get the ticket at the “Super-Saver“ price. 
* R02: If you want to take a train before 6AM you get the ticket at a “Saver“ price. 
* R03: At other times of the day you pay the standard price. 
* R04: If you have a Railcard you get a 25% rebate for all tickets except “Super Saver”
  
| # | Question | Assumption |
| :-- | :-- | :-- |
| Q01 | Does "after 9PM" mean strictly after 21:00 (21:01+) or 21:00 inclusive? | A01: Exclusive - 21:00 is Standard, 21:01+ is Super-Saver |
| Q02 | Does "before 6AM" mean strictly before 06:00 (up to 05:59) or 06:00 inclusive? | A02: Exclusive - 05:59 is Saver, 06:00 is Standard |
| Q03 | What about trains exactly at midnight (00:00)?  Is this considered "after 9PM" (previous day) or "before 6AM" (new day)? | A03: 23:59 - Super-Saver; 00:00 - Saver |
| Q04 | Do the three time ranges cover all 24 hours? Specifically: 06:00–21:00 (Standard), 21:01–23:59 (Super-Saver), 00:00–05:59 (Saver) - is this correct? | A04: Yes |
| Q05 | What is the smallest step 1-minute granularity (per HH:MM) or 1-sec granularity (per HH:MM:SS)?                                                     | 1-minute granularity (per HH:MM) |
| Q06 | What is the anchor for time: time of purchase or train departure time?                                                                               | needs clarification  |
| Q07 | What about policy for different types of tickets: Student, Senior, Child, Disability tickets                                                         | needs clarification  |



> Note: If modeled as limited-entry with three separate binary conditions (Is after 9PM? / Is before 6AM? / Is other time?), we'd get 2×2×2×2 = 16 rules, where 10 (62,5%) would be infeasible (a train can only depart in one time range).
> The extended-entry approach with one 3-value condition eliminates this waste: 3×2 = 6 rules, all feasible.


## Legend:
* ~ - any value
* P1 - after 9 PM   (EP+BVA 21:00 | 21:01     23:59 | 00:00 )
* P2 - before 6 AM  (EP+BVA 23:59 | 00:00     05:59 | 06:00 )
* P3 - other time   (EP+BVA 05:59 | 06:00     21:00 | 21:01 ) 

---


## 2-value BVA for Time 

| Identifier    | Traceability      |  Boundary                                    |  Value       | Expected result                          | Traceability to TC |
|---------------|-----------------  |----------------------------------------------|--------------|-------------------------------------------| -------------------|
| BVA01        |  R01/A01/R03/A03  |  less than min boundary P1 / max boundary P3 |  21:00       |   Standard price                          |   TC06             |
| BVA02        |  R01/A01/R03/A03  |  min boundary P1 / more than max boundary P3 |  21:01       |  “Super-Saver“ price                      |   TC01             |
| BVA03        |  R01/A01/R02/A02  |  max boundary P1/ less than min boundary P2  |  23:59       |  “Super-Saver“ price                      |   TC02             |
| BVA04        |  R01/A01/R02/A02  |  more than max boundary P1/ min boundary P2  |  00:00       |  “Saver“  price                           |   TC03             |
| BVA05        |  R02/A02/R03/A03  |  max boundary P2/ less than min boundary P3  |  05:59       |  “Saver“ price                            |   TC04             |
| BVA06        |  R02/A02/R03/A03  |  more than max boundary P2/ min boundary P3  |  06:00       |   Standard price                          |   TC05            |


---

## Full Decision Table 
*Number of rule = 3 * 2 = 6*
  
| Conditions              | Parameters | Rule 1 | Rule 2 | Rule 3 | Rule 4 | Rule 5 | Rule 6  |
|-------------------------|------------|--------|--------|--------|--------|--------|---------|
| C1: Time                | P1, P2, P3 | P1     | P2     | P3     | P1     | P2     | P3      |
| C2: Railcard presents   | T, F       | T      | T      | T      | F      | F      | F       |
| **Actions**             |            |        |        |        |        |        |         |
| A1: “Super-Saver“ price |            | x      | -      | -      | x      | -      | -       |
| A2: "Saver“ price       |            | -      | x      | -      | -      | x      | -       |
| A3: Standard price      |            | -      | -      | x      | -      | -      | x       |
| A4: 25% rebate          |            | -      | x      | x      | -      | -      | -       |


---

## Traceability Matrix

| Collapsed Rule | Derived from | Actions |
| :-- | :-- | :-- |
| Rule 1 | Full: 1, 4 | A1 |
| Rule 2 | Full: 2 | A2 + A4  |
| Rule 3 | Full: 3  |  A3 + A4|
| Rule 4 | Full: 5 | A2 |
| Rule 5 | Full: 6 | A3 |

---

## Collapsed Decision Table 
  
| Conditions              | Parameters | Rule01 | Rule02 | Rule03 | Rule04 | Rule05  |
|-------------------------|------------|--------|--------|--------|--------|---------|
| C1: Time                | P1, P2, P3 | P1     | P2     | P3     | P2     | P3      |
| C2: Railcard presents   | T, F       | ~      | T      | T      | F      | F       |
| **Actions**             |            |        |        |        |        |         |
| A1: “Super-Saver“ price |            | x      | -      | -      | -      | -       |
| A2: "Saver“ price       |            | -      | x      | -      | x      | -       |
| A3: Standard price      |            | -      | -      | x      | -      | x       |
| A4: 25% rebate          |            | -      | x      | x      | -      | -       |


---


## Min test suite based on Collapsed Decision Table and EP/BVA analysis

| Test cases | Traceability                       |  Test Data                           | Expected Result                      |
|------------|----------------------------------- |---------------------------------------|--------------------------------------|
| TC01       | R01/A01/R03/A03/Rule01/BVA02       | Time: 21:01,  Railcard presents: T    | “Super-Saver“ price                  | 
| TC02       | R01/A01/R02/A02/Rule01/BVA03       | Time: 23:59,  Railcard presents: F    | “Super-Saver“ price                  | 
| TC03       | R01/A01/R02/A02/Rule02/BVA04       | Time: 00:00,  Railcard presents: T    | “Saver“ price  + 25% rebate          |
| TC04       | R02/A02/R03/A03/Rule04/BVA05       | Time: 05:59,  Railcard presents: F    | “Saver“  price                       |
| TC05       | R02/A02/R03/A03/Rule03/BVA06       | Time: 06:00,  Railcard presents: T    | Standard price + 25% rebate          |
| TC06       | R01/A01/R03/A03/Rule05/BVA01       | Time: 21:00,  Railcard presents: F    | Standard price                       |



---

See also:

* **[Decision Table Testing Practice](./README.md)** -  More examples of designing test cases.
* **[Decision Table Testing](https://olha-yatskivska.github.io/decition-table.html)** -  Summary of the core concepts from ISTQB Advanced Test Analyst.
* **[Decision Table Template](https://olha-yatskivska.github.io/template-decision-table.html)**
* **[Back to Main Page](./)**


