[Back to Main Page](../../README.md)

[Back](./)

> *Note: This is a raw outcome from the [Detailed Test Cases Generator](https://github.com/olha-yatskivska/detailed-test-cases-generator) (Custom generator used to expand combinatorial pairs into full scenario steps).* 


### TC-P-NP-01: Validate submission with nominal valid integer input for Number of People
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Meal Preferences - Number of People Input

**Preconditions:**
1. User is on the "Your Recipes for Today" page.
2. "Number of People" field is visible and accessible.

**Test Data:**
Number of People = 10

**Execution Steps:**
1. Navigate to the "Number of People" input field.
2. Enter "10" into the input field.
3. Click the "Find Recipes" button.

**Expected Results:**
• Input field accepts value 10.
• System successfully submits request and displays recipe results.
---

### TC-P-NP-02: Validate lower boundary (LB) value for Number of People
- **Priority**: High | **Traceability**: REQ-NP-01 / Boundary Value Analysis (Lower Bound)

**Preconditions:**
1. User is on the "Your Recipes for Today" page.
2. Form is in default state.

**Test Data:**
Number of People = 1

**Execution Steps:**
1. Enter lower boundary value "1" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Input field accepts minimum boundary value 1.
• Form submits successfully and recipe search results are displayed.
---

### TC-P-NP-03: Validate upper boundary (UB) value for Number of People
- **Priority**: High | **Traceability**: REQ-NP-01 / Boundary Value Analysis (Upper Bound)

**Preconditions:**
1. User is on the "Your Recipes for Today" page.
2. Form is ready for submission.

**Test Data:**
Number of People = 100

**Execution Steps:**
1. Enter upper boundary value "100" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Input field accepts maximum boundary value 100.
• Form submits successfully without error.
---

### TC-P-NP-04: Validate input with single leading space before valid number
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Data Sanitization

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = " 10"

**Execution Steps:**
1. Enter single space followed by number " 10" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Leading space is trimmed/sanitized automatically.
• System processes input as integer 10 and displays search results.
---

### TC-P-NP-05: Validate input with multiple leading spaces before valid number
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Data Sanitization

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "                 12"

**Execution Steps:**
1. Enter multiple leading spaces followed by "12" into the field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Leading spaces are stripped automatically.
• Form submits successfully using value 12.
---

### TC-P-NP-06: Validate input with inner spaces between digits
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Data Sanitization

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "1 0"

**Execution Steps:**
1. Enter "1 0" (digits separated by space) into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Space between digits is stripped or sanitized to form number 10.
• Request is submitted successfully.
---

### TC-P-NP-07: Validate pasting valid numeric data using keyboard shortcut (Ctrl+V)
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Input Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.
2. Value "55" is copied to clipboard.

**Test Data:**
Clipboard content = "55"

**Execution Steps:**
1. Select the "Number of People" input field.
2. Paste value "55" using Ctrl+V.
3. Click the "Find Recipes" button.

**Expected Results:**
• Pasted value "55" is populated correctly into input field.
• Search request completes successfully.
---

### TC-P-NP-08: Validate input stepper lower boundary value
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Input Stepper Control

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Stepper value set to 1

**Execution Steps:**
1. Focus on the "Number of People" field.
2. Use stepper controls to adjust value to 1.
3. Click the "Find Recipes" button.

**Expected Results:**
• Stepper control sets value to 1.
• Form processes successfully.
---

### TC-P-NP-09: Validate input stepper upper boundary value
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Input Stepper Control

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Stepper value set to 100

**Execution Steps:**
1. Focus on the "Number of People" field.
2. Use stepper controls to adjust value to 100.
3. Click the "Find Recipes" button.

**Expected Results:**
• Stepper control sets value to 100.
• Form processes successfully.
---

### TC-N-NP-01: Validate validation error when submitting empty mandatory Number of People field
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Mandatory Field Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "" (Empty)

**Execution Steps:**
1. Leave the "Number of People" field empty.
2. Click the "Find Recipes" button.

**Expected Results:**
• Form submission is blocked.
• Error message appears informing user that field is mandatory.
---

### TC-N-NP-02: Validate stepper control prevented or errored below lower boundary (0)
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Input Stepper Boundary Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Stepper value set to 0

**Execution Steps:**
1. Attempt to decrease stepper control value to 0 in "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Stepper prevents set value to 0 or displays error: "Error! Please fill out this field."
---

### TC-N-NP-03: Validate stepper control prevented or errored above upper boundary (101)
- **Priority**: High | **Traceability**: REQ-NP-01 / Input Stepper Boundary Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Stepper value set to 101

**Execution Steps:**
1. Attempt to increase stepper control value to 101.
2. Click the "Find Recipes" button.

**Expected Results:**
• Stepper prevents incrementing past 100 or displays error: "Impossible max 100".
---

### TC-N-NP-04: Validate error message when entering value below lower boundary (0)
- **Priority**: High | **Traceability**: REQ-NP-01 / Boundary Value Analysis (LB-1)

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = 0

**Execution Steps:**
1. Enter "0" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message: "Error! Value must be greater than or equal to 1."
• Form submission is prevented.
---

### TC-N-NP-05: Validate error message when entering value above upper boundary (101)
- **Priority**: High | **Traceability**: REQ-NP-01 / Boundary Value Analysis (UB+1)

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = 101

**Execution Steps:**
1. Enter "101" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message: "Error! Value must be less than or equal to 100."
• Form submission is prevented.
---

### TC-N-NP-06: Validate error message when entering value exceeding byte boundary capacity (256)
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Datatype Limits Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = 256

**Execution Steps:**
1. Enter "256" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message: "Error! Value must be less than or equal to 100."
• Request is rejected.
---

### TC-N-NP-07: Validate rejection of negative integer input (-1)
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Negative Input Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = -1

**Execution Steps:**
1. Enter "-1" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message: "Error! Value must be greater than or equal to 1."
• Negative value is rejected.
---

### TC-N-NP-08: Validate input rejection for exponential character 'e'
- **Priority**: Low | **Traceability**: REQ-NP-01 / Type Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "e"

**Execution Steps:**
1. Enter letter "e" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field blocks entry or displays error: "Error! Please enter a number".
---

### TC-N-NP-09: Validate handling of single leading zero in numeric input
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Formatting & Parsing Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "06"

**Execution Steps:**
1. Enter "06" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message or automatically strips leading zero saving value as "6".
---

### TC-N-NP-10: Validate handling of multiple leading zeros in numeric input
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Formatting & Parsing Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "0000000000015"

**Execution Steps:**
1. Enter "0000000000015" into the field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message or strips leading zeros saving value as "15".
---

### TC-N-NP-11: Validate handling of single leading plus sign in numeric input
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Formatting & Parsing Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "+4"

**Execution Steps:**
1. Enter "+4" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message or strips plus sign saving value as "4".
---

### TC-N-NP-12: Validate error message when entering multiple leading plus signs
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Syntax Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "++++++++++++77"

**Execution Steps:**
1. Enter "++++++++++++77" into the field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error: "Error! Please enter a number" or strips plus signs to save as "77".
---

### TC-N-NP-13: Validate rejection/sanitization of non-printing control characters
- **Priority**: Low | **Traceability**: REQ-NP-01 / Character Set Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Non-printing character U+20B

**Execution Steps:**
1. Paste non-printing character U+20B into "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Non-printing character is rejected/stripped or error message is displayed.
---

### TC-N-NP-14: Validate rejection of operating system special filename characters
- **Priority**: Low | **Traceability**: REQ-NP-01 / Character Set Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "\ * . :,"

**Execution Steps:**
1. Attempt to enter special characters "\ * . :," into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Input is blocked or error message displays: "Error! Please enter a number."
---

### TC-N-NP-15: Validate rejection of ASCII 255 character
- **Priority**: Low | **Traceability**: REQ-NP-01 / Character Set Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
ASCII 255 character "˙"

**Execution Steps:**
1. Attempt to enter ASCII 255 character into the input field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field prevents entry of ASCII 255 character ("Can't add").
---

### TC-N-NP-16: Validate rejection of uppercase alphabetic characters
- **Priority**: Low | **Traceability**: REQ-NP-01 / Character Set Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "A"

**Execution Steps:**
1. Type uppercase letter "A" into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field rejects character entry ("Can't add").
---

### TC-N-NP-17: Validate rejection of lowercase alphabetic characters
- **Priority**: Low | **Traceability**: REQ-NP-01 / Character Set Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "b"

**Execution Steps:**
1. Type lowercase letter "b" into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field rejects character entry ("Can't add").
---

### TC-N-NP-18: Validate handling of pasted string exceeding 500 digits
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Length Limit & Boundary Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.
2. String of 500 digits is copied to clipboard.

**Test Data:**
500-digit string

**Execution Steps:**
1. Paste 500-digit string into field via Ctrl+V.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field truncates string or displays error: "Error! Value must be less than or equal to 100."
---

### TC-N-NP-19: Validate handling of pasted string containing 500 alphanumeric characters
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Input Masking & Length Validation

**Preconditions:**
1. User is on the "Your Recipes for Today" page.
2. String of 500 digits and letters is copied to clipboard.

**Test Data:**
500-character alphanumeric string

**Execution Steps:**
1. Paste 500 alphanumeric characters into field via Ctrl+V.
2. Click the "Find Recipes" button.

**Expected Results:**
• Non-digits are stripped/blocked and numeric portion validated against limit, or error message displays.
---

### TC-N-NP-20: Validate rejection of Mathematical Bold Unicode digits
- **Priority**: Low | **Traceability**: REQ-NP-01 / Unicode Character Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "𝟑𝟒"

**Execution Steps:**
1. Attempt to enter Unicode Math Bold digits "𝟑𝟒" into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field rejects input ("Can't add").
---

### TC-N-NP-21: Validate rejection of ASCII 47 character ('/')
- **Priority**: Low | **Traceability**: REQ-NP-01 / Non-digit Boundary Character

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "/"

**Execution Steps:**
1. Type character "/" into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field rejects character entry ("Can't add").
---

### TC-N-NP-22: Validate rejection of ASCII 58 character (':')
- **Priority**: Low | **Traceability**: REQ-NP-01 / Non-digit Boundary Character

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = ":"

**Execution Steps:**
1. Type character ":" into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field rejects character entry ("Can't add").
---

### TC-N-NP-23: Validate error message when entering non-integer decimal value (6.7)
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Integer Data Type Enforcement

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = 6.7

**Execution Steps:**
1. Enter "6.7" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error: "Error! Please enter a valid value. The two nearest valid values are 6 and 7."
• Form submission is blocked.
---

### TC-N-NP-24: Validate error message when entering decimal with zero fractional part (5.0)
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Integer Data Type Enforcement

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = 5.0

**Execution Steps:**
1. Enter "5.0" into the "Number of People" field.
2. Click the "Find Recipes" button.

**Expected Results:**
• System displays error message: "Error! Please enter a whole number."
• Form submission is blocked.
---

### TC-N-NP-25: Validate rejection of emoji input
- **Priority**: Low | **Traceability**: REQ-NP-01 / Character Set Handling

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "✅"

**Execution Steps:**
1. Attempt to enter emoji "✅" into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Field rejects emoji input ("Can't add").
---

### TC-N-NP-26: Validate prevention of SQL Injection in input field
- **Priority**: Medium | **Traceability**: REQ-NP-01 / Security - SQL Injection Prevention

**Preconditions:**
1. User is on the "Your Recipes for Today" page.

**Test Data:**
Number of People = "1 OR 1=1"

**Execution Steps:**
1. Enter SQL injection string "1 OR 1=1" into field.
2. Click the "Find Recipes" button.

**Expected Results:**
• Input is sanitized or rejected.
• System does not return all records or execute malicious query.
---
