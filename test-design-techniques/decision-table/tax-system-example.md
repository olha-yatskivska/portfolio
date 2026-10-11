[Back to Main Page](../../README.md)

[Back](./)

# Tax System

A tax system needs to be updated due to new legislation.    
R01: For a person with a salary of less than 20.000 and who is married, the tax needs to be re-calculated.   
R02: If the person also has more than two and less than five children, an additional 10 % reduction is applicable.

| # | Questions to BA, PO, Dev |  Assumption |
| :--- | :--- | :---: | 
| Q01 | What should be done if a person has exactly 2, less or exactly 5, more children? (The requirement says "> 2 and < 5", which only covers 3 and 4).  | Incomplete requirement? A01: onlly for 3, 4 children  - 10% reduction |
| Q02 | Can a person with a salary >= 20,000 get the 10 % reduction if they have 3-4 children, or is the reduction only for married people making < 20.000? Is there true operator AND between Salary and Married |  A02: true operator AND | 
| Q03 | What is the step for salary? 19.999 or 19.999,99 and 20.001 or 20.000,01? 20.000 less is not included?  |  A03: 19.999 and 20.001 | 
| Q04 | Are there any actions for divorced with children? | A04: out of scope | 
| Q05 | If a person doesn't work and doesn't have any salary (0) ? | Pending on clarification |


## Full Decision Table
Test cases = 2 * 2 * 2 = 8 (numbers of rules)

| Type | Parameters  | Rule 1 | Rule 2 | Rule 3 | Rule 4 |  Rule 5 | Rule 6 | Rule 7 | Rule 8 |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |:---: |:---: |:---: |
| **Salary of less than 20.000?** | T, F                   | T | T | T | T | F | F | F | F |
| **Is married?**   | T, F |                                 T | T | F | F | T | T | F | F |
| **Has more than two and less than five children** ({3, 4})| T, F | T | F |  T | F | T | F | T | F |
| **Action** | ------ | --- | --- | --- | --- | --- | --- | --- | --- | 
| **Tax needs to be re-calculated** |                       | x | x | - | - | - | - | - | - |
| **An additional 10%** |                                   | x | - | - | - | - | - | - | - |


## Legend:
* True: a salary  <  20.000
* False: a salary  >= 20.000
* ~ - any parameter
---


## Collapsed decision table with "don't care" values

| Type                                              | Parameters             | Rule01 | Rule02 | Rule03 | Rule04 | 
| :---                                              | :---                   | :---:  | :---:  | :---:  | :---:  | 
| **Salary of less than 20.000?**                   | T, F                   |    T   |   T    | T      |   F    |
| **Is married?**                                   | T, F                   |    T   |   T    | F      |   ~    |
| **Has more than two and less than five children** | T, F                   |    T   |   F    |  ~     |   ~    |
| **Action**                                        | ----------             |   ---  |   ---  |   ---  |    --- | 
| **Tax needs to be re-calculated**                 |                        |   x    |   x    |    -   |   -    | 
| **An additional 10%**                             |                        |   x    |   -    |    -   |    -   | 



---

## EP for Tax System

| Identifier | Traceability to Req     | Traceability to BVA                          |  Entity   |     Value                       | Expected result                                                 | Traceability to TC         |  
|------------|-------------------------|----------------------------------------------|-----------|------------------------|-------------------------------------------------------------------|---------------------------|
| EP-C-01     |          R02/A01       |           -                                  | children  | no children                     |  doesn't need additional 10 % reduction                         | TC05                       | 
| EP-C-02     |          R02/A01       | BVA-C-01, BVA-C-04                           | children  | has child(children) without tax |  doesn't need additional 10 % reduction                         | TC02, TC03, TC07           |
| EP-C-03     |          R02/A01       | BVA-C-02, BVA-C-03                            | children  | has child(children) for tax     |  see BVA analysis below                                        | TC01, TC04, TC06, TC08     |
| EP-M-01     |          R01/R02       |  BVA-C-01 - BVA-C-04 and BVA-S-01 - BVA-S-03 | marriage  | married                         |  see BVA analysis below                                         | TC01, TC02, TC04-TC08      |
| EP-M-02     |          R01/R02       |           -                                  | marriage  | single, divorced                |  doesn't need  additional 10 % reduction and tax re-calculation | TC03                       |
| EP-S-01     |          R01/A03       |           -                                  | salary    | no salary                       |  pending Q05 clarification                                      | TC06                       | 
| EP-S-02     |          R01/A03       | BVA-S-03, BVA-S-04                           | salary    | has salary > = 20.000           |  doesn't need  tax re-calculation                               | TC04, TC08                  |
| EP-S-03     |          R01/A03       | BVA-S-01, BVA-S-02                           | salary    | has salary  < 20.000            |  see BVA analysis below                                         | TC01, TC02, TC07, TC03, TC05, TC06 |


---

## BVA for Tax System 

| EP                                | Identifier    | Traceability      |  Boundary                           |  Value       | Expected result                          | Traceability to TC (include only TC with nested requirement according to EP column) |
|-----------------------------------|---------------|-----------------  |------------------------------------|--------------|-------------------------------------------| -----------------------------------------------------------------------|
| EP-M-01, EP-S-03, EP-C-03         | BVA-C-01      |  R02/A01          | children - less than min boundary  |  2           |  doesn't need  additional 10 % reduction  |  TC02                                                                  |
| EP-M-01, EP-S-03, EP-C-03         | BVA-C-02      |  R02/A01          | children -  min boundary           |  3           |  additional 10 % reduction                |  TC01                                                                 |
| EP-M-01, EP-S-03, EP-C-03         |  BVA-C-03     |  R02/A01          | children -  max boundary           |  4           |  additional 10 % reduction                |  TC06 (if no salary is the same salary < 20.000 ) else add another TC  |
| EP-M-01, EP-S-03, EP-C-03         |  BVA-C-04     |  R02/A01          | children - more than max boundary  |  5           |  doesn't need additional 10 % reduction   |  TC07                                                                  |
| EP-M-01, EP-S-03                  |  BVA-S-01     |  R01/A03          | salary - less than boundary        |  19.998      |  tax needs to be re-calculated            |  TC02                                                                  |
| EP-M-01, EP-S-03                  |  BVA-S-02     |  R01/A03          | salary - min boundary              |  19.999      |  tax needs to be re-calculated            |  TC01                                                                  |
| EP-M-01, EP-S-02                  |  BVA-S-03     |  R01/A03          | salary - max boundary              |  20.000      |  tax doesn't need to be re-calculated     |  TC04                                                                  |
| EP-M-01, EP-S-02                  |  BVA-S-04     |  R01/A03          | salary - more than max boundary    |  20.001      |  tax doesn't need to be re-calculated     |  TC08                                                                 |

---


## Min test suite based on Collapsed Decision Table and EP/BVA analysis


| Test cases | Traceability Req/Assumption/DT     | Traceability EP/BVA                              |   Test Data                          | Expected Result                                     |
|------------|----------------------------------- |------------------------------------------------- |--------------------------------------|-----------------------------------------------------|
| TC01       |  R01,R02/A01,A03/Rule01            | EP-M-01, EP-S-03, EP-C-03, BVA-C-02, BVA-S-02    | Married, salary 19.999, 3 children   | Tax needs to be re-calculated, An additional 10%    | 
| TC02       |  R01,R02/A01,A03/Rule02            | EP-M-01, EP-S-03,  EP-C-03,  BVA-S-01,  BVA-C-01 | Married, salary 19.998, 2 children    | Tax needs to be re-calculated                       | 
| TC03       |  R01,R02/Rule03                    | EP-M-02,  EP-S-03,  EP-C-02, BVA-C-04            | Single, salary 10.000, 5 children     | Doesn't need any action                             |
| TC04       |  R01,R02/A01,A03/Rule04            | EP-M-01, EP-S-02, EP-C-03, BVA-S-03, BVA-C-03    | Married, salary 20.000, 4 children   | Doesn't need any action                             |

---

## Min additional test cases to cover all EP/BVA 


| Test cases | Traceability Req/Assumption/Q/DT     | Traceability EP/BVA                              |   Test Data                          | Expected Result                                     |
|------------|----------------------------------- |------------------------------------------------- |--------------------------------------|-----------------------------------------------------|
| TC05       |  R01,R02/A01,A03/Rule02            | EP-M-01, EP-S-03, EP-C-01                        | Married, salary 5.000, no children   | Tax needs to be re-calculated                      | 
| TC06       |  R01,R02/A01,A03/Q05 => Rule01?    | EP-M-01, EP-S-01,  EP-C-03,  BVA-C-03            | Married, no salary, 4 children        | pending Q05 clarification                          | 
| TC07       |  R01,R02/A01,A03/Rule02            | EP-M-01,  EP-S-03,  EP-C-02, BVA-C-04            | Married, salary 1.000, 5 children     | Tax needs to be re-calculated                     |
| TC08       |  R01,R02/Rule04                    | EP-M-01, EP-S-02, EP-C-03, BVA-S-04, BVA-C-04    | Married, salary 20.001, 3 children   | Doesn't need any action                             |


> Note: Can be added additional test cases based on '~` from DT, but as DT has nested conditions it doesn't add any coverage value. 

---

See also:

* **[Decision Table Testing Practice](./README.md)** -  More examples of designing test cases.
* **[Decision Table Testing](https://olha-yatskivska.github.io/decition-table.html)** -  Summary of the core concepts from ISTQB Advanced Test Analyst.
* **[Decision Table Template](https://olha-yatskivska.github.io/template-decision-table.html)**
* **[Back to Main Page](./)**


