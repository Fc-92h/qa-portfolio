# Test Cases: BDO Patch Notifier & Automated Monitor

## Project Overview

**Project:** BDO Patch Notifier & Automated Monitor  
**Platform:** Make (Integromat)  
**Source:** Black Desert Online Global Lab news page  
**Destination:** Lolka  

**Purpose:** Automatically check the source website according to a schedule, detect new publications, identify them using `boardNo`, prevent duplicate notifications, and send new publication links to Lolka.

## Test Cases

### TC-001: Send a Notification for a New Publication

**Preconditions:**
- A new publication is available on the source website.
- The publication has not been processed before.

**Steps:**
1. Wait for the scheduled scenario execution.
2. Check the messages received in Lolka.
3. Open the notification link and verify the publication.

**Expected Result:**
- A new publication is detected during a scheduled check.
- A notification containing a link to the publication is sent to Lolka.

**Actual Result:**
- Notifications containing links to publications were received in Lolka.

**Status:** Pass

---

### TC-002: Prevent Duplicate Notifications

**Preconditions:**
- A publication has already been processed.
- Duplicate notifications were observed before the duplicate-checking logic was added.

**Steps:**
1. Run the scenario after implementing the duplicate-checking logic.
2. Observe whether the same publication is sent repeatedly.
3. Check the notifications received in Lolka.

**Expected Result:**
- Previously processed publications do not generate duplicate notifications.

**Actual Result:**
- Duplicate notifications were observed before the fix. After the duplicate-checking logic was added, repeated notifications stopped in the cases checked.

**Status:** Pass

---

### TC-003: Identify Publications Using `boardNo`

**Preconditions:**
- Publications are available on the source website.
- Notification links contain the `boardNo` parameter.

**Steps:**
1. Check the notification links received in Lolka.
2. Compare the `boardNo` values in the links.
3. Open the links and verify that they lead to the corresponding publications on the source website.

**Expected Result:**
- Links lead to the corresponding source publications.
- Different publications have different `boardNo` values.

**Actual Result:**
- Notification links contained different `boardNo` values and led to different publications on the source website.

**Status:** Pass

---

### TC-004: Skip an Already Processed Publication

**Preconditions:**
- A publication has already been processed.

**Steps:**
1. Allow the scheduled scenario to check the source website again.
2. Observe whether the same publication generates another notification.
3. Check the notifications received in Lolka.

**Expected Result:**
- The previously processed publication is skipped.
- No duplicate notification is sent.

**Actual Result:**
- Repeated notifications stopped after the duplicate-checking logic was added. The internal Data Store lookup was not verified separately.

**Status:** Pass

---

### TC-005: Handle the Absence of New Publications

**Preconditions:**
- All available publications have already been processed.
- Their identifiers are stored in the Make Data Store.

**Steps:**
1. Allow the scenario to execute according to its schedule.
2. Check whether any new publications are available.
3. Check the messages received in Lolka.

**Expected Result:**
- Previously processed publications are skipped.
- No duplicate notifications are sent when no new publications are available.

**Actual Result:**
- The automation uses stored publication identifiers to identify previously processed news and prevent duplicate notifications.

**Status:** Pass

---

### TC-006: Verify Notification Content and Links

**Preconditions:**
- Notifications for different publications are available in Lolka.

**Steps:**
1. Open the notifications in Lolka.
2. Compare the publication links and available content with the source website.
3. Verify that the links lead to the corresponding articles.

**Expected Result:**
- Notifications refer to the correct publications.
- Links lead to the corresponding source articles.

**Actual Result:**
- Notifications contained different publication descriptions and links to different articles on the source website.

**Status:** Pass

---

### TC-007: Process Multiple New Publications

**Preconditions:**
- At least two new publications are available on the source website before a scheduled check.

**Steps:**
1. Allow the scenario to execute while multiple new publications are available.
2. Check which publications are sent to Lolka.
3. Verify that duplicate notifications are not generated.

**Expected Result:**
- New publications supported by the scenario are processed according to its configuration.
- Duplicate notifications are not generated.

**Actual Result:**
- Not recorded. Processing multiple new publications during one scheduled execution has not been tested separately.

**Status:** Not Run

---

### TC-008: Handle Source Data Retrieval Failure

**Preconditions:**
- A safe test setup is available to simulate a failed request to the source website.

**Steps:**
1. Simulate a source data retrieval failure.
2. Run the scenario.
3. Check the execution result and messages received in Lolka.

**Expected Result:**
- The failure is handled or reported appropriately.
- No misleading notification is sent.

**Actual Result:**
- Not recorded. Source data retrieval failure has not been tested.

**Status:** Not Run

---

## Test Execution Summary

| Test Case | Description | Status |
|---|---|---|
| TC-001 | Send a notification for a new publication | Pass |
| TC-002 | Prevent duplicate notifications | Pass |
| TC-003 | Identify publications using `boardNo` | Pass |
| TC-004 | Skip an already processed publication | Pass |
| TC-005 | Handle the absence of new publications | Pass |
| TC-006 | Verify notification content and links | Pass |
| TC-007 | Process multiple new publications | Not Run |
| TC-008 | Handle source data retrieval failure | Not Run |

## Notes

- **Pass:** The expected result was observed or supported by the behavior checked during testing.
- **Fail:** The observed result differed from the expected result.
- **Not Run:** The test case has not been executed or its result has not been verified.
- The automation checks the source website according to its configured schedule. A new publication may be detected during the next scheduled check rather than immediately when it appears.
- The Make Data Store is used to identify previously processed publications and prevent duplicate notifications.
- Multiple-publication processing and source data retrieval failure have not been tested separately.
