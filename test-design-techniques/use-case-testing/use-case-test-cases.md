[Back to Main Page](../../README.md)

[Back](./)

**Requirements:** [Use Case ID: UC-15504](https://drive.google.com/file/d/16oliLF85i-kHR-oBaY9kCy7bEPyyyq5J/view?usp=sharing)   

**Coverage:** Minimum suite = one test case per path (main + each alternative + each exception) and suggestions for additional test cases, clarifing questionts to BA 
                                                         

## Questions to BA

| # | Question | Raised in |
| :-- | :-- | :-- |
| Q01 | What is a valid voucher code? Can it be reused or it goes into invalid partition after usage?  (TODO: derives EP, BVA for valid/invalid code) | TC-V-01   |
| Q02 | Can ITP switch date if on waiting list for a full date? | TC-V-03 |
| Q03 | How the business want the queue to be realized: concurrency or sequentially (FIFO)? | TC-V-03  |
| Q04 | Change the date: If ITP is on waiting list for Date A, can he switch to date B where spots are available? | TC-V-03  |
| Q05 | Change the location: If location A is full, can ITP select Location B that isn't full | TC-V-03  |
| Q06 | Change the date and the location the same questions | TC-V-03  |
| Q07 | If ITP can change how he can do it? Go back and select a different date/location? Canceling his waiting list position before or after? Can be on multiple waiting lists? |  TC-V-03  |
| Q08 | What is the limit for waiting list? |  TC-V-03  |
| Q09 | Is there a max number of invalid attempts per session? | TC-inV-01 |
| Q10 | Is there a lockout mechanism after N failures? (TODO: If we won't implement it (the financial damage from brute-forced voucher is minimal) - write down it into the one-page test plan or risk-analyze documentation about accepting the risk) | TC-inV-01 |
| Q11 | Is there a time delay between attempts? | TC-inV-01 |
| Q12 | Is the account locked or just the session? | TC-inV-01 |
| Q13 | What if ITP is already registered for the same course? |  TC-inV-02 |
| Q14 | What causes a valid voucher to have no available course sessions, and how does SP detect this? Should the voucher remain valid for future sessions, or is it consumed/refunded?  | TC-inV-02 |
| Q15 | What type of error handling will be for invalid EP? | TC-inV-01 |


BVA for participant limit boundary:

| Identifier | Boundary  |  Values  |  Expected result |  Traceability |
| :-- | :-- | :-- | :-- | :-- | 
| BVA01 | below limit  | 11 participants |  Registration succeeds  | TC-V-01 | 
| BVA02 | at limit   | 12 participants   | Registration succeeds (last spot)   | TC-V-01 | 
| BVA03 | above limit  | 13th participant   |  Placed on waiting list; count stays 12; WL + 1  | TC-V-03 | 


## Main scenario

TC-V-01: Main Scenario - Successful Course Registration    
Objective: Verify that an ITP with a valid voucher can complete full registration flow end-to-end.

Precondition: ITP has a valid voucher code; SP is accessible; course has available spots (<12 participants registered) (BVA01, BVA02)
| # | Test step | Expected result|
| :--- | :--- | :--- |
| 1 | Launch SP  | SP's home page is shown and requests a voucher code from the ITP. |
| 2 | Enter the voucher code (valid EP + BVA (pending Q01 clarification)) | SP lists the dates, locations and current number of registered participants for the course indicated in the voucher code. |
| 3 | Select a date and location  | SP shows an overview of the selected course's contents. |
| 4 | Confirm selection of this course by pressing the "Register" button  | SP places the ITP onto the list of participants and a message shown "You are registered for the course". SP updates the participants list. |
| 5 | Log out | SP's login page is shown |

Postcondition: ITP appears on participants list; participant count incremented by 1; voucher is consumed

Additional test case (pending Q03 clarification): 
Simultaneous registration for the last spot (2 ITPs, 12th seat)    
Expected result: (pending Q03 clarification) - Assumed behavior: one registration succeeds (at limit, last spot), the other is placed on the waiting list. Actual expected outcome depends on concurrency vs FIFO policy 

---

## Alternative flow steps:

TC-V-02 Alternative flow from 2a - Logout from Home Page      
Objective: Verify that an ITP has ability to log out, stability of the system.

Preconditions: ITP has access to SP; SP is accessible

| # | Test step | Expected result|
| :--- | :--- | :--- |
| 1 | Launch SP  | SP's home page is shown and requests a voucher code from the ITP. |
| 2 | Log out from the application's home page  | SP's login page is shown |

Postcondition: No registration occurs; system state unchanged; session terminated

Additional test cases ideas (choose according to time/budget/risk policy):

1. Re-login after log out immediately
2. Re-login after log out after some time before the session timeout threshold
3. Log out from any step 2-4 from TC-V-01 Main Scenario with re-login immediately
4. Log out from any step 2-4 from TC-V-01 Main Scenario with re-login some time before the session timeout threshold
5. Session timeout: remain idle on any page (steps 1–4) beyond the session timeout threshold - verify SP handles expiry gracefully (redirect to login, no data corruption).
6. Log in to SP and change the PC user


TC-V-03 Alternative flow from 8a - Full Course, Waiting List    
Objective: Verify that an ITP with a valid voucher can be added into waiting list if a course is already full. 

Precondition: ITP has a valid voucher code; SP is accessible; the selected course already has exactly 12 participants registered (BVA03)

| # | Test step | Expected result |
| :--- | :--- | :--- |
| 1 | Repeat steps 1-3 from main scenario test case |  Same expected results as main scenario steps 1-3 |
| 2 | Confirm selection of this course by pressing the "Register" button |  SP places the ITP onto a waiting list and a message shown "You are on the waiting list". SP updates the waiting list. |
| 3 | Log out | SP's login page is shown |

Postconditions: ITP appears on the waiting list (not on participants list); participant count remains 12; waiting list count incremented by 1

   
---

## Exceptions

TC-inV-01 Exception E1 -  Invalid Voucher Code    
Objective: Verify that an ITP with a invalid voucher can't complete full registration.

Precondition: ITP has access to SP; SP is accessible; ITP has an invalid voucher code AND a valid voucher code (for recovery verification)

| # | Test step | Expected result|
| :--- | :--- | :--- |
| 1 | Launch SP  | SP's home page is shown and requests a voucher code from the ITP. |
| 2 | Enter invalid voucher code (invalid EP + BVA) | SP shows a message "Voucher not known - please try again". SP returns to the home page |
| 3 | Verify home page is functional (can enter new valid voucher code) | SP accepts valid voucher code |
| 4 | Log out | SP's login page is shown |

Postcondition: No registration occurs after invalid attempt; system remains functional; home page is accessible for retry


TC-inV-02 Exception E2 - No Courses Available        
Objective: Verify that an ITP with a valid voucher can't complete full registration if no courses are available for the voucher code's indicated course.

Precondition: ITP has a valid voucher code; SP is accessible; no courses are available for the voucher code's indicated course

| # | Test step | Expected result|
| :--- | :--- | :--- |
| 1 | Launch SP  | SP's home page is shown and requests a voucher code from the ITP. |
| 2 | Enter the voucher code | SP shows a message "Sorry no courses available - please log out and talk to your manager". Returns to the home page
| 3 | Log out | SP's login page is shown |

Postcondition: No registration occurs; system returns to home page; ITP can log out cleanly

---

TC-E2E-01 	Recovering after error handling: Entering wrong data and getting into waiting list       
Objective: Error Recovery into Capacity Boundary Path

Precondition: ITP has a valid voucher code; SP is accessible; course has no available spots (12 participants)

| # | Test step | Expected result|
| :--- | :--- | :--- |
| 1 | Launch SP  | SP's home page is shown and requests a voucher code from the ITP. |
| 2 | Enter invalid voucher code (invalid EP + BVA) | SP shows a message "Voucher not known - please try again". SP returns to the home page |
| 3 | Verify home page is shown and functional | Home page is displayed; voucher input field is accessible and empty |
| 4 | Enter the valid voucher code (valid EP + BVA) | SP lists the dates, locations and current number of registered participants for the course indicated in the voucher code. |
| 5 | Select a date and location  | SP shows an overview of the selected course's contents. |
| 6 | Confirm selection of this course by pressing the "Register" button  | SP places the ITP onto a waiting list and a message shown "You are on the waiting list". SP updates the waiting list. |
| 7 | Log out | SP's login page is shown |

Postcondition: No registration occurs after invalid attempt; system remains functional; home page is accessible for retry; ITP appears on the waiting list; participant count remains 12; waiting list count is incremented by 1 


---

## Traceability Matrix

| Test Case | Covers UC Steps | Covers Paths | Classification | Purpose |
| :-- | :-- | :-- | :-- | :-- |
| TC-V-01 | 1-9 | Main | Minimum suite | Verifies happy path in isolation |
| TC-V-02 | 1-2, 2a | Alternative | Minimum suite | Verifies early exit path |
| TC-V-03 | 1-8a, 9 | Alternative | Minimum suite | Verifies capacity boundary in isolation |
| TC-inV-01 | 1-3 (E1) | Exception | Minimum suite | Verifies error handling in isolation |
| TC-inV-02 | 1-4 (E2) | Exception | Minimum suite | Verifies unavailability handling in isolation |
| TC-E2E-01 | 1-3(E1) -> 3-8a, 9 | Exception + Alternative | Additional | Recovering after error handling: Entering wrong data and getting into waiting list |


---

See also:


* **[Use Case Testing](https://olha-yatskivska.github.io/use-case-testing.html)** - Summary of core concepts from ISTQB Advanced Test Analyst.


* **[Back to Main Page](./)**
