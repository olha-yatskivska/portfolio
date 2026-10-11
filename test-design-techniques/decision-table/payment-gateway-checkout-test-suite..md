[Back to Main Page](../../README.md)

### TC-001: Member 15th Rental with Missed Return Deadline - Full Price + T-Shirt Gift
- **Priority**: Critical | **Type**: Boundary | **Technique**: Decision Table Testing / Boundary Value Analysis
- **Traceability**: R01, R02, R03 / Decision Table Rule 01 / BVA02
- **Preconditions**:
- Customer account exists with 'Member' status active
- Customer has 14 completed rentals recorded in SRM system history
- **Test Data**: `CustomerType: Member, RentalCount: 15, ReturnDeadlineMissed: true, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Log into SRM as staff or API client.
2. Initiate 15th rental order for active Member.
3. Complete rental return processing after the scheduled return deadline (deadline missed).
4. Calculate final billing invoice and evaluate promotional rewards.

- **Expected Result**:
- 20% discount is revoked due to missed deadline (R02). Billing amount is full rate ($20.00).
- T-Shirt gift is triggered and awarded for reaching 15th rental threshold (R03, Q01, Q04).
- Rental count is incremented to 15 in customer history (Q02).
---
### TC-002: Member 14th Rental with Missed Return Deadline - Full Price, No Gift
- **Priority**: High | **Type**: Boundary | **Technique**: Boundary Value Analysis (3-point BVA: Min-1)
- **Traceability**: R01, R02, R03 / Decision Table Rule 02 / BVA01
- **Preconditions**:
- Customer account exists with 'Member' status active
- Customer has 13 completed rentals in history
- **Test Data**: `CustomerType: Member, RentalCount: 14, ReturnDeadlineMissed: true, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Initiate 14th rental order for active Member.
2. Complete rental return after the scheduled deadline.
3. Generate final invoice and check rewards status.

- **Expected Result**:
- Full price ($20.00) charged; discount revoked due to missed deadline (R02).
- No T-Shirt gift awarded (14 rentals < 15 rentals threshold).
- Rental count updated to 14 in customer profile.
---
### TC-003: Member 15th Rental On-Time - 20% Discount + T-Shirt Gift
- **Priority**: Critical | **Type**: Positive | **Technique**: Decision Table Testing / Boundary Value Analysis
- **Traceability**: R01, R03 / Decision Table Rule 03 / BVA02
- **Preconditions**:
- Customer account exists with 'Member' status active
- Customer has 14 completed rentals in history
- **Test Data**: `CustomerType: Member, RentalCount: 15, ReturnDeadlineMissed: false, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Create 15th rental order for active Member.
2. Process rental return on or before scheduled return deadline.
3. Calculate final invoice and system reward assignment.

- **Expected Result**:
- 20% discount applied to daily rate ($16.00 charged instead of $20.00) (R01).
- T-Shirt gift is successfully triggered and flagged for delivery (R03).
- Total rental counter updated to 15.
---
### TC-004: Member 16th Rental On-Time - 20% Discount, No Gift
- **Priority**: High | **Type**: Boundary | **Technique**: Boundary Value Analysis (3-point BVA: Max+1)
- **Traceability**: R01, R03 / Decision Table Rule 04 / BVA03
- **Preconditions**:
- Customer account exists with 'Member' status active
- Customer has 15 completed rentals (and already received T-shirt on 15th)
- **Test Data**: `CustomerType: Member, RentalCount: 16, ReturnDeadlineMissed: false, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Create 16th rental order for active Member.
2. Process rental return on time.
3. Verify billing invoice and reward items.

- **Expected Result**:
- 20% discount applied ($16.00 charged) (R01).
- No T-Shirt gift provided (Q01: T-shirt awarded exactly once on 15th rental).
- Rental count incremented to 16.
---
### TC-005: Non-Member 1st Rental - Full Price, No Discount, No Gift
- **Priority**: High | **Type**: Positive | **Technique**: Equivalence Partitioning / Decision Table Testing
- **Traceability**: R01 / Decision Table Rule 05 / BVA04
- **Preconditions**:
- Customer account exists with 'Non-Member' / Guest status
- **Test Data**: `CustomerType: Non-Member, RentalCount: 1, ReturnDeadlineMissed: false, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Create 1st rental order for Non-Member.
2. Complete return on time.
3. Check billing and reward output.

- **Expected Result**:
- Full rental price ($20.00) charged with 0% discount (R01).
- No gift awarded.
- Rental count initialized to 1.
---
### TC-006: Member 1st Rental On-Time - Minimum Boundary Discount Test
- **Priority**: Medium | **Type**: Boundary | **Technique**: Boundary Value Analysis (Min valid boundary = 1)
- **Traceability**: R01 / BVA04
- **Preconditions**:
- Customer account created as 'Member' with 0 past rentals
- **Test Data**: `CustomerType: Member, RentalCount: 1, ReturnDeadlineMissed: false, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Initiate 1st rental order for new Member.
2. Return bicycle on time.
3. Verify billing invoice.

- **Expected Result**:
- 20% discount applied ($16.00 charged) (R01).
- No gift awarded.
- Rental history updated to 1 rental.
---
### TC-007: Non-Member 15th Rental - Full Price, No Gift Eligibility
- **Priority**: Medium | **Type**: Positive | **Technique**: Equivalence Partitioning / Business Rule Boundary Validation
- **Traceability**: R01, R03 / Decision Table Rule 05
- **Preconditions**:
- Customer account has 'Non-Member' status with 14 past completed rentals
- **Test Data**: `CustomerType: Non-Member, RentalCount: 15, ReturnDeadlineMissed: false, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Initiate 15th rental for Non-Member.
2. Complete rental return on time.
3. Verify invoice details and gift rewards status.

- **Expected Result**:
- Full price ($20.00) charged without discount.
- No T-Shirt gift awarded (R03 applies specifically to members).
---
### TC-008: Member Missed Deadline Recovery on Subsequent Rental (16th)
- **Priority**: High | **Type**: State-Transition | **Technique**: State Transition Testing / Error Guessing
- **Traceability**: R01, R02, Q03
- **Preconditions**:
- Member missed deadline on 15th rental (TC-001 state)
- Customer history now shows 15 total completed rentals
- **Test Data**: `CustomerType: Member, RentalCount: 16, ReturnDeadlineMissed: false, DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Create 16th rental for Member who missed deadline on previous 15th rental.
2. Process rental return on time.
3. Verify billing invoice calculation.

- **Expected Result**:
- 20% discount is successfully restored ($16.00 charged) confirming discount loss is temporary (Q03).
- No gift awarded (already claimed on 15th rental).
---
### TC-009: Invalid Rental Count Validation (0 or negative count)
- **Priority**: Low | **Type**: Negative | **Technique**: Equivalence Partitioning (Invalid EP) / Error Guessing
- **Traceability**: R01, R03 / Error Guessing
- **Preconditions**:
- Member account created
- **Test Data**: `CustomerType: Member, RentalCount: 0 (or -1), DailyRentalRate: $20.00`

#### Test Execution Steps:
1. Attempt to execute rental transaction with system state having 0 prior valid rentals.
2. Verify system behavior during billing and reward evaluation.

- **Expected Result**:
- System handles boundary 0 as initial state without gift triggering.
- Disallows negative counts if manually injected via API/DB integrity check.
---
