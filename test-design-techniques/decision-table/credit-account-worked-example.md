[Back](./)

# Credit account worked example

R01: If you are a new customer opening a credit account, you will get a 15% discount on all your purchases today.     
R02: If you are an existing customer and you hold a loyalty card, you get a 10% discount.   
R03: If you have a coupon, you can get 20% off today   
R04: but it cannot be used with the new customer discount.    
R05: Discount amounts are added, if applicable. 

Notes: 
R06: You can not be both a new customer and already hold a loyalty card.
Process of getting of loyalty card is out of scope for this DT


## Questions & Assumptions

| # | Question | Assumption |
|---|----------|------------|
| Q01 | Is it possible for an existing customer to not have a loyalty card? If so, is that customer still eligible to receive a discount when using a coupon?  | A01: Existing customer can be without loyalty card and can receive a discount with coupon |
| Q02 | "You can get 20% off today" — does this apply to a single purchase or to all purchases made today? | A02: A single purchase |
| Q03 | If the coupon is valid for a single purchase, am I still entitled to use my 15% new customer discount on all other purchases throughout the day? | A03: no logic built into DT  |
| Q04 | Are there any limits on the number of coupons per customer? What about limits on the number of coupons that can be used in a single day? | A04: One per person / one per day |
| Q05 | Can coupons be combined  with each other? | A05: No | 
| Q06 | When a new customer has a coupon, does the system automatically apply the higher discount (20% coupon), or can the customer choose between coupon (20%) and new customer discount (15%)? | A06: System applies the higher discount - coupon 20% replaces the 15% new customer discount |

> Note: The first condition starts with F (existing customer) to align rule numbering between the full and collapsed tables.

## Full Decision Table
Test cases = 2 * 2 * 2 = 8 (numbers of rules)

| Condition                                           | Parameters | Rule01 | Rule02 | Rule03 | Rule04 | Rule05 | Rule06 | Rule07 | Rule08  |
|-----------------------------------------------------|------------|--------|--------|--------|--------|--------|--------|--------|---------|
| C1: A new customer (T - new, F - existing)              | T, F    |   F   | F      | F      | F      | T      | T      | T      | T       |
| C2: Hold a loyalty card                                 | T, F    |   T   | T      | F      | F      | N/A    | N/A    | F      | F       |
| C3: You have a coupon                                  | T, F     |   T   | F      | T      | F      | T      | F      | T      | F       |
| Action                                     |            |         |       |        |        |        |        |        |        |         |
| A1: Can get a 15% discount on all your purchases today (R01) |         | -     | -      | -      | -      | N/A    | N/A    | -      | x       |
| A2: Can get a 10% discount (R02)                             |         | x     | x      | -      | -      | N/A    | N/A    | -      | -       |
| A3: Can get 20% off today  (R03)                             |         | x     | -      | x      | -      | N/A    | N/A    | x      | -       |
| A4: No discount (full price)                         |            | -     | -      |  -     |  x     | N/A    | N/A    |  -     | -       |  
| Total discount, %                                   |             | 30    | 10     | 20     | 0      | N/A    | N/A    | 20     | 15      |



## Legend:
* ~ - any parameter
* N/A (in conditions) - this condition causes the infeasibility (R06)
* N/A (in actions) - rule is infeasible, no testable outcome

---

## Traceability Matrix for Full and Collapsed Decision Table 

| Collapsed Rule | Derived from Full Table | Actions |
| :-- | :-- | :-- |
| Rule01 | Rule01 | Use 10% discount loyalty card and 20% coupon |
| Rule02 | Rule02 | Use 10 % discount loyalty card |
| Rule03 | Rule03, Rule07 | Use only coupon |
| Rule04 | Rule04 | Without any discount|
| Rule05 | Rule08 | Use 15 % discount for a new customer|
| N/A | Rule05, Rule06 | You can not be both a new customer and already hold a loyalty card. |

## Collapsed Decision Table 

*(Using "don't care" values (~) and Infeasible conditions (N/A))*

  

| Condition                                           | Parameters | Rule 1 | Rule 2 | Rule 3 | Rule 4 | Rule 5  |
|-----------------------------------------------------|------------|--------|--------|--------|--------|---------|
| C1: A new customer (T - new, F - existing)          | T, F       | F      | F      | ~      | F      | T       |
| C2: Hold a loyalty card                             | T, F       | T      | T      | F      | F      | F       |
| C3: You have a coupon                               | T, F       | T      | F      | T      | F      | F       |
| **Action**                                              |        |        |        |        |        |         |
| A1: Can get a 15% discount on all your purchases today. |        | -      | -      | -      | -      | x       |
| A2: Can get a 10% discount.                             |        | x      | x      | -      | -      | -       |
| A3: Can get 20% off today                               |        | x      | -      | x      | -      | -       |
| A4: No discount (full price)                        |            | -      | -      | -      | x      |  -      |           
| Total discount, %                                   |            | 30     | 10     | 20     | 0      | 15      |

---

## Test suite based on Collapsed Decision Table 
> Note: enough coveradge according to ISTQB


| Test cases | Traceability            |   Test Data                                                 | Expected Result                                     |                       |
|------------|-------------------------|-------------------------------------------------------------|-----------------------------------------------------|-----------------------|
| TC01       |  Rule01, R02, R03, R05  | Existing customer, hold a loyalty card, with a coupon       | 10% +  20% = 30%                                    | passed                |
| TC02       |  Rule02, R02            | Existing customer, hold a loyalty card, without a coupon    | 10%                                                 | passed                |
| TC03       |  Rule03, R03, R04, A06 (assumption) | A new customer with a coupon                    | 20%                                                 | failed                |
| TC04       |  Rule04                 | Existing customer, without a loyalty card, without a coupon | 0%, Full price                                      | passed                |
| TC05       |  Rule05, R01            | A new customer without a coupon                             | 15%                                                 | skipped               |


Additional test cases I would add: 

| Test cases | Traceability            |   Test Data                                                 | Expected Result                                     |     |
|------------|-------------------------|-------------------------------------------------------------|-----------------------------------------------------|-----|
| TC06       |  Rule03, R03           | Existing customer, without a loyalty card, with a coupon     | 20%                                                 | failed  |
| TC07       |  R06                   |  A new customer                                              | System prevents/rejects the combination (new customer + loyalty card) Verify via UI (option blocked/error) AND DB (no such record can exist) | skipped |

---

See also:

* **[Decision Table Testing Practice](./README.md)** -  More examples of designing test cases.
* **[Decision Table Testing](https://olha-yatskivska.github.io/decition-table.html)** -  Summary of the core concepts from ISTQB Advanced Test Analyst.
* **[Decision Table Template](https://olha-yatskivska.github.io/template-decision-table.html)**
* **[Back to Main Page](./)**
