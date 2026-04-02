# Help Desk Ticket #0042

**Category:** Windows 11 — Software Deployment and Version Management
**Priority:** Medium — Required before shift start
**Status:** Resolved

---

## Ticket Details

| Field | Value |
|---|---|
| Ticket ID | 0042 |
| Date Opened | April 2026 |
| Date Resolved | April 2026 |
| Assigned To | Nnamso Mkpong — IT Support |
| Machine | WIN11_CLIENT01 |
| Application | Adobe Acrobat Reader |
| Approved Version | 2025.001.21288 (64-bit) |
| Conflicting Version | Adobe Acrobat 5.0 / Acrobat Reader 5.1 |
| Priority | Medium — user requires application before shift start |

---

## Issue Reported

User requires the approved version of Adobe Acrobat Reader installed and confirmed before the start of their shift. A previous installation may be present on the machine. IT requires that the approved version is verified, any conflicting version is identified and removed, and evidence of the correct state is captured before the ticket is closed.

---

## Investigation

**Baseline — approved version installed and confirmed:**

1. Downloaded `Reader_en_install` (1.56 MB) from the official Adobe source to the Downloads folder.
2. Ran the installer — installation completed at 100% with no errors.
3. Opened Adobe Acrobat Reader and navigated to Menu → Help → About Adobe Acrobat Reader.
4. Confirmed version string: **2025.001.21288 | Continuous Release | 64-bit**.
5. Baseline confirmed: approved version installed and version number matches IT requirement.

**Conflict simulation — legacy version introduced:**

6. Downloaded legacy installer `acrobat51` (13,415 KB) to the Downloads folder to simulate a pre-existing legacy installation.
7. Ran the Acrobat Reader 5.1 setup wizard — installation completed with confirmation dialog.
8. Confirmed legacy splash screen: **Acrobat 5.1.0 — September 17, 2002**.
9. Both versions now present on the machine simultaneously — conflict state active.

**Conflict identification:**

10. Attempted to launch Adobe Acrobat 5 from the desktop shortcut.
11. Windows 11 **Program Compatibility Assistant** fired with the following warning:
    - Application: **Adobe Acrobat 5**
    - Message: This app cannot run because it causes security or performance issues on Windows.
12. Opened Settings → Apps → Installed Apps and confirmed both versions listed:
    - Adobe Acrobat (64-bit) 26.001.21367 — approved version, present
    - Adobe Acrobat 5.0 — conflicting legacy version, present

**Root Cause Identified:**

Legacy application (Adobe Acrobat 5.0 / Reader 5.1) present on the machine alongside the approved version. The legacy application is a 32-bit application built for Windows XP. Windows 11 flags it as a security and performance risk and blocks execution. The user is unable to determine which icon to use and may attempt to work with the legacy version, which cannot open.

---

## Actions Taken

1. Confirmed approved version (2025.001.21288) is installed and functional.
2. Identified legacy version (Adobe Acrobat 5.0) present in Installed Apps list.
3. Navigated to Settings → Apps → Installed Apps.
4. Located Adobe Acrobat 5.0 entry — clicked three-dot menu (⋮) → Uninstall.
5. Followed uninstall prompts to completion.
6. Refreshed Installed Apps list — confirmed Adobe Acrobat 5.0 no longer present.
7. Launched Adobe Acrobat Reader from Start Menu — opened to Welcome screen with no warnings.
8. Reconfirmed version via Help → About: **2025.001.21288 | 64-bit — unchanged**.
9. Approved version is the only Adobe Reader installation on the machine.

---

## User Communication

The user was informed that the approved version of Adobe Acrobat Reader is installed and confirmed. An older version that had been present on the machine has been removed. They were advised that Windows 11 had flagged the older version as incompatible and that it could not have been used for work regardless. The user was asked to use the Adobe Acrobat shortcut on the Start Menu going forward and to contact the helpdesk if the application fails to open or if a compatibility warning appears.

---

## Outcome

Software deployment task completed for WIN11_CLIENT01. Approved version Adobe Acrobat Reader 2025.001.21288 (64-bit) confirmed installed and running. Legacy conflicting version Adobe Acrobat 5.0 removed via Installed Apps. Application opens to home screen without error or compatibility warning. Version string reconfirmed after legacy removal — unchanged.

No changes were required to:

- Windows audio or display settings
- Network configuration
- User account or licence
- Driver installation

Root cause confirmed as **legacy application (Adobe Acrobat 5.0) present alongside approved version, generating compatibility conflict on Windows 11**.

---

## Validation Evidence

| Screenshot | What It Confirms |
|---|---|
| `01_download_installer.png` | Approved installer present in Downloads folder |
| `02_installation_in_progress.png` | Installer running at 80% — no errors |
| `03_installation_complete.png` | Installation completed at 100% |
| `04_version_check_annotated.png` | Version 2025.001.21288 (64-bit) confirmed via Help → About |
| `05_legacy_installer_downloaded.png` | Legacy acrobat51 installer present (conflict simulation) |
| `06_legacy_setup_wizard.png` | Legacy Reader 5.1 setup wizard running |
| `07_legacy_install_confirmation.png` | Legacy installation confirmed complete |
| `08_legacy_splash_screen.png` | Acrobat 5.1.0 (9/17/2002) splash screen — conflict state |
| `09_compatibility_warning_annotated.png` | Program Compatibility Assistant warning — root cause visible |
| `10_uninstall_legacy_version_annotated.png` | Uninstall option selected for Adobe Acrobat 5.0 |
| `11_approved_version_running_annotated.png` | Approved version opens correctly — fault resolved |

---

## Troubleshooting Logic

| Check | Location | Result |
|---|---|---|
| Approved installer source and file | Downloads folder | Present — correct filename and size |
| Installation progress | Adobe Installer window | Completed 100% without error |
| Version number post-install | Help → About | 2025.001.21288 64-bit — confirmed |
| Legacy version presence | Settings → Apps → Installed Apps | Adobe Acrobat 5.0 found — root cause |
| Compatibility warning | Program Compatibility Assistant | Fired on Acrobat 5 launch — confirmed incompatible |
| Legacy version removal | Installed Apps → Uninstall | Adobe Acrobat 5.0 removed |
| Approved version post-removal | Welcome screen + Help → About | Opens correctly, version unchanged |
| Root cause | Legacy app present alongside approved version | Adobe Acrobat 5.0 — Windows 11 incompatible |
| Resolution | Uninstall legacy version | Approved version confirmed sole installation |

---

## Real World Relevance

Software deployment calls are often treated as low-complexity tasks, but they carry significant risk if handled without a structured approach. A technician who installs an application without confirming the version, or who closes a ticket without checking for conflicting installations, may leave the user in a worse state than they were in before — with two versions installed, unclear file associations, and no certainty about which application is actually running.

The correct approach is to confirm what is installed before making changes, install or remove in a controlled sequence, confirm the version at the end, and record every step. This protects the user, protects the technician, and ensures the machine state is clear to the next person who opens the ticket or touches the machine.

---

## Ticket Closure Note

Software deployment completed for WIN11_CLIENT01. Approved Adobe Acrobat Reader 2025.001.21288 (64-bit) confirmed installed and running. Legacy conflicting version Adobe Acrobat 5.0 removed via Installed Apps. No warnings on launch. Version string confirmed unchanged after legacy removal. User informed and advised on correct shortcut to use. Ticket closed.

**Documented by:**
Nnamso Mkpong
IT Support Portfolio
