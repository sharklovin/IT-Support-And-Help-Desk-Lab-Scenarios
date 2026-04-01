# Help Desk Ticket #0056

**Category:** Microsoft 365 — OneDrive Sync Failure
**Priority:** Standard
**Status:** Resolved

---

## Ticket Details

| Field | Value |
|------|------|
| Ticket ID | 0056 |
| Date Opened | April 2026 |
| Date Resolved | April 2026 |
| Assigned To | Nnamso Mkpong — IT Support |
| Machine | WIN11_CLIENT01 |
| OneDrive Account | Nnamso — Personal (Microsoft Account) |
| Affected Folder | Sync Test |
| Affected File | TestFile.txt |
| Root Cause | Sync paused — client not uploading changes |

---

## Issue Reported

User reported that files saved to the OneDrive folder on their desktop were not appearing on their other devices or in the OneDrive browser interface. Files were being saved as normal but the cloud version was not updating. The user was concerned that their work may have been lost.

---

## Investigation

**Baseline check performed before fault simulation:**

1. Opened File Explorer and navigated to OneDrive root.
2. Confirmed breadcrumb showed **OneDrive** — client signed in and healthy.
3. Created test folder **Sync Test** — green tick confirmed within seconds.
4. Created **TestFile.txt** inside Sync Test — green tick confirmed, file visible in cloud.
5. Baseline confirmed: sync running normally.

**Fault simulation:**

6. Right-clicked OneDrive system tray icon and selected **Pause syncing**.
7. Breadcrumb changed from **OneDrive** to **Paused** — sync suspended confirmed.
8. Sync Test folder lost its status icon — no sync activity occurring.
9. Modified TestFile.txt and saved — file showed **sync pending** spinner icon.
10. Cloud version of TestFile.txt was not updated during paused state.

**Root Cause Identified:**

OneDrive sync was paused. The client was signed in and the account was healthy. No storage quota issue, no authentication failure, no network fault. The sync client had been suspended, either by the user accidentally selecting the pause option or by an automatic pause triggered by a metered connection or policy. All files were safe locally and queued for upload.

---

## Actions Taken

1. Confirmed OneDrive account was signed in and baseline sync was healthy.
2. Created Sync Test folder and TestFile.txt to establish a controlled test state.
3. Paused sync deliberately to reproduce the reported fault state.
4. Confirmed breadcrumb changed to Paused and TestFile showed sync pending icon.
5. Right-clicked OneDrive system tray icon and selected **Resume syncing**.
6. Confirmed breadcrumb returned to **OneDrive**.
7. Confirmed Sync Test folder showed green tick.
8. Confirmed TestFile.txt showed green tick and timestamp updated.
9. Verified file would now be accessible from cloud and other signed-in devices.

---

## User Communication Note

The user was advised that their files were not lost. Files saved to the OneDrive folder while sync was paused exist safely on the local machine and were queued for upload. Once sync was resumed, all pending changes uploaded successfully. The user was asked to check their other devices to confirm the files were now visible, and to contact the helpdesk if sync paused again unexpectedly.

---

## Outcome

Sync restored on WIN11_CLIENT01. All files in the Sync Test folder confirmed synced to the cloud with green tick status. No data loss occurred. Files that had been modified during the paused state uploaded successfully on sync resumption.

No changes were required to:

- OneDrive account credentials
- Network configuration
- Storage quota
- Licence or tenant settings

Root cause was confirmed as **sync paused** at the client level.

---

## Validation Evidence

- Breadcrumb confirmed healthy OneDrive state at baseline
- Green tick on Sync Test folder and TestFile.txt confirmed before pause
- Breadcrumb confirmed Paused after suspension
- Sync pending icon on TestFile confirmed changes queued but not uploading
- Breadcrumb returned to OneDrive after resuming
- Green tick on Sync Test folder confirmed folder sync healthy
- Green tick on TestFile.txt with updated timestamp confirmed file upload complete

---

## Troubleshooting Logic

| Check | Result |
|------|------|
| OneDrive signed in | Pass |
| Breadcrumb healthy at baseline | Pass |
| Test folder and file created | Pass |
| Sync paused — breadcrumb shows Paused | Confirmed fault state |
| File modified while paused — shows sync pending icon | Confirmed pending upload |
| Resume syncing selected | Pass |
| Breadcrumb restored to OneDrive | Pass |
| Folder green tick restored | Pass |
| File green tick and timestamp confirmed | Pass |
| Root cause | Sync paused |
| Resolution | Resume sync via system tray |

---

## Escalation Notes

This ticket was resolved at first line. If sync had not resumed after the above steps, the following escalation paths would apply:

| Scenario | Next Step |
|------|------|
| Account signed out or token expired | User re-signs in; coordinate with identity team if MFA blocks the session |
| Storage quota exceeded | Raise with IT admin to review licence storage allocation |
| Sync client error persists after resume | Unlink and relink the account; escalate if reinstall is needed |
| Policy preventing sync on managed device | Escalate to endpoint management team to review Intune or Group Policy settings |

---

## Real World Relevance

OneDrive sync complaints are among the most common Microsoft 365 tickets. The typical pattern is that a user pauses sync, forgets they did it, and raises a ticket when files are not appearing on their other devices. The resolution is fast once the technician knows to check the breadcrumb and the system tray icon before investigating anything more complex. Communicating clearly to the user that their files are not lost is equally important to resolving the technical problem quickly.

---

## Ticket Closure Note

OneDrive sync restored for affected user on WIN11_CLIENT01. Root cause identified as sync paused at the client level. Resolved by resuming sync via the system tray icon. All pending file changes uploaded successfully. No data loss, no infrastructure changes required. Ticket closed.

**Documented by:**
Nnamso Mkpong
IT Support Portfolio
