# Lab 11: Remote Support Session Workflow

> **Author:** Nnamso Mkpong
>
> **Domain:** Remote Assistance — Help Desk Support Workflow
>
> **Environment:** Windows 11 Client, Quick Assist (built-in Windows tool)
> **Completed:** April 2026

---

## Objective

Run a complete, documented remote support session using Quick Assist, diagnose a software installation failure on the remote machine, resolve it by obtaining a clean installer from the official source, and close the session with a full ticket trail from open to resolution.

---

## Business Scenario

> **Ticket #2026-04-01-001 | Remote Application Installation Failure**
>
> Elisha Ibanga, a remote employee, reports that they cannot install an application on their machine. The installer is failing with an error message and they have already attempted the installation twice without success. The issue is blocking them from completing a shift-critical task. IT support has been asked to connect remotely, investigate the failure, fix it, and confirm the application is working before closing the session.

This scenario covers a complete first-line remote support workflow: creating the ticket, establishing the remote session, verifying the fault, identifying the root cause, applying the fix, confirming with the user, and closing cleanly with documentation. Every step produces evidence that appears in the ticket trail.

---

## Environment and Tools Used

| Component | Detail |
|---|---|
| **Technician Machine** | Windows 11 — Nnamso Mkpong (Technician) |
| **Remote User Machine** | Windows 11 — Elisha Ibanga (User) |
| **Remote Tool** | Quick Assist (built into Windows 11) |
| **Ticket Logged In** | Notepad (simulating a ticketing system) |
| **Ticket Number** | 2026-04-01-001 |
| **Application Being Installed** | 7-Zip (used to replicate the access denied install scenario) |
| **Root Cause** | Corrupted installer file — NSIS Error |
| **Fix Applied** | Clean installer downloaded from official source |

---

## Ticket Timeline

| Time | Event |
|---|---|
| 9:28 AM | Ticket opened — Elisha Ibanga reports installation failure with Access denied error |
| 9:32 AM | Technician opens Quick Assist and generates security code |
| 9:32 AM | User enters security code on their machine |
| 9:33 AM | User allows screen sharing — connection established |
| 9:35 AM | Technician verifies problem and adds investigation note to ticket |
| 9:38 AM | Corrupt installer identified — NSIS Error on the existing download |
| 9:45 AM | Technician navigates to official site and downloads clean installer on remote machine |
| 9:50 AM | Application installs successfully — user confirms it is working |
| 9:52 AM | Quick Assist session ended cleanly |
| 9:54 AM | Ticket updated with resolution note and closed |

---

## Steps Performed

---

### Phase 1 — Create the Ticket

**Step 1.1 — Log the Initial Ticket**

Before connecting to the remote machine, the ticket is created with all required fields: ticket number, status, priority, user, issue description, time opened, and a brief description of what the user has reported.

<img width="947" alt="Ticket 2026-04-01-001 showing user Elisha Ibanga, priority High, issue cannot install Adobe Reader" src="screenshots/01-ticket-created-initial.png" />

> Creating the ticket before the session begins is standard practice. It establishes the start time, captures the user's own description of the problem before any investigation begins, and creates a record that exists independently of the technician's memory. If the session is interrupted or handed over, another technician can pick up from the ticket without losing context.

---

### Phase 2 — Establish the Remote Session

**Step 2.1 — Generate a Security Code in Quick Assist (Technician Side)**

Open **Quick Assist** on the technician machine and click **Help someone**. After signing in with a Microsoft account, Quick Assist generates a six-character security code that expires within ten minutes. Share this code with the user verbally, via chat, or via the ticket.

<img width="459" alt="Quick Assist on technician side showing security code TL4C45 with expiry countdown" src="screenshots/02-quick-assist-tech-security-code.png" />

> The code is time-limited for security. If the user does not enter it before expiry, a new code must be generated. In a real support environment this code would be communicated over a verified channel — typically the same phone call or chat the ticket was raised through — to ensure the user knows who is connecting to their machine.

---

**Step 2.2 — User Enters the Security Code (User Side)**

On the user's machine, Quick Assist opens to the **Get help** screen. The user types the security code provided by the technician and clicks **Submit**.

<img width="461" alt="Quick Assist on user side showing security code TL4C45 entered in the Get help field" src="screenshots/03-quick-assist-user-enters-code.png" />

---

**Step 2.3 — User Allows Screen Sharing**

Quick Assist presents the user with an Allow screen sharing confirmation. The user ticks the security acknowledgement checkbox and clicks **Allow**.

<img width="459" alt="Quick Assist Allow screen sharing dialog with Nnamso M. shown and Allow button" src="screenshots/04-user-allows-screen-sharing.png" />

> The security warning on this screen is intentional and important. It reminds the user that they should only allow connections from people they trust and who contacted them through a verified channel. In a corporate environment, the IT department would train users to expect this dialog and to verify the technician's name before clicking Allow.

---

**Step 2.4 — Connection Established: Technician View**

The technician's Quick Assist window now shows the remote desktop. The user mode shows **Administrator**, confirming the session has elevated rights. The remote screen is fully visible inside the Quick Assist frame with a yellow border.

<img width="1364" alt="Quick Assist technician view showing remote desktop fully visible with User mode Administrator" src="screenshots/05-remote-connection-tech-view.png" />

> ✅ The yellow border around the remote desktop confirms the session is live. The toolbar at the top gives the technician options to annotate, chat, switch monitors, pause, and request full control. User mode Administrator is critical for software installation work — without it, the installer may fail before the technician can diagnose the real cause.

---

**Step 2.5 — Connection Confirmed: Client View**

On the user's machine, a Quick Assist banner appears at the top of the screen reading **Screen sharing on**, confirming to the user that the session is active. The user can end the session at any time using the Leave button.

<img width="1018" alt="User machine showing Quick Assist Screen sharing on banner at top of screen" src="screenshots/06-client-side-screen-sharing-confirmed.png" />

---

### Phase 3 — Investigate the Fault

**Step 3.1 — Add Investigation Note to the Ticket**

With the session active and the problem confirmed on screen, the technician updates the ticket with an investigation note including the timestamp, what was observed, and the user's exact description of the error.

<img width="947" alt="Ticket updated with 9:35 AM investigation note confirming Access denied error observed" src="screenshots/07-ticket-notes-updated-mid-session.png" />

> Updating the ticket during the session, not after it, is a professional habit. If the call drops or the technician needs to escalate mid-investigation, the record is already there. Timestamps matter — they show how long each stage of the investigation took and support SLA reporting.

---

**Step 3.2 — Identify the Root Cause: NSIS Error**

On the remote machine, the technician navigates to the Downloads folder and attempts to run the installer the user had been using. The installer returns an **NSIS Error**: the installer file is corrupted or incomplete.

<img width="1364" alt="NSIS Error dialog on remote machine showing installer is corrupted or incomplete" src="screenshots/08-nsis-installer-error-corrupt-file.png" />

> ❌ The NSIS Error confirms the installer file itself is the problem, not the user's permissions or UAC settings. This rules out the Access denied description the user gave — they were reading a different error, or the NSIS error preceded the access denied message. The fix is to obtain a clean copy of the installer from a verified source.

> This is an important diagnostic moment. The temptation is to try running the installer as admin, checking UAC, or disabling antivirus. None of those would fix a corrupt file. Correctly identifying the root cause as a bad download prevents wasted time and additional risk.

---

### Phase 4 — Fix the Issue

**Step 4.1 — Download a Clean Installer from the Official Source**

While still connected via Quick Assist, the technician opens the browser on the remote machine and navigates to the official download page at **7-zip.org**. The correct 64-bit Windows installer is downloaded directly to the remote machine.

<img width="1365" alt="Official 7-zip.org download page on remote machine with clean installer downloading" src="screenshots/09-clean-installer-downloaded-official-site.png" />

> Downloading from the official vendor site on the remote machine means the clean file goes directly where it is needed without file transfer steps. The technician confirms the URL in the address bar before downloading to ensure the source is legitimate. This matters from both a security and an audit perspective — a technician should never install software from an unverified source on a user's machine.

---

**Step 4.2 — Install the Application and Confirm It Works**

The clean installer runs without errors. The application installs successfully and opens on the remote machine, confirming it is fully functional.

<img width="753" alt="7-Zip application installed and open on the remote machine showing file manager" src="screenshots/10-application-installed-and-working.png" />

> ✅ 7-Zip opens and the file manager interface loads correctly. The installation completed without errors. The technician confirms with the user verbally that the application is working as expected before ending the session.

---

### Phase 5 — End the Session and Close the Ticket

**Step 5.1 — End the Quick Assist Session**

Once the user confirms the application is working, the technician ends the Quick Assist session. Quick Assist shows the **Screen sharing has ended** confirmation on the technician side.

<img width="1365" alt="Quick Assist showing Screen sharing has ended confirmation after session closed" src="screenshots/11-quick-assist-session-ended.png" />

> Ending the session clearly and confirming it with the user is part of the professional workflow. The user should know the technician has left their machine. Leaving a session running after the work is done is a security risk and a professional lapse.

---

**Step 5.2 — Update and Close the Ticket**

Return to the ticket and add the resolution note with timestamp, root cause confirmed, action taken, and user confirmation. Change the status from Open to Resolved and record the close time.

See `TICKET-2026-04-01-001.md` for the complete ticket trail.

---

## Help Desk Ticket Note

See `TICKET-2026-04-01-001.md` in this folder.

---

## Outcome and Validation

| Check | Result |
|---|---|
| Ticket created with all required fields before session started | Pass |
| Quick Assist security code generated on technician machine | Pass |
| User entered code and allowed screen sharing | Pass |
| Remote desktop visible on technician machine with Administrator mode | Pass |
| User machine confirmed Screen sharing on banner | Pass |
| Investigation note added to ticket during session at 9:35 AM | Pass |
| NSIS Error confirmed — corrupt installer identified as root cause | Pass |
| Clean installer downloaded from official vendor site on remote machine | Pass |
| Application installed and opened successfully | Pass |
| User confirmed application working before session ended | Pass |
| Quick Assist session ended cleanly | Pass |
| Ticket updated with resolution note and closed | Pass |

---

## What I Learned

1. **The ticket should be open before the session starts.** Creating the ticket first establishes the start time, captures the user's description of the problem before any investigation, and ensures there is a record even if the session ends unexpectedly. A ticket without a start time is missing a piece of evidence.

2. **Investigate the actual error before trying fixes.** The user described the problem as Access denied. The real cause was a corrupt installer file producing an NSIS Error. Attempting UAC fixes or admin launches would have wasted time. Reading the actual error message and understanding what it means determines the correct next step.

3. **Always download from the official source.** Using a clean copy from the vendor's official site is the only acceptable approach when an installer is corrupt. Downloading from third-party sites introduces security risk and is not something a professional technician should do on a user's machine.

4. **Update the ticket during the session, not after.** Investigation notes with timestamps should be added as the session progresses. This protects the technician if the call drops, documents the timeline accurately, and shows professional habits to anyone reviewing the ticket.

5. **End the session clearly and confirm with the user.** The user must know when the technician has left their machine. Confirming this verbally and then ending Quick Assist properly is the professional close. It is also a security requirement — remote sessions should not be left open after the work is done.

---

## Real World Relevance

Remote support is one of the most common delivery mechanisms for IT help desk work in any organisation with distributed teams, remote workers, or multiple office locations. The ability to connect quickly, diagnose efficiently, and fix without requiring the user to be physically present is a core competency for anyone in a desktop support or first-line help desk role.

The scenario in this lab also demonstrates something important about user-reported symptoms. The user said they had an Access denied error. The actual fault was a corrupt installer file. This is extremely common in support work — users describe what they see in terms they understand, which is not always the technical description of the fault. A technician who takes the user's description at face value and starts checking permissions will waste time. A technician who reproduces the error themselves and reads it accurately will find the cause in minutes.

The ticket trail this lab produces — from open time through investigation notes to resolution and close — is the kind of documentation that makes a support operation auditable, improvable, and professional. In organisations with formal SLAs, this trail is not optional. It is how the team proves the ticket was handled correctly and within the agreed time frame.

---

## Troubleshooting Reference

| Symptom | Likely Cause | Resolution |
|---|---|---|
| NSIS Error on installer launch | Installer file corrupted during download | Delete the file and download a fresh copy from the official vendor site |
| Access denied during installation | Installer not running with admin rights | Right-click installer and select Run as administrator |
| Quick Assist code not accepted | Code has expired — 10 minute limit | Generate a new code in Quick Assist and share again |
| Remote desktop not visible after connection | User did not click Allow on the consent screen | Ask user to check for the Allow screen sharing prompt |
| Application installs but does not open | Conflicting old version or missing dependency | Check Apps and Features for an existing version; uninstall first if found |
| Session drops mid-investigation | Network interruption | Reconnect via Quick Assist with a new code; update ticket with interruption note |
| User cannot find Quick Assist | Search bar not returning results | Press Win + R and type quickassist; or open it from the Microsoft Store |
