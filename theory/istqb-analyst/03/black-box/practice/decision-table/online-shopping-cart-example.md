[Back](./)

# Online Shopping Cart Checkout

You are testing the checkout process of an online shopping cart system.   

| Identifier | Requirement                                                                                              | Traceability to TC   |
|------------|----------------------------------------------------------------------------------------------------------|----------------------|
| R01 | There are regular customers and premium customers, which have a special discounts.                              | TC01-TC07            | 
| R02 | There are three options of payment method: Credit card, PayPal and Gift card.                                   | TC01-TC02, TC04-TC07 |
| R03 | Regular customers can order only products that are in stock now, in other case there should be the validation.  | TC03                 |
| R04 | If Customer has Premium account, there is an option to make pre-order for products out of stock.                | TC04, TC05, TC07     |
| R05 | Gift card payment method is allowed to be used for all users but only for products that are in stock.           | TC02, TC05           |   
 
**Customer Type:**
* Regular customer (T)
* Premium customer (F)

**Product Availability:**
* Product is in stock (T)
* Product is out of stock (F)

**Payment Method:**
* Credit card (a)
* PayPal (b)
* Gift card (c)

**Actions:**
* Action1 : Display a notification about the product being out of stock and pre-order mode
* Action2 : Inform the customer about the unavailability of the product
* Action3 : Show customer the additional field for a Gift Card payment method
* Action4 : Block the Gift card field and prompt the customer to select an alternative payment method
* Action5 : Process the order
---

## Questions & Assumptions

| # | Question | Assumption |
|---|----------|------------|
| Q01 | When does a Regular customer transition to a Premium customer? (Could you also confirm if my understanding is correct: does 'Regular' refer to an unregistered guest user, while 'Premium' refers to a registered account holder?)  | A01: Regular customer - unregistered guest user; Premium - registered account holder |
| Q02 | Does 'Action 5: Process the order' include a pre-order mode? Or is this action triggered only when the product is currently in stock? | A02: No, does not. Does not include a pre-order mode |
| Q03 | What exactly does 'validation' mean in the R03? Is it simply Action 2 (inform about unavailability), or is there a separate validation flow (e.g., waitlist registration, email notification when back in stock)? | A03: There is no additional Action for validation |
| Q04 | Should Action 3 (show gift card field) only appear when the gift card can actually be used (product in stock)? Or does the field always appear and then gets blocked by Action 4 when not applicable? | A04: The additional field for a Gift Card payment method appears after selecting this payment method |
| Q05 | R01 Premium customers have "special discounts", but no corresponding Condition or Action is defined in the spec to apply it. How and when is discount applied to the shopping cart? The DT cannot cover the behavior until the discount logic is specified. Is this an incomplete-requirement defect, or out of scope for this release? | A05: Out of scope |
| Q06 | R03: *Regular customers can order only products that are in stock now* - Does system block order before payment selection is reachable for that case? | A06: Yes, it does |


## Out of Scope (noted for discussion)

| # | Question | Why noted |
|---|----------|-----------|
| Q07 | How should the system behave if the order total is either greater or less than the Gift Card balance? For example, if the balance is insufficient, does the system allow a split payment with PayPal? If the balance is greater, does the remainder stay on the card? | Maybe need its own DT |
| Q08 | Could you clarify what is included in the 'Process the order' action? For example, does it involve: <br> The 'Place Order' button becoming active? <br> Triggering a confirmation email to the customer? <br> An automatic deduction from the inventory (stock count)? <br>  | UX |


## Full Decision Table
Test cases = 2 * 2 * 3 = 12 (numbers of rules)

| Conditions | Parameters | Rule01 |Rule02 | Rule03 | Rule04 | Rule05 | Rule06 | Rule07 | Rule08 | Rule09 | Rule10 | Rule11 | Rule12 |
|-----------------------|------------|--------|-------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|
| Regular customer | T, F   |   T    |   T   |   T    |    T   |    T   |    T   |    F   |    F   |   F    |    F    |    F    |    F    |
| Product is in stock                                                                       | T, F       |   T    |   T   |   T    |    F   |    F   |    F   |    T   |    T   |   T    |    F    |    F    |    F    |
| Payment Method:                                                                           | a, b,c     |   a    |   b   |   c    |   N/A  |   N/A  |   N/A  |    a   |    b   |   c    |    a    |    b    |    c    |
| **Actions**                                                                               |            |        |       |        |        |        |        |        |        |        |         |         |         |
| Display a notification about the product being out of stock and pre-order mode            |            |   -    |   -   |   -    |    -   |    -   |    -   |    -   |    -   |   -    |    x    |    x    |    x    |
| Inform the customer about the unavailability of the product                               |            |   -    |   -   |   -    |    x   |    x   |    x   |    -   |    -   |   -    |    -    |    -    |    -    |
| Show customer the additional field for a Gift Card payment method                         |            |   -    |   -   |   x    |    -   |    -   |    -   |    -   |    -   |   x    |    -    |    -    |    -    |
| Block the Gift card field and prompt the customer to select an alternative payment method |            |   -    |   -   |   -    |    -   |    -   |    -   |    -   |    -   |   -    |    -    |    -    |    x    |
| Process the order                                                                         |            |   x    |   x   |   x    |    -   |    -   |    -   |    x   |    x   |   x    |    x    |    x    |    -    |


## Legend:
* ~ - any parameter
* N/A - not applicable conditions
* a/b - either parameter leads to the same outcome

---

NOTE: Although payment methods a and b are collapsed into a single rule, separate test cases should still be created for each payment method to ensure complete coverage.
---

## Traceability Matrix

| Collapsed Rule | Derived from | Actions |
| :-- | :-- | :-- |
| Rule01 | Full: 1, 2, 7, 8 | Process order |
| Rule02 | Full: 3, 9 | Show gift card + Process |
| Rule03 | Full: 4, 5, 6 | Inform unavailability |
| Rule04 | Full: 10, 11 | Pre-order + Process |
| Rule05 | Full: 12 | Pre-order + Block gift card |

---
## Collapsed Decision Table 

*Using "don't care" values (~) and not applicable conditions (N/A)*

| Conditions                                                                                | Parameters |  Rule01 | Rule02 | Rule03 |  Rule04 |  Rule05 |
|-------------------------------------------------------------------------------------------|------------|---------|--------|--------|----------|--------|
| Regular customer                                                                          | T, F       | ~       | ~      |   T      |     F    |    F   |
| Product is in stock                                                                       | T, F       |    T    |   T    |    F   |     F    |    F   |
| Payment Method:                                                                           | a, b, c    |   a/b   |   c    |   N/A  |    a/b   |    c   |
| **Actions**                                                                               |            |         |        |        |          |        |
| Display a notification about the product being out of stock and pre-order mode            |            |   -     |   -    |    -   |     x    |    x   |
| Inform the customer about the unavailability of the product                               |            |   -     |   -    |    x   |     -    |    -   |
| Show customer the additional field for a Gift Card payment method                         |            |   -     |   x    |    -   |     -    |    -   |
| Block the Gift card field and prompt the customer to select an alternative payment method |            |   -     |   -    |    -   |     -    |    x   |
| Process the order                                                                         |            |   x     |   x    |    -   |     x    |    -   | 

---


## EP for Online Shopping Cart Checkout

| Identifier  |  Traceability to Req     | Traceability to TC       | Traceability to Collapsed Decision Table |   Value                     | Expected result                                                                                   |
|-------------|--------------------------|--------------------------|------------------------------------------|-----------------------------|----------------------------------------------------------------------------------------------------|
| EP-C-01     |  R01, R03                |      TC01, TC02, TC03   | Rule01, Rule02, Rule03                    | Regular customer             |  can order only products that are in stock now, in other case there should be the validation       |
| EP-C-02     |  R01, R04                |      TC04, TC05, TC06, TC07 |  Rule04, Rule05, Rule01, Rule04       | Premium customer            |  there is an option to make pre-order for products out of stock                                    | 
| EP-P-01     |  R03, R04, R05           |      TC01, TC02, TC06    | Rule01, Rule02                           | Product is in stock         |  can be ordered by regular and premium customers, can be payed by Credit card, PayPal, Gift card   | 
| EP-P-02     |  R03, R04, R05           |      TC03, TC04, TC05, TC07 | Rule03, Rule04, Rule05                   | Product is out of stock     |  can be pre-ordered only by premium customer, can be payed only by Credit card or PayPal          | 
| EP-PM-01    |  R02                     |      TC01, TC07          | Rule01, Rule04                           | Credit card                 |  for all users, for all products                                                                   |
| EP-PM-02    |  R02                     |      TC04, TC06          | Rule04, Rule01                           | PayPal                      |  for all users, for all products                                                                   | 
| EP-PM-03    |  R02, R05                |      TC02, TC05          | Rule02, Rule05                           | Gift card                   |  for all users, only for products that are in stock                                                | 
---

## Minimum test suite based on Collapsed Decision Table and EP analysis
> Note: can be expanded or randomize for the automation test suite by test cases from the Full Decision Table 


| Test cases | Traceability to Req | Traceability to EP           | Traceability to Collapsed DT  | Priority  |   Test Data                                          | Expected Result                                     | Execution Result |  
|------------|---------------------| -----------------------------|--------------------------------|---------|---------------------------------------------|-----------------------------------------------------|----------------------------|
| TC01       |   R01, R02          | EP-C-01, EP-P-01, EP-PM-01   |  Rule01                        | Hight |  Regular customer, Product is in stock, Credit card    | Process the order (pending on Q08 clarification)     | passed               |
| TC02       |   R01, R02, R05     | EP-C-01, EP-P-01, EP-PM-03   |  Rule02                        | Medium  | Regular customer, Product is in stock, Gift card      | Show customer the additional field for a Gift Card payment method, Process the order  (pending on Q08 clarification)   | skipped |  
| TC03       |   R01, R03          | EP-C-01, EP-P-02             |  Rule03                        | Hight   | Regular customer, Product is out of stock             | Inform the customer about the unavailability of the product, suggest validation  (pending on Q03 clarification)           | failed |
| TC04       |   R01, R02, R04     | EP-C-02,  EP-P-02, EP-PM-02  |  Rule04                        | Hight | Premium customer, Product is out of stock, PayPal     | Display a notification about the product being out of stock and pre-order mode,<br><br> Process the order (pending on Q08 clarification)                          | passed |
| TC05       |  R01, R02, R04, R05| EP-C-02, EP-P-02, EP-PM-03    |  Rule05                        | Medium | Premium customer, Product is out of stock, Gift card   | Display a notification about the product being out of stock and pre-order mode,<br><br>Block the Gift card field and prompt the customer to select an alternative payment method | passed |


## Additional test cases 

| Test cases | Traceability to Req | Traceability to EP           | Traceability to Collapsed DT   | Priority |  Test Data                                          | Expected Result                                     |
|------------|---------------------| -----------------------------|--------------------------------|-----------|-------------------------------------------|-----------------------------------------------------|
| TC06       |   R01, R02          | EP-C-02, EP-P-01, EP-PM-02   |  Rule01                        | Low     | Premium customer, Product is in stock,  PayPal    | Process the order (pending on Q08 clarification)     | skipped |
| TC07       |   R01, R02, R04     | EP-C-02,  EP-P-02, EP-PM-01  |  Rule04                        | Low    |  Premium customer, Product is out of stock,  Credit card    | Display a notification about the product being out of stock and pre-order mode,<br><br> Process the order (pending on Q8 clarification) | passed | 

---

See also:

* **[Decision Table Testing Practice](./README.md)** -  More examples of designing test cases.
* **[Decision Table Testing](https://olha-yatskivska.github.io/decition-table.html)** -  Summary of the core concepts from ISTQB Advanced Test Analyst.
* **[Decision Table Template](https://olha-yatskivska.github.io/template-decision-table.html)**
* **[Back to Main Page](./)**





