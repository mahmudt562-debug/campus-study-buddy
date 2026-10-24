
# Campus Study Buddy – Add Assignment Specification

## Steps 5–6: Rules and Concrete Examples

### R1: Assignment Title
Remove extra spaces from the title. The title cannot be empty.

- "Biology quiz" → Accepted.
- " " → Rejected.
- "A" → Accepted (one-character boundary).

### R2: Course Selection
A student must select an existing course before saving an assignment.

- Course "BY163" selected → Accepted.
- No course selected → Rejected.

### R3: Due Date
The due date is required and must be a valid date in YYYY-MM-DD format.

- 2026-11-30 → Accepted.
- 2026-11-31 → Rejected (invalid date).
- Empty date → Rejected.

### R4: Validation
If required information is missing or invalid, show an error for each invalid field and do not save.

- Title "A", course "BY163", date 2026-11-30 → Assignment saved.
- Title empty and date empty → Not saved; two errors displayed.

### R5: Required-Field Messages
Show a specific error message when a required field is missing.

- Empty title → "Title is required."
- Empty date → "Due date is required."
- No course → "Please select a course."

### R6: Successful Save
After a successful save, show a confirmation and add the assignment to the list immediately.

- Save "Biology quiz" with a valid course and date → One assignment appears with confirmation.
- Save with an empty title → No assignment is added.

### R7: Error Placement
If an assignment has missing or invalid information, show the error message below the corresponding field.

- Empty title → "Title is required." appears below the title field.
- Title "A" → No title error appears.

### R8: Form After Saving
After a successful save, clear the assignment form and show the new assignment in the list.

- Save "Biology quiz" with a valid course and date → Form clears and assignment appears in the list.
- Save with an empty title → Form stays unchanged and no assignment is added.

## Step 7: Acceptance Criteria

### A1-AC1: Successful Save
- Given: Existing course BY163 is selected, title "Biology quiz", due date 2026-11-30.
- When: Student chooses Save.
- Then: One assignment is saved under BY163 and confirmation is displayed.
- Traces to: REQ-2; UC-1 main flow.

### A1-AC2: Missing Title
- Given: BY163 is selected, title is blank, due date 2026-11-30.
- When: Student chooses Save.
- Then: No assignment is saved and a title-required error is displayed.
- Traces to: REQ-5; UC-1 alternative.

### A1-AC3: Missing Due Date
- Given: BY163 is selected, title "Biology quiz", due date is blank.
- When: Student chooses Save.
- Then: No assignment is saved and a due-date-required error is displayed.
- Traces to: REQ-5; UC-1 alternative.

### A1-AC4: Missing Course
- Given: No course is selected, title "Biology quiz", due date 2026-11-30.
- When: Student chooses Save.
- Then: No assignment is saved and a course-required error is displayed.
- Traces to: REQ-2; added UC-1 alternative.

### A1-AC5: Invalid Due Date
- Given: BY163 is selected, title "Biology quiz", due date 2026-11-31.
- When: Student chooses Save.
- Then: No assignment is saved and an invalid-date error is displayed.
- Traces to: REQ-2; added UC-1 alternative.

## Step 8: Pure JavaScript Function Interfaces

`validateAssignment(title, course, dueDate, courses) → {valid, errors}`

`isValidDate(dueDate) → true or false`

`isExistingCourse(course, courses) → true or false`

These functions perform validation without accessing the DOM or storage.

## Step 9: Test Cases

| AC ID | Input | Expected Result |
|---|---|---|
| A1-AC2 | `validateAssignment("", "BY163", "2026-11-30", ["BY163"])` | Invalid; title-required error (0-character boundary). |
| A1-AC1 | `validateAssignment("A", "BY163", "2026-11-30", ["BY163"])` | Valid; no errors (1-character boundary). |
| A1-AC1 | `validateAssignment("Biology quiz", "BY163", "2026-11-30", ["BY163"])` | Valid; no errors (ordinary case). |
| A1-AC5 | `validateAssignment("Biology quiz", "BY163", "2026-11-31", ["BY163"])` | Invalid; invalid-date error. |
| A1-AC4 | `validateAssignment("Biology quiz", "", "2026-11-30", ["BY163"])` | Invalid; course-required error. |
