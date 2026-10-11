[Back to Main Page](../../README.md)

[Back](./)

# Bicycle rental SRM

Your favorite bicycle daily rental store has just introduced a new Customer Relationship Management system and asked you, one of their most loyal members, to test it. The implemented features are as follows:

* R01: Anyone can rent a bicycle, but members receive a 20% discount
* R02: However, if the return deadline is missed, the discount is no longer available
* R03: After 15 rentals, members get a gift: a T-Shirt

---

## Questions & Assumptions

| # | Questions to BA, PO, Dev | Assumption | 
| :--- | :--- | :---: | 
| **Q01** | *After 15 rentals* - Does this mean they get the shirt exactly on the 15th rental, or after every 15 rentals (15th, 30th, 45th)?  | **A01:** Yes, exactly once, on the 15th rental  | 
| **Q02** | Are rentals where the customer missed the return deadline still counted towards the total rentals? | **A02:** Yes, they still count as a completed rental  | 
| **Q03** | Temporary or permanent discount loss? | **A03:** This rental only | 
| **Q04** | Does missed deadline affect the T-shirt too? | **A04:** No, only discount  | 

## Out of Scope (noted for discussion)

| # | Questions | Why noted  | 
| :--- | :--- | :---: | 
| **Q05** | Is there any penalty for a non-member who misses the return deadline? The requirements only mention members losing their discount | Not in requirements but affects UX |
| **Q06** | Does the system use prepayment or postpayment? If it is prepayment, the 20% discount is applied before the rental  | Impacts how discount revocation works technically |


---

## Full Decision Table
Test cases = 2 * 2 * 2 = 8 (numbers of rules)

| Conditions                  | Traceability | Parameters | Rule 1 | Rule 2 | Rule 3 | Rule  4 | Rule 5 | Rule 6 | Rule 7 | Rule 8  |
|-----------------------------|--------------|------------|--------|--------|--------|---------|--------|--------|--------|---------|
| Is a Member?                |    R01       |   T, F     | T      | T      | T      | T       | F      | F      | F      | F       |
| Is deadline  missed?        |    R02       |   T, F     | T      | T      | F      | F       | N/A     | N/A   | N/A   | N/A      |
| Is it 15th rental?          |    R03       |   T, F     | T      | F      | T      | F       | N/A     | N/A   | N/A    | N/A     |
| **Actions**                 |              |            |         |        |        |         |        |        |        |         |
| Rent at full price          |    R01       |            | -      | -      | -      | -       | x      | x      | x      | x       |
| 20% discount                |    R01, R02  |            | -      | -      | x      | x       | -      | -      | -      | -       |
| Get a gift: a T-Shirt       |    R03       |            | x      | -      | x      | -       | -      | -      | -      | -       |


## Collapsed Decision Table 

*(Using not applicable conditions (N/A))*
 

| Conditions             | Traceability  | Parameters  | Rule01  | Rule02 |  Rule03 | Rule04  |  Rule05 |
|------------------------|---------------| ------------|---------|--------|---------|---------|---------|
| Is a Member?           |       R01     |  T, F       | T       | T      | T       | T       | F       |
| Is deadline  missed?   |       R02     |  T, F       | T       | T      | F       | F       | N/A      |
| Is it 15th rental?     |       R03     |  T, F       | T       | F      | T       | F       | N/A      |
| **Actions**            |               |             |         |        |         |         |         |
| Rent at full price     |       R01     |             | -       | -      | -       | -       | x       |
| 20% discount           |       R02     |             | -       | -      | x       | x       | -       |
| Get a gift: a T-Shirt  |       R03     |             | x       | -      | x       | -       | -       |



## BVA for numbers of rentals 

| Identifier |  Boundary   |  Value  | Expected result  |
|------------|-------------|---------|------------------|
| BVA01      |  below      |  14     |  without a gift  |
| BVA02      |  at         |  15     |  get a gift      |
| BVA03      |  above      |  16     |  without a gift  |
| BVA04      |  min        |  1      | without a gift   | 

---



## Test suite based on Collapsed Decision Table and BVA analysis


| Test cases | Traceability        |   Test Data                          | Expected Result                                     |
|------------|---------------------|--------------------------------------|-----------------------------------------------------|
| TC01       |  Rule01/BVA02      | Member, missed deadline, 15th rental  | Full price (no discount - R02) + T-shirt gift (R03) | 
| TC02       |  Rule02/BVA01      | Member, missed deadline, 14th rental  | Full price (no discount – R02), no gift             | 
| TC03       |  Rule03/BVA02      | Member, on-time, 15th rental          | 20% discount (R01) + T-shirt gift (R03)             |
| TC04       |  Rule04/BVA03      | Member, on-time, 16th rental          | 20% discount (R01), no gift                         |
| TC05       |  Rule05/BVA04      | Non-member, 1st rental                | Full price, no discount, no gift                    |


---

See also:

* **[Decision Table Testing Practice](./README.md)** -  More examples of designing test cases.
* **[Decision Table Testing](https://olha-yatskivska.github.io/decition-table.html)** -  Summary of the core concepts from ISTQB Advanced Test Analyst.
* **[Decision Table Template](https://olha-yatskivska.github.io/template-decision-table.html)**
* **[Back to Main Page](./)**

