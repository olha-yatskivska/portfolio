[Back to Main Page](../../README.md)

> Note: Assume the coupon is applied via a YES/NO toggle switch on the UI. 


### TC01: Verify combined 30% discount for an existing customer with a loyalty card and coupon switch set to YES
- **Priority**: High | **Traceability**: Rule01, R02, R03, R05

**Preconditions:**
1. User account exists in system as an existing customer.
2. User holds an active loyalty card linked to their account.
3. User is on the checkout page with items in the cart.

**Test Data:**
Customer Type: Existing
Loyalty Card Status: Active
Cart Subtotal: $100.00
Coupon Toggle Switch: YES

**Execution Steps:**
1. Navigate to the Checkout page with cart total of $100.00.
2. Verify that system recognizes existing customer status and linked loyalty card.
3. Toggle the 'Apply Coupon' switch to 'YES'.
4. Observe the discount breakdown and order total.

**Expected Results:**
1. Loyalty card 10% discount ($10.00) is recognized.
2. Coupon 20% discount ($20.00) is applied.
3. System adds discounts together for a total of 30% ($30.00 off).
4. Total payable amount displays $70.00.
---

### TC02: Verify 10% discount for an existing customer with a loyalty card and coupon switch set to NO
- **Priority**: High | **Traceability**: Rule02, R02

**Preconditions:**
1. User is logged in as an existing customer with an active loyalty card.
2. User has items in the shopping cart.

**Test Data:**
Customer Type: Existing
Loyalty Card Status: Active
Cart Subtotal: $100.00
Coupon Toggle Switch: NO

**Execution Steps:**
1. Proceed to the Checkout page with cart total of $100.00.
2. Ensure the 'Apply Coupon' toggle switch is set to 'NO'.
3. Review the applied discounts in order summary.

**Expected Results:**
1. 10% loyalty card discount ($10.00 off) is applied.
2. No coupon discount is applied.
3. Total discount is 10% ($10.00 off).
4. Total payable amount displays $90.00.
---

### TC03: Verify 20% coupon discount overrides 15% new customer discount when coupon switch is set to YES
- **Priority**: High | **Traceability**: Rule03, R03, R04, A06

**Preconditions:**
1. User is opening a new credit account during checkout.
2. User has items in the shopping cart.

**Test Data:**
Customer Type: New Customer (Credit Account Opening)
Loyalty Card Status: None
Cart Subtotal: $100.00
Coupon Toggle Switch: YES

**Execution Steps:**
1. Select option to open a new credit account during checkout.
2. Toggle the 'Apply Coupon' switch to 'YES'.
3. Review the order total breakdown.

**Expected Results:**
1. System identifies that coupon cannot be combined with new customer discount (R04).
2. System automatically applies the higher discount (20% coupon, $20.00 off) per assumption A06.
3. 15% new customer discount is not combined.
4. Total discount is 20% ($20.00 off) and total payable amount displays $80.00.
---

### TC04: Verify full price (0% discount) for an existing customer without loyalty card and coupon switch set to NO
- **Priority**: Medium | **Traceability**: Rule04

**Preconditions:**
1. User account exists as an existing customer without a loyalty card.
2. User is on the checkout page.

**Test Data:**
Customer Type: Existing
Loyalty Card Status: None
Cart Subtotal: $100.00
Coupon Toggle Switch: NO

**Execution Steps:**
1. Navigate to Checkout page with cart total of $100.00.
2. Confirm the 'Apply Coupon' toggle switch is set to 'NO'.
3. Review the order summary.

**Expected Results:**
1. No discounts are applied to the purchase.
2. Total discount is 0% ($0.00).
3. Total payable amount displays full price of $100.00.
---

### TC05: Verify 15% discount for a new customer opening a credit account with coupon switch set to NO
- **Priority**: High | **Traceability**: Rule05, R01

**Preconditions:**
1. User is opening a new credit account.
2. User has items in cart on checkout page.

**Test Data:**
Customer Type: New Customer (Credit Account Opening)
Loyalty Card Status: None
Cart Subtotal: $100.00
Coupon Toggle Switch: NO

**Execution Steps:**
1. Initiate process to open a new credit account during checkout.
2. Ensure 'Apply Coupon' toggle switch is set to 'NO'.
3. Check calculated discount in order summary.

**Expected Results:**
1. 15% new customer discount ($15.00 off) is applied.
2. Total discount is 15% ($15.00 off).
3. Total payable amount displays $85.00.
---

### TC06: Verify 20% coupon discount for an existing customer without a loyalty card when coupon switch is set to YES
- **Priority**: Medium | **Traceability**: Rule03, R03

**Preconditions:**
1. User account exists as an existing customer without a loyalty card.
2. User is on the checkout page.

**Test Data:**
Customer Type: Existing
Loyalty Card Status: None
Cart Subtotal: $100.00
Coupon Toggle Switch: YES

**Execution Steps:**
1. Navigate to Checkout page with items totaling $100.00.
2. Toggle the 'Apply Coupon' switch to 'YES'.
3. Verify order total breakdown.

**Expected Results:**
1. 20% coupon discount ($20.00 off) is applied.
2. Total discount is 20% ($20.00 off).
3. Total payable amount displays $80.00.
---

### TC07: Verify system prevents assigning loyalty card to a new credit account customer (UI and DB validation)
- **Priority**: Low | **Traceability**: R06

**Preconditions:**
1. User is on the credit account application page.
2. Test analyst has access to system Database and UI.

**Test Data:**
Customer Type: New Customer (Credit Account Opening)
Loyalty Card Field: Selection attempt

**Execution Steps:**
1. Select 'New Customer Credit Account Registration' option on UI.
2. Attempt to select or enter a loyalty card number during registration.
3. Attempt to submit the registration form.
4. Query database for user record: SELECT loyalty_card_id FROM users WHERE customer_id = [NEW_USER_ID];

**Expected Results:**
1. UI blocks loyalty card entry/selection for new customer setup (option disabled or error message shown).
2. Submission with both conditions active is prevented by front-end validation.
3. Database verification confirms no user record can exist with both new customer status and an active loyalty card.
---
