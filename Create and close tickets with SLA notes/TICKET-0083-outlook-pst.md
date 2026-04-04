# Help Desk Ticket #0083

**Category:** Microsoft 365 — Outlook PST Corruption and Send Receive Failure
**Priority:** P2 High
**Status:** Closed

---

## Ticket Details

| Field | Value |
|---|---|
| Ticket ID | TKT-0083 |
| Date Opened | April 7, 2026 — 08:47 |
| Date Closed | April 7, 2026 — 11:23 |
| Total Resolution Time | 2 hours 36 minutes |
| SLA Response Target | 1 hour (P2 High) |
| SLA Resolve Target | 8 hours (P2 High) |
| First Response Sent | 08:52 (5 minutes after intake) |
| SLA Response Status | Met |
| SLA Resolve Status | Met |
| Assigned To | Nnamso Mkpong — IT Support L1 |
| Affected User | Adaeze Nwosu |
| Department | Legal |
| Machine | WIN11-AN-04 |
| Application | Microsoft Outlook (Microsoft 365 version) |
| Impact | Single user — no email access, no workaround |
| Urgency | High — Legal department, time-sensitive casework |

---

## Issue Reported

User reports that Outlook is not sending or receiving emails. The error message shown is "The operation failed. An object could not be found." When Outlook opens, it immediately prompts for a data file that it cannot locate. The user states she was working normally on Friday April 4 and the issue appeared this morning. She has not intentionally changed any settings.

The user is in the Legal department. Email access is critical to her role and there is no alternative communication channel available to her that is acceptable for client-facing correspondence.

---

## First Response Note

**Sent at:** 08:52 | **Sent to:** adaeze.nwosu@company.com

> Good morning Adaeze,
>
> Thank you for reporting this. I have opened ticket TKT-0083 and I am investigating the issue now.
>
> Based on the symptoms you have described — the missing data file prompt and the send receive failure — this appears to be a data file location issue in Outlook. This can occur after a Windows update changes profile paths or if the PST file has become detached from the profile.
>
> I am going to connect to your machine remotely in the next few minutes to investigate. Please keep your laptop on and Outlook open if possible. I will update this ticket with my findings as soon as I have assessed the situation.
>
> Your ticket is P2 High priority. Our target resolution time is 8 hours from this morning. I will aim to resolve this significantly sooner.
>
> Nnamso Mkpong — IT Support

---

## Investigation Log

**08:58 — Remote session established to WIN11-AN-04**

Connected via Remote Desktop. User present and has confirmed the machine state described in the ticket. Outlook is open and showing the profile load error.

**09:03 — Outlook error message captured**

Error on Outlook open: "Cannot start Microsoft Outlook. Cannot open the Outlook window. The set of folders cannot be opened. The file C:\Users\Adaeze.Nwosu\Documents\Outlook Files\Adaeze.pst is not found."

This confirms the PST file path is broken. The profile is pointing to a PST location that no longer contains the expected file.

**09:07 — File Explorer search for PST file**

Searched C:\Users\Adaeze.Nwosu\ for all files with the .pst extension. Found the following:

| File | Location | Size | Date Modified |
|---|---|---|---|
| Adaeze.pst | C:\Users\Adaeze.Nwosu\AppData\Local\Microsoft\Outlook\ | 2.3 GB | 4/4/2026 17:42 |
| Adaeze_old.pst | C:\Users\Adaeze.Nwosu\Documents\Outlook Files\ | 1.1 GB | 3/15/2026 09:10 |

The active PST file exists but has moved to a different location from the one the Outlook profile expects. The profile is pointing to the Documents path but the current file is in AppData\Local. This is consistent with a Windows Update redistributing user folders or a OneDrive sync event that moved the file without updating the Outlook profile reference.

**09:14 — Outlook profile investigation**

Opened Control Panel → Mail → Show Profiles → Adaeze Nwosu profile → Data Files. Confirmed the profile references `C:\Users\Adaeze.Nwosu\Documents\Outlook Files\Adaeze.pst` — the old location.

**09:18 — Root cause confirmed**

The PST file was moved during a OneDrive sync event over the weekend. OneDrive attempted to sync the Documents\Outlook Files folder and in doing so moved the PST file to the local AppData location as part of a known-files protection action. The Outlook profile was not updated to reflect the new path. This is a documented behaviour when OneDrive known-folder protection is applied to a machine that has a locally stored PST file.

**Root cause:** OneDrive known-folder protection moved the PST file from Documents to AppData\Local. Outlook profile still references the old Documents path.

---

## Action Log

**09:22 — Profile data file path updated**

In Control Panel → Mail → Show Profiles → Adaeze Nwosu → Data Files, removed the broken reference to `C:\Users\Adaeze.Nwosu\Documents\Outlook Files\Adaeze.pst`. Added the correct PST file at `C:\Users\Adaeze.Nwosu\AppData\Local\Microsoft\Outlook\Adaeze.pst` as the default data file.

**09:25 — Outlook reopened**

Closed and reopened Outlook. Profile loaded without error. Outlook opened to the inbox. Send and receive initiated manually — completed successfully. 47 new emails downloaded including emails sent since Friday that had been queued.

**09:30 — PST integrity check**

With user's permission, ran the Outlook inbox repair tool (scanpst.exe) against the PST file to confirm no corruption from the move event. Scanpst located at `C:\Program Files\Microsoft Office\root\Office16\SCANPST.EXE`.

Scan result: No errors found. PST file integrity confirmed.

**09:45 — OneDrive configuration reviewed to prevent recurrence**

Navigated to OneDrive settings → Sync and Backup → Manage Backup. Confirmed that the Documents, Desktop, and Pictures folders are set for OneDrive backup (known-folder protection). PST files in these locations will be subject to future sync events.

Recommended action to prevent recurrence: Outlook PST files should not be stored in OneDrive-synced folders. Created a new folder at `C:\OutlookData\` (outside all OneDrive-managed paths) and moved the PST file to this location. Updated the Outlook profile data file path to `C:\OutlookData\Adaeze.pst`. Confirmed Outlook reopens correctly from the new location.

**10:05 — Confirmed with user**

User confirmed Outlook is working correctly. All emails present. Calendar and contacts intact. Sent a test email to herself — delivered successfully. No further errors reported.

---

## Escalation Assessment

**Escalation considered at:** 09:18 (after root cause confirmed)

**Escalation decision:** No escalation required. Root cause identified as a OneDrive path conflict with a locally stored PST file — a known issue with a documented resolution. Fix applied at first-line level. PST file integrity confirmed via scanpst with no errors found.

If scanpst had identified corruption, escalation to the Microsoft 365 team for mailbox data recovery would have been initiated.

---

## User Confirmation

**10:05 — User verbal confirmation during remote session:** "Yes, everything is back. I can see all my emails and it is sending fine. Thank you."

**10:08 — Written confirmation email sent to user:**

> Hi Adaeze,
>
> I am glad to confirm that Outlook is working correctly on your machine. Here is a brief summary of what was found and what was changed.
>
> The issue was caused by OneDrive moving your Outlook data file when it applied its folder backup protection over the weekend. The Outlook profile was still pointing to the old location, which caused the send and receive failure.
>
> I have updated the data file path in your Outlook profile and moved the data file to a location that OneDrive will not sync. This prevents the same issue from occurring again.
>
> If you experience any further issues with Outlook, please do not hesitate to raise a new ticket. I will be closing TKT-0083 now.
>
> Nnamso Mkpong — IT Support

**10:10 — User reply received:** "Perfect, thank you so much. All working."

---

## Closure Note

**Closed at:** 11:23 (administrative close after documentation completed)

**Root cause:** OneDrive known-folder protection moved the Outlook PST file from the Documents folder to AppData\Local during a weekend sync event. The Outlook profile data file reference was not updated, causing Outlook to be unable to locate the PST file on the next launch.

**Resolution:** Updated Outlook profile data file path to reference the new PST location. Ran scanpst.exe — no corruption found. Moved PST file to C:\OutlookData\ (outside OneDrive sync scope) to prevent recurrence. Updated profile reference to new location. Confirmed Outlook opens and send and receive function correctly.

**User confirmation:** Verbal and written confirmation received at 10:10.

**Preventive action taken:** PST file relocated to a non-OneDrive path. Outlook profile updated. User advised that PST files must not be stored in OneDrive-managed folders (Documents, Desktop, Pictures).

**Preventive recommendation raised:** Submitted an advisory to the IT team lead recommending that a group policy or OneDrive administrative template be applied to exclude PST files from OneDrive sync on all managed machines. This is a documented Microsoft-recommended configuration.

**SLA performance:**

| Metric | Target | Actual | Status |
|---|---|---|---|
| First response | 1 hour | 5 minutes | Met |
| Resolution | 8 hours | 2 hours 36 minutes | Met |

No SLA breach. No data loss. No escalation required.

---

## Validation Evidence

No screenshots were captured for this ticket as it was conducted via a remote session. The following evidence exists within the ticket log:

Evidence item one: First response timestamp of 08:52 — 5 minutes after ticket intake — confirmed within P2 SLA response window.

Evidence item two: PST file path conflict confirmed in Control Panel → Mail → Show Profiles at 09:14.

Evidence item three: Root cause confirmed as OneDrive known-folder protection at 09:18 with the two PST file locations recorded.

Evidence item four: Scanpst.exe result at 09:30 — no corruption found.

Evidence item five: PST file moved to C:\OutlookData\ at 09:45. Outlook profile updated. Outlook reopens correctly.

Evidence item six: User written confirmation received at 10:10.

---

## Troubleshooting Logic

| Check | Location | Result |
|---|---|---|
| Outlook error message | Outlook on startup | "The file is not found" — PST path broken |
| PST file search | C:\Users\Adaeze.Nwosu\ recursive search | Found at AppData\Local — not at Documents path |
| Outlook profile data file reference | Control Panel → Mail → Data Files | Pointing to old Documents path |
| OneDrive sync scope | OneDrive settings → Sync and Backup | Documents folder backed up — included PST file |
| PST file integrity | scanpst.exe | No corruption found |
| Fix applied | Profile path updated, PST moved to C:\OutlookData\ | Outlook opens and functions correctly |
| Root cause | OneDrive moved PST during known-folder sync | Confirmed |
| Resolution | Profile updated, PST relocated outside OneDrive scope | Confirmed by user at 10:10 |

---

## Ticket Closure Declaration

TKT-0083 closed with full resolution. Outlook PST path conflict resolved on WIN11-AN-04. No data loss. No escalation required. SLA met. User confirmed resolution in writing. Preventive action taken on machine and advisory raised to IT team lead.

**Documented by:**
Nnamso Mkpong
IT Support Portfolio
