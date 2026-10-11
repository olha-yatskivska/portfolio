[Back](./)

> *Note: This is a raw outcome from the [Detailed Test Cases Generator](https://github.com/olha-yatskivska/detailed-test-cases-generator) (Custom generator used to expand combinatorial pairs into full scenario steps).*


### TC-P-01: Verify recipe search for Birthday occasion, Vegetarian Diet, 1 person, and Full Matched OFF
- **Priority**: High | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is navigated to the 'Your Recipes for Today' page.
2. Recipe search form is displayed with default values.

**Test Data:**
Pantry: Meat=None, Fish=None, Vegetables=None; Special Occasion: Birthday; Diet Types: Vegetarian Diet; Number of People: 1; Full Matched: OFF

**Execution Steps:**
1. Verify Pantry options (Meat, Fish, Vegetables) are set to 'None'.
2. Ensure 'Full Matched' toggle is OFF.
3. Select 'Birthday' from the 'Special Occasion' dropdown.
4. Enter or select '1' in 'Number of People'.
5. Check the 'Vegetarian Diet' checkbox.
6. Click 'Find Recipes' button.

**Expected Results:**
- Search request is processed successfully.
- Relevant recipe results matching the selected criteria (Birthday, Vegetarian Diet, serving 1) are displayed.
---

### TC-P-02: Verify recipe search with default occasion, all diet types selected, 10 people, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is navigated to the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None; Diet Types: Low-Glycemic Index Diet, Vegetarian Diet, Gastritis-Friendly Diet; Number of People: 10; Full Matched: OFF

**Execution Steps:**
1. Keep Pantry items as 'None'.
2. Keep Special Occasion as 'None'.
3. Select all Diet Types checkboxes (Low-Glycemic Index Diet, Vegetarian Diet, Gastritis-Friendly Diet).
4. Set 'Number of People' to 10.
5. Ensure 'Full Matched' toggle is OFF.
6. Click 'Find Recipes' button.

**Expected Results:**
- Search is performed successfully.
- System displays recipes compatible with all checked diet types for 10 people.
---

### TC-P-03: Verify recipe search for New Year occasion, no diet types selected, 1 person, and Full Matched ON
- **Priority**: High | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: New Year; Diet Types: None; Number of People: 1; Full Matched: ON

**Execution Steps:**
1. Leave Pantry items set to 'None'.
2. Toggle 'Full Matched' to ON.
3. Select 'New Year' from 'Special Occasion' dropdown.
4. Set 'Number of People' to 1.
5. Ensure no Diet Types checkboxes are checked.
6. Click 'Find Recipes' button.

**Expected Results:**
- Search executes successfully.
- Exact-match recipes for New Year celebration serving 1 person are returned.
---

### TC-P-04: Verify recipe search for New Year occasion, Vegetarian Diet, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: New Year; Diet Types: Vegetarian Diet; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Leave Pantry items set to 'None'.
2. Toggle 'Full Matched' switch to ON.
3. Select 'New Year' from 'Special Occasion' dropdown.
4. Set 'Number of People' to 10.
5. Select 'Vegetarian Diet' checkbox.
6. Click 'Find Recipes' button.

**Expected Results:**
- Search completes without error.
- System returns fully matched recipes tailored for New Year, Vegetarian Diet, for 10 people.
---

### TC-P-05: Verify recipe search for Birthday occasion, Low-Glycemic Index Diet, 100 people, and Full Matched ON
- **Priority**: High | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Birthday; Diet Types: Low-Glycemic Index Diet; Number of People: 100; Full Matched: ON

**Execution Steps:**
1. Leave Pantry dropdowns at 'None'.
2. Enable 'Full Matched' toggle (ON).
3. Select 'Birthday' from 'Special Occasion'.
4. Set 'Number of People' to 100.
5. Select 'Low-Glycemic Index Diet' checkbox.
6. Click 'Find Recipes'.

**Expected Results:**
- System processes search with maximum allowed headcount (100).
- Results display matching recipes scaled for 100 people adhering to Low-Glycemic Index Diet.
---

### TC-P-06: Verify recipe search for Easter occasion, no diet types selected, 100 people, and Full Matched OFF
- **Priority**: High | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Easter; Diet Types: None; Number of People: 100; Full Matched: OFF

**Execution Steps:**
1. Keep Pantry options as 'None'.
2. Set 'Full Matched' toggle to OFF.
3. Select 'Easter' from 'Special Occasion'.
4. Set 'Number of People' to 100.
5. Leave all Diet Types unchecked.
6. Click 'Find Recipes'.

**Expected Results:**
- Search executes successfully.
- System displays recipes suited for Easter for 100 people.
---

### TC-P-07: Verify recipe search with default occasion, Low-Glycemic Index Diet, 10 people, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None; Diet Types: Low-Glycemic Index Diet; Number of People: 10; Full Matched: OFF

**Execution Steps:**
1. Keep Pantry dropdowns as 'None'.
2. Keep Special Occasion as 'None'.
3. Select 'Low-Glycemic Index Diet'.
4. Set 'Number of People' to 10.
5. Ensure 'Full Matched' toggle is OFF.
6. Click 'Find Recipes'.

**Expected Results:**
- Search is executed.
- Recipes for Low-Glycemic Index Diet for 10 people are displayed.
---

### TC-P-08: Verify recipe search for Birthday occasion, no diet types, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Birthday; Diet Types: None; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Set Pantry to 'None'.
2. Turn 'Full Matched' switch ON.
3. Choose 'Birthday' under 'Special Occasion'.
4. Enter '10' in 'Number of People'.
5. Uncheck all Diet Types checkboxes.
6. Click 'Find Recipes'.

**Expected Results:**
- Search completes successfully.
- Exact-match Birthday recipes for 10 people are listed.
---

### TC-P-09: Verify recipe search with default occasion, Vegetarian Diet, 100 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None; Diet Types: Vegetarian Diet; Number of People: 100; Full Matched: ON

**Execution Steps:**
1. Ensure Pantry selections are 'None'.
2. Turn ON 'Full Matched'.
3. Leave Special Occasion as 'None'.
4. Enter '100' for 'Number of People'.
5. Check 'Vegetarian Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- System processes search successfully.
- Full-match Vegetarian recipes for 100 people are displayed.
---

### TC-P-10: Verify recipe search for Christmas occasion, Low-Glycemic Index Diet, 1 person, and Full Matched ON
- **Priority**: High | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Christmas; Diet Types: Low-Glycemic Index Diet; Number of People: 1; Full Matched: ON

**Execution Steps:**
1. Keep Pantry as 'None'.
2. Turn ON 'Full Matched'.
3. Select 'Christmas' from 'Special Occasion'.
4. Set 'Number of People' to 1.
5. Select 'Low-Glycemic Index Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search executes successfully.
- Results show Christmas recipes matching Low-Glycemic Index Diet for 1 person.
---

### TC-P-11: Verify recipe search for New Year occasion, all diet types checked, 100 people, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: New Year; Diet Types: Low-Glycemic Index Diet, Vegetarian Diet, Gastritis-Friendly Diet; Number of People: 100; Full Matched: OFF

**Execution Steps:**
1. Leave Pantry as 'None'.
2. Set 'Full Matched' to OFF.
3. Select 'New Year' from Special Occasion.
4. Check all three Diet Types checkboxes.
5. Set 'Number of People' to 100.
6. Click 'Find Recipes'.

**Expected Results:**
- System returns recipes matching New Year criteria and all selected diet types for 100 people.
---

### TC-P-12: Verify recipe search for Christmas occasion, all diet types checked, 10 people, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Christmas; Diet Types: Low-Glycemic Index Diet, Vegetarian Diet, Gastritis-Friendly Diet; Number of People: 10; Full Matched: OFF

**Execution Steps:**
1. Keep Pantry selections at 'None'.
2. Set 'Full Matched' toggle to OFF.
3. Select 'Christmas' from Special Occasion dropdown.
4. Select all Diet Types checkboxes.
5. Set 'Number of People' to 10.
6. Click 'Find Recipes'.

**Expected Results:**
- Search is successful.
- Results display Christmas recipes accommodating all three diet types for 10 people.
---

### TC-P-13: Verify recipe search for New Year occasion, Low-Glycemic Index Diet, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: New Year; Diet Types: Low-Glycemic Index Diet; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Set Pantry dropdowns to 'None'.
2. Switch 'Full Matched' to ON.
3. Select 'New Year' from Special Occasion.
4. Set 'Number of People' to 10.
5. Check 'Low-Glycemic Index Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search executes successfully.
- Exact matching recipes for New Year with Low-Glycemic Index Diet for 10 people are shown.
---

### TC-P-14: Verify recipe search for Easter occasion, Low-Glycemic Index Diet, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Easter; Diet Types: Low-Glycemic Index Diet; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Keep Pantry as 'None'.
2. Switch 'Full Matched' to ON.
3. Select 'Easter' from Special Occasion.
4. Set 'Number of People' to 10.
5. Check 'Low-Glycemic Index Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- System processes the request.
- Exact-match Easter recipes adhering to Low-Glycemic Index Diet for 10 people are returned.
---

### TC-P-15: Verify recipe search for Easter occasion, Vegetarian Diet, 1 person, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Easter; Diet Types: Vegetarian Diet; Number of People: 1; Full Matched: OFF

**Execution Steps:**
1. Set Pantry dropdowns to 'None'.
2. Set 'Full Matched' to OFF.
3. Select 'Easter' from Special Occasion.
4. Set 'Number of People' to 1.
5. Check 'Vegetarian Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search is executed successfully.
- Easter recipes matching Vegetarian Diet for 1 person are displayed.
---

### TC-P-16: Verify recipe search for Birthday occasion, Gastritis-Friendly Diet, 100 people, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Birthday; Diet Types: Gastritis-Friendly Diet; Number of People: 100; Full Matched: OFF

**Execution Steps:**
1. Set Pantry dropdowns to 'None'.
2. Set 'Full Matched' to OFF.
3. Select 'Birthday' from Special Occasion.
4. Set 'Number of People' to 100.
5. Check 'Gastritis-Friendly Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search request completes successfully.
- Recipes for Birthday with Gastritis-Friendly Diet for 100 people are displayed.
---

### TC-P-17: Verify recipe search for Christmas occasion, Gastritis-Friendly Diet, 100 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Christmas; Diet Types: Gastritis-Friendly Diet; Number of People: 100; Full Matched: ON

**Execution Steps:**
1. Leave Pantry items as 'None'.
2. Enable 'Full Matched' (ON).
3. Select 'Christmas' from Special Occasion.
4. Set 'Number of People' to 100.
5. Check 'Gastritis-Friendly Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search completes successfully.
- System displays exact matching Christmas recipes suitable for Gastritis-Friendly Diet serving 100 people.
---

### TC-P-18: Verify recipe search for Christmas occasion, Vegetarian Diet, 10 people, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Christmas; Diet Types: Vegetarian Diet; Number of People: 10; Full Matched: OFF

**Execution Steps:**
1. Keep Pantry dropdowns as 'None'.
2. Keep 'Full Matched' OFF.
3. Select 'Christmas' from Special Occasion.
4. Set 'Number of People' to 10.
5. Check 'Vegetarian Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search executes successfully.
- Results display Christmas recipes for Vegetarian Diet serving 10 people.
---

### TC-P-19: Verify recipe search with default occasion, Gastritis-Friendly Diet, 1 person, and Full Matched OFF
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None; Diet Types: Gastritis-Friendly Diet; Number of People: 1; Full Matched: OFF

**Execution Steps:**
1. Keep Pantry as 'None'.
2. Keep Special Occasion as 'None'.
3. Keep 'Full Matched' OFF.
4. Set 'Number of People' to 1.
5. Select 'Gastritis-Friendly Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search finishes successfully.
- System displays Gastritis-Friendly recipes for 1 person.
---

### TC-P-20: Verify recipe search with default occasion, no diet types, 100 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None; Diet Types: None; Number of People: 100; Full Matched: ON

**Execution Steps:**
1. Keep Pantry as 'None'.
2. Keep Special Occasion as 'None'.
3. Toggle 'Full Matched' to ON.
4. Set 'Number of People' to 100.
5. Uncheck all Diet Types.
6. Click 'Find Recipes'.

**Expected Results:**
- Search executes successfully.
- Recipes catering to 100 people with full match matching criteria are displayed.
---

### TC-P-21: Verify recipe search for Easter occasion, all diet types checked, 1 person, and Full Matched ON
- **Priority**: High | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Easter; Diet Types: Low-Glycemic Index Diet, Vegetarian Diet, Gastritis-Friendly Diet; Number of People: 1; Full Matched: ON

**Execution Steps:**
1. Set Pantry options to 'None'.
2. Enable 'Full Matched' (ON).
3. Select 'Easter' from Special Occasion.
4. Set 'Number of People' to 1.
5. Check all three Diet Types checkboxes.
6. Click 'Find Recipes'.

**Expected Results:**
- Search processes successfully.
- Displays recipes matching Easter for 1 person that fulfill all three diet restrictions.
---

### TC-P-22: Verify recipe search for Birthday occasion, all diet types checked, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Birthday; Diet Types: Low-Glycemic Index Diet, Vegetarian Diet, Gastritis-Friendly Diet; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Set Pantry options to 'None'.
2. Turn ON 'Full Matched'.
3. Select 'Birthday' from Special Occasion.
4. Set 'Number of People' to 10.
5. Check all Diet Types checkboxes.
6. Click 'Find Recipes'.

**Expected Results:**
- Search completes successfully.
- Shows fully matched Birthday recipes meeting all three diet preferences for 10 people.
---

### TC-P-23: Verify recipe search for Christmas occasion, no diet types, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Christmas; Diet Types: None; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Keep Pantry options as 'None'.
2. Enable 'Full Matched' switch (ON).
3. Select 'Christmas' from Special Occasion.
4. Set 'Number of People' to 10.
5. Keep all Diet Types unchecked.
6. Click 'Find Recipes'.

**Expected Results:**
- Search is executed successfully.
- System displays Christmas recipes tailored for 10 people.
---

### TC-P-24: Verify recipe search for Easter occasion, Gastritis-Friendly Diet, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: Easter; Diet Types: Gastritis-Friendly Diet; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Leave Pantry items as 'None'.
2. Set 'Full Matched' to ON.
3. Select 'Easter' from Special Occasion.
4. Set 'Number of People' to 10.
5. Check 'Gastritis-Friendly Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search request completes successfully.
- Returns exact match Easter recipes conforming to Gastritis-Friendly Diet for 10 people.
---

### TC-P-25: Verify recipe search for New Year occasion, Gastritis-Friendly Diet, 10 people, and Full Matched ON
- **Priority**: Medium | **Traceability**: REQ-SEARCH-01

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: New Year; Diet Types: Gastritis-Friendly Diet; Number of People: 10; Full Matched: ON

**Execution Steps:**
1. Keep Pantry dropdowns as 'None'.
2. Set 'Full Matched' to ON.
3. Select 'New Year' from Special Occasion.
4. Set 'Number of People' to 10.
5. Select 'Gastritis-Friendly Diet'.
6. Click 'Find Recipes'.

**Expected Results:**
- Search completes successfully.
- System displays exact matching recipes for New Year with Gastritis-Friendly Diet for 10 people.
---

### TC-N-26: Verify system validation when Number of People exceeds maximum limit (101 people)
- **Priority**: High | **Traceability**: REQ-SEARCH-02

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None (default); Diet Types: None (default); Number of People: 101; Full Matched: OFF (default)

**Execution Steps:**
1. Retain default form values for Pantry, Special Occasion, Full Matched, and Diet Types.
2. Enter or select '101' in 'Number of People'.
3. Click 'Find Recipes' button.

**Expected Results:**
- Search is not performed.
- An appropriate validation error message is displayed (e.g., 'Number of people must be between 1 and 100').
---

### TC-N-27: Verify system validation when Number of People is set below minimum limit (0 people)
- **Priority**: High | **Traceability**: REQ-SEARCH-02

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None (default); Diet Types: None (default); Number of People: 0; Full Matched: OFF (default)

**Execution Steps:**
1. Retain default form values for Pantry, Special Occasion, Full Matched, and Diet Types.
2. Enter or select '0' in 'Number of People'.
3. Click 'Find Recipes' button.

**Expected Results:**
- Search is not performed.
- An error message appears stating that Number of People must be at least 1.
---

### TC-N-28: Verify system validation when mandatory field 'Number of People' is left empty
- **Priority**: High | **Traceability**: REQ-SEARCH-02

**Preconditions:**
1. User is on the 'Your Recipes for Today' page.

**Test Data:**
Pantry: None; Special Occasion: None; Diet Types: None; Number of People: EMPTY; Full Matched: OFF

**Execution Steps:**
1. Ensure Pantry items are 'None'.
2. Set Special Occasion to 'None'.
3. Leave all Diet Types unchecked.
4. Leave 'Number of People' field empty/unselected.
5. Click 'Find Recipes' button.

**Expected Results:**
- Search is not performed.
- Validation error is triggered highlighting 'Number of People' as a required field.
---
