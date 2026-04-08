# Help Desk Ticket #0094

**Category:** Identity Management — New User Onboarding
**Priority:** P3 Medium — planned work, start date is Monday 15 April 2026
**Status:** Closed

---

## Ticket Details

| Field | Value |
|---|---|
| Ticket ID | TKT-0094 |
| Date Opened | 10 April 2026 — 09:15 |
| Date Closed | 14 April 2026 — 16:45 |
| Provisioning Deadline | 14 April 2026 (Friday before Monday start) |
| SLA Response Target | 4 hours (P3 Medium) |
| SLA Resolve Target | 24 hours (with deadline override — must complete by April 14) |
| First Response Sent | 09:28 (13 minutes after intake) |
| SLA Response Status | Met |
| SLA Resolve Status | Met |
| Assigned To | Nnamso Mkpong — IT Support |
| New User | Maria Shima |
| Department | Finance |
| Manager | Heidi Hogan |
| Start Date | Monday 15 April 2026 |
| Machine Assigned | WIN11_CLIENT01 |
| Domain | mylab.local |

---

## Request Summary

HR submitted an onboarding request for Maria Shima joining the Finance Department on Monday 15 April 2026. All provisioning must be completed by end of business Friday 14 April to ensure the device and account are ready before the user arrives.

Requirements from the ticket:

Account creation in Active Directory with domain logon name maria.shima@mylab.local. Department: Finance. Manager: Heidi Hogan. Required applications: Microsoft Office, Microsoft Teams, Google Chrome. Hardware: Laptop and Headset.

---

## First Response

**Sent at 09:28 — 13 minutes after intake, to Heidi Hogan (manager):**

> Hi Heidi, thank you for submitting the onboarding request for Maria Shima. I have logged this as TKT-0094 and I am targeting completion of all provisioning by Friday 14 April so everything is ready before Monday.
>
> I will need to confirm the following before I proceed: which Organisational Unit in Active Directory should the account be created in (standard Users container or a specific department OU), whether a Microsoft 365 licence is available for assignment, and whether WIN11_CLIENT01 is the laptop designated for this user.
>
> I will update you by end of business Friday with a Day One handover note confirming everything that is ready.

---

## Provisioning Log

**10 April 2026 — 10:05 — HR confirmation received**

Heidi Hogan confirmed: standard Users container is correct, a Microsoft 365 licence is available in the tenant, and WIN11_CLIENT01 is the designated laptop. Provisioning proceeding.

**10 April 2026 — 10:20 — AD account created**

Created user account in Active Directory Users and Computers. Account details:

Full name: Maria Shima. User logon name: maria.shima@mylab.local. Pre-Windows 2000 logon: MYLAB\maria.shima. OU: mylab.local/Users. Temporary password set. User must change password at next logon: enabled.

**10 April 2026 — 10:35 — Finance_Department group created and user assigned**

Finance_Department security group did not exist. Created new Global Security group named Finance_Department in mylab.local/Users. Added Maria Shima to Finance_Department. Confirmed group membership: Domain Users and Finance_Department both confirmed on Member Of tab.

**11 April 2026 — 09:00 — Device provisioned and domain joined**

WIN11_CLIENT01 collected from IT storage. Confirmed DNS on the client was set to the domain controller IP (192.168.1.1) before attempting domain join. Joined the machine to mylab.local using domain admin credentials. Machine restarted. Confirmed machine visible in ADUC Computers container as WIN11_CLIENT01.

Confirmed System Properties: Full computer name WIN11_CLIENT01.mylab.local. Domain: mylab.local.

**11 April 2026 — 11:30 — Email access provisioning**

Submitted Microsoft 365 licence request to the M365 admin. Admin confirmed licence assigned to maria.shima@mylab.local. Exchange Online mailbox created automatically. Verified email access available via Outlook and OWA. Confirmation sent to Heidi Hogan.

**14 April 2026 — 09:00 — Software installation**

Installed the following applications on WIN11_CLIENT01 and verified each in Settings > Apps > Installed Apps:

Microsoft Teams version 1.25.28902, installed 4/7/2026.
WPS Office version 12.2.0.23196, installed 4/7/2026.
Google Chrome version 146.0.7680.178, installed 4/7/2026.
Microsoft 365 version 16.0.19822.20142, installed 4/7/2026.

All four applications confirmed installed and launchable.

**14 April 2026 — 11:00 — Shared drive created and mapped**

Confirmed Finance_Share folder is shared on the file server at \\WINDOWSSERVER202\Finance_Share (IP 192.168.1.10). NTFS permissions confirmed: Finance_Department group has Modify access. Other users denied.

Mapped Finance_Share as drive X: on WIN11_CLIENT01 from \\192.168.1.10\Finance_Share. Confirmed drive appears in File Explorer under Network Locations with 42.6 GB free of 59.3 GB.

**14 April 2026 — 14:30 — Day One handover note produced**

Produced and attached the Day One handover note to this ticket. Contents confirmed:

User: Maria Shima. Department: Finance. Manager: Heidi Hogan. Start Date: 15 April 2026. Device: WIN11_CLIENT01. Login: MYLAB\maria.shima. Email: maria.shima@mylab.local. Software: Microsoft Office, Microsoft Teams, Google Chrome. Access: Domain User, Finance_Department group, Finance_Share (\\192.168.1.10\Finance_Share mapped as X:).

Handover note sent to Heidi Hogan at 14:45.

**14 April 2026 — 16:30 — Manager confirmation received**

Heidi Hogan confirmed receipt of the handover note and confirmed the setup meets all requirements. Ticket closed at 16:45.

---

## Onboarding Checklist — Completion Record

| Action | Completed | Date | Notes |
|---|---|---|---|
| AD account created | Yes | 10 April | maria.shima@mylab.local |
| Finance_Department group created | Yes | 10 April | Global Security group |
| User added to Finance_Department | Yes | 10 April | Confirmed on Member Of tab |
| Device domain joined | Yes | 11 April | WIN11_CLIENT01.mylab.local |
| Device visible in ADUC | Yes | 11 April | Computers container confirmed |
| M365 licence assigned | Yes | 11 April | Email access confirmed |
| Microsoft Teams installed | Yes | 14 April | Version 1.25.28902 |
| WPS Office installed | Yes | 14 April | Version 12.2.0.23196 |
| Google Chrome installed | Yes | 14 April | Version 146.0.7680.178 |
| Microsoft 365 installed | Yes | 14 April | Version 16.0.19822.20142 |
| Finance_Share permissions set | Yes | 14 April | Finance_Department: Modify |
| Network drive mapped | Yes | 14 April | X: = \\192.168.1.10\Finance_Share |
| Day One handover note produced | Yes | 14 April | Sent to manager at 14:45 |
| Manager confirmation received | Yes | 14 April | Heidi Hogan confirmed at 16:30 |

---

## Outcome

All provisioning completed for Maria Shima before the Monday 15 April 2026 start date. Device ready, account active, software installed, shared drive mapped, email access confirmed, and manager notified. No missed steps. No access gaps.

**Documented by:**
Nnamso Mkpong
IT Support Portfolio
