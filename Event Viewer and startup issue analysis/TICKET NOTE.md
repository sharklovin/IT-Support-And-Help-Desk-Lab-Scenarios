# Help Desk Ticket #0061

**Category:** Windows 11 — Startup Performance and Login Crash
**Priority:** High — user unable to begin work at login
**Status:** Resolved — pending reboot verification

---

## Ticket Details

| Field | Value |
|---|---|
| Ticket ID | 0061 |
| Date Opened | April 3, 2026 |
| Date Resolved | April 3, 2026 |
| Assigned To | Nnamso Mkpong — IT Support |
| Machine | Shark007 |
| OS | Windows 11 |
| Tools Used | Task Manager Startup Apps, Event Viewer Application Log |
| Priority | High — login crash blocking start of shift |

---

## Issue Reported

User reports that their PC takes significantly longer than normal to boot and that an application crashes every morning at login. The issue began after a recent software installation. The user is unable to start their primary workflow until the crash is cleared, which requires a manual application relaunch after each login. The delay between power-on and a usable desktop is estimated by the user at several minutes.

---

## Investigation

**Startup Apps audit — Task Manager:**

1. Opened Task Manager → Startup Apps on machine Shark007.
2. Recorded Last BIOS time: **12.4 seconds** (hardware handoff time — within normal range).
3. Reviewed full startup list. Identified the following High-impact items:
   - `BlueStacksServices.exe` (88 child processes) — Enabled — **High** — no publisher registered
   - `CCXProcess.exe` (6 child processes) — Enabled — High — Adobe Creative Cloud
   - `AdobeCollabSync.exe` (3 child processes) — Enabled — High — Adobe sync
4. BlueStacksServices.exe identified as primary suspect: High startup impact, no publisher, large child process count, non-essential for business workflow.

**Event Viewer investigation — Application log:**

5. Opened Event Viewer → Windows Logs → Application on machine Shark007.
6. Total events in Application log: 17,912 — filtered by Warning and Error, sorted by Date descending.
7. Located the following event at 4/3/2026 3:30:20 PM:

   | Field | Value |
   |---|---|
   | Event ID | **4096** |
   | Source | **VBScriptDeprecationAlert** |
   | Level | **Warning** |
   | Log Name | Application |
   | Computer | Shark007 |
   | Date | 4/3/2026 3:30:20 PM |

8. ProcessTree in event detail:
   ```
   cscript.exe;BlueStacksServices.exe;explorer.exe;userinit.exe;winlogon.exe
   ```
9. ProcessTreeEnhanced confirms:
   `cscript.exe ("cscript.exe //Nologo <path>\regList.wsf A <path>\BlueStacksServices");BlueStacksServices.exe ("<path>\BlueStacksServices.exe" --hidden);explorer.exe;userinit.exe;winlogon.exe`

**Root Cause Identified:**

BlueStacksServices.exe is invoking `cscript.exe` with a VBScript file (`regList.wsf`) during the Windows login sequence (winlogon → userinit → explorer). Windows 11 is actively deprecating VBScript. Event ID 4096 is the system's warning that a deprecated scripting method was used. In the user's environment, this invocation is failing or causing a delay sufficient to crash the dependent application at login.

The fault is confirmed at two diagnostic layers:
- **Task Manager:** BlueStacksServices.exe — High startup impact, 88–106 child processes
- **Event Viewer:** Event ID 4096 at login time, ProcessTree explicitly names BlueStacksServices.exe

---

## Actions Taken

1. Opened Task Manager → Startup Apps on Shark007.
2. Right-clicked BlueStacksServices.exe → selected **Disable**.
3. Confirmed Status changed to **Disabled**.
4. Reviewed remaining startup list and disabled additional non-essential items:
   - Spotify Launcher, Spotify — Disabled (personal application)
   - Microsoft Teams — Disabled (user launches manually as needed)
   - Telegram Desktop — Disabled (personal messaging)
   - Xbox — Disabled (gaming platform, not required on workstation)
   - Microsoft 365 Copilot — Disabled (AI overlay, not required at login)
   - Phone Link — Disabled (personal device sync)
5. Recorded updated Last BIOS time: **15.3 seconds** (within normal range — BIOS time varies slightly between boots).
6. Opened Event Viewer → Application log.
7. Located and recorded Event ID 4096 — VBScriptDeprecationAlert — 4/3/2026 3:30:20 PM.
8. Captured ProcessTree confirming BlueStacksServices.exe as the invoking process during winlogon.
9. Advised user to reboot and report whether login crash recurs.

---

## User Communication

The user was informed that the slow boot was caused by a third-party Android emulator application (BlueStacks) that was configured to run a significant number of background processes at startup. They were also informed that BlueStacks was generating a Windows system warning during login by running a scripting method that Windows 11 is phasing out, which was causing the application crash they experienced each morning.

The user was advised that:
- BlueStacks has not been uninstalled and remains available to launch manually if needed
- It will no longer start automatically at login
- Several other non-work applications have also been removed from startup to improve overall boot performance
- They should reboot and test before their next shift and contact the helpdesk if the crash recurs

---

## Outcome

Startup configuration remediated on machine Shark007. BlueStacksServices.exe and seven additional non-essential startup items disabled. Event ID 4096 (VBScriptDeprecationAlert) recorded and attributed to BlueStacksServices.exe ProcessTree during winlogon. Root cause confirmed at both the startup layer and the event log layer. Login crash expected to be resolved on next boot. Reboot verification pending.

No changes required to:
- Windows system files or drivers
- Network or domain configuration
- User profile or application data
- Licence or account settings

---

## Validation Evidence

| Screenshot | What It Confirms |
|---|---|
| `01_startup_apps_baseline_annotated.png` | Startup list at baseline — BlueStacks and CCXProcess flagged High |
| `02_bluestacks_disabled_annotated.png` | BlueStacksServices.exe confirmed Disabled in startup list |
| `03_event_viewer_vbscript_warning_annotated.png` | Event ID 4096 — VBScriptDeprecationAlert — ProcessTree confirms BlueStacks |

---

## Troubleshooting Logic

| Check | Location | Result |
|---|---|---|
| Last BIOS time | Task Manager → Startup Apps (top right) | 12.4s baseline — hardware normal |
| Startup items with High impact | Task Manager → Startup Apps → Status + Impact columns | BlueStacksServices.exe — High — Enabled — primary suspect |
| Publisher verification | Task Manager → Startup Apps → Publisher column | No publisher registered for BlueStacks — confirms non-Microsoft, non-business process |
| Event log at login time | Event Viewer → Application log → Warning level | Event ID 4096 — VBScriptDeprecationAlert — 4/3/2026 3:30:20 PM |
| ProcessTree in event detail | Event 4096 → General tab → ProcessTree field | cscript.exe;BlueStacksServices.exe;winlogon.exe — root cause confirmed |
| Fix applied | Startup Apps → Disable | BlueStacksServices.exe disabled — 7 additional items disabled |
| Root cause | VBScript invocation during winlogon by BlueStacks | Event ID 4096 — BlueStacks ProcessTree — confirmed |
| Resolution | Disable BlueStacksServices.exe at startup | Login crash expected resolved on next boot |

---

## Forward Risk Note

Event ID 4096 from VBScriptDeprecationAlert is not just a current fault indicator. Microsoft is actively removing VBScript support from Windows 11 across a phased rollout. Applications that invoke VBScript during startup — as BlueStacksServices.exe does via regList.wsf — will transition from generating warnings (current state) to generating hard failures in future Windows 11 builds. This machine will likely experience a recurring and worsening fault if BlueStacks is re-enabled for startup without a vendor update that removes the VBScript dependency.

**Recommended follow-up:**
- Check if a BlueStacks update is available that addresses the VBScript invocation
- If BlueStacks is not required for business purposes, raise a request to block it via application policy
- Monitor the Application event log on this machine for recurrence of Event ID 4096 after any BlueStacks update

---

## Ticket Closure Note

Startup performance fault and login crash investigated and remediated on machine Shark007. BlueStacksServices.exe identified as primary cause via Task Manager Startup Apps (High impact, 88–106 child processes) and corroborated by Event Viewer Event ID 4096 (VBScriptDeprecationAlert, ProcessTree confirming BlueStacks invocation during winlogon). Startup item disabled. Seven additional non-essential startup items disabled to further reduce boot load. User informed and advised on next steps. Reboot verification pending. Forward risk of VBScript deprecation noted and flagged for follow-up.

**Documented by:**
Nnamso Mkpong
IT Support Portfolio
