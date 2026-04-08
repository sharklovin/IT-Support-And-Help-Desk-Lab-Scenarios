# Help Desk Ticket #0099

**Category:** Identity Management — User Offboarding and Access Removal
**Priority:** P2 High — account must be disabled before end of business on last day
**Status:** Closed

---

## Ticket Details

| Field | Value |
|---|---|
| Ticket ID | TKT-0099 |
| Date Opened | 29 April 2026 — 14:22 |
| Date Closed | 30 April 2026 — 17:15 |
| Offboarding Deadline | 30 April 2026 — end of business |
| SLA Response Target | 1 hour (P2 High) |
| SLA Resolve Target | 8 hours (same business day) |
| First Response Sent | 14:35 (13 minutes after intake) |
| SLA Response Status | Met |
| SLA Resolve Status | Met |
| Assigned To | Nnamso Mkpong — IT Support |
| Departing User | Maria Shima |
| Department | Finance |
| Manager | Heidi Hogan |
| Last Day | 30 April 2026 |
| Machine to Collect | WIN11_CLIENT01 |
| Submitted By | Heidi Hogan (Manager) — 29 April 2026 |

---

## Request Summary

Heidi Hogan submitted an offboarding request for Maria Shima on 29 April 2026. Last day of employment is 30 April 2026. All access must be removed and hardware collected by end of business on 30 April.

Actions required as listed on the ticket:

Disable AD account. Remove group memberships. Reset password. Collect laptop WIN11_CLIENT01. Collect headset. Verify no outstanding data or files needed.

---

## Authorisation Confirmation

> **Offboarding is a security-sensitive workflow. No action was taken on the user account until manager authorisation was confirmed in writing.**

Submitted by: Heidi Hogan (line manager).
Method of submission: HR self-service portal with manager credentials.
Authorisation confirmed: Yes — submission through authenticated HR portal constitutes authorisation.
Cross-reference with HR: HR confirmed Maria Shima termination as of 30 April 2026.

Proceeding with offboarding on 30 April.

---

## First Response

**Sent at 14:35 on 29 April — 13 minutes after intake, to Heidi Hogan:**

> Hi Heidi, thank you for submitting the offboarding request for Maria Shima. I have logged this as TKT-0099 and I will complete all required actions by end of business tomorrow, 30 April 2026.
>
> The account will be disabled at the start of business on 30 April. I will collect the laptop and headset from Maria directly — please advise the best time and location for collection.
>
> I will send you a completion confirmation once all actions have been completed and all hardware has been collected.

---

## Offboarding Execution Log

**30 April 2026 — 09:00 — Account disabled**

Opened Active Directory Users and Computers on the domain controller. Located Maria Shima in the Users container. Right-clicked and selected Disable Account. Confirmed: dialog read Object Maria Shima has been disabled.

The account is now unable to authenticate to any domain resource. Active sessions (if any) will expire on their next activity — IT operations was notified to check for any active VPN or remote desktop sessions and terminate them.

Account disable completed at 09:03.

**30 April 2026 — 09:10 — Group memberships removed**

Opened Finance_Department group properties in ADUC. Navigated to Members tab. Located Maria Shima and clicked Remove. Confirmation dialog appeared: Do you want to remove the selected member from the group? Clicked Yes.

Maria Shima is no longer a member of Finance_Department. Access to Finance_Share and all other Finance_Department-controlled resources is revoked. She remains in Domain Users by default — this is the standard minimum group and does not grant access to any departmental resources.

Group removal completed at 09:14.

**30 April 2026 — 09:18 — Password reset**

Opened Maria Shima's account properties in ADUC. Navigated to the Account tab. Reset password to a strong IT-controlled value (not recorded in this ticket). Confirmed User must change password at next logon is ticked. Confirmed Unlock account checkbox is cleared.

The account is now disabled with an unknown password. Even if re-enabled accidentally, the original password cannot be used and any re-enablement requires IT action.

Password reset completed at 09:21.

**30 April 2026 — 12:00 — Device collection**

Collected the following hardware from Maria Shima at 12:00 in the second floor meeting room. Heidi Hogan was present as witness.

Hardware collected:

Laptop WIN11_CLIENT01 — no physical damage, screen no cracks, keyboard functional, battery holds charge. Power adapter — collected. Headset — collected. Mouse — collected. Docking station — not issued, N/A.

Condition assessment completed. Data wipe confirmed required. Device tagged for reimaging and redeployment by the IT operations team.

Collection completed at 12:15.

**30 April 2026 — 12:20 — Outstanding data verification**

Confirmed with Heidi Hogan that there are no outstanding files or data belonging to Maria Shima that need to be retained or transferred. No business-critical files identified by the manager. No data recovery action required before wipe.

**30 April 2026 — 14:00 — M365 licence check**

Confirmed with the M365 admin that Maria Shima's Microsoft 365 licence has been revoked and her mailbox has been placed in a 30-day inactive state as per the organisation's data retention policy. Email forwarding was not requested by the manager.

**30 April 2026 — 16:45 — Final verification**

Confirmed the following final states in ADUC:

Maria Shima account: Disabled. The down arrow icon is visible on the account object in ADUC.
Finance_Department Members tab: Maria Shima is no longer listed.
WIN11_CLIENT01: Device is in IT possession, tagged for wipe and reimaging.

All offboarding actions completed. Confirmation email sent to Heidi Hogan at 16:50.

**30 April 2026 — 17:15 — Manager confirmation received**

Heidi Hogan confirmed receipt of the completion notification and confirmed all requirements have been met. Ticket closed at 17:15.

---

## Offboarding Checklist — Completion Record

| Action | Completed | Time | Evidence |
|---|---|---|---|
| Manager authorisation confirmed | Yes | 29 April 14:22 | HR portal submission by Heidi Hogan |
| AD account disabled | Yes | 09:03 | ADUC confirmation dialog — Object Maria Shima has been disabled |
| Active sessions terminated | Yes | 09:05 | IT operations confirmed no active VPN or RDP sessions |
| Finance_Department group membership removed | Yes | 09:14 | ADUC Members tab — Maria Shima no longer listed |
| Password reset — IT-controlled value | Yes | 09:21 | Account tab — must change at next logon confirmed |
| M365 licence revoked | Yes | 14:00 | M365 admin confirmation |
| Mailbox placed in inactive state (30-day retention) | Yes | 14:00 | Per data retention policy |
| Laptop (WIN11_CLIENT01) collected | Yes | 12:15 | Device collection checklist completed |
| Headset collected | Yes | 12:15 | Device collection checklist completed |
| Power adapter collected | Yes | 12:15 | Device collection checklist completed |
| Mouse collected | Yes | 12:15 | Device collection checklist completed |
| Outstanding data verified — none | Yes | 12:20 | Confirmed with manager Heidi Hogan |
| Device tagged for wipe and reimaging | Yes | 12:15 | IT operations notified |
| Manager completion confirmation received | Yes | 17:15 | Email from Heidi Hogan |

---

## Security Handling Record

All offboarding actions were completed in the correct order:

Account disabled before any other action: Yes. This is the security-critical first step. Disabling the account immediately blocks all authentication regardless of whether other removal steps are complete.

Group memberships removed after account disable: Yes. Removing groups after disabling ensures no active session could exploit lingering group access during the removal process.

Password reset after account disable: Yes. The password reset hardens the disabled account against accidental re-enablement.

Manager authorisation confirmed before any account action: Yes. No action was taken on the account until written authorisation was confirmed from the manager.

Recovery key exposure or sensitive data shared in ticket: No. No security credentials were documented in this ticket.

---

## Outcome

All offboarding actions completed for Maria Shima by 17:15 on 30 April 2026 — within the same-business-day deadline. Account disabled, group memberships removed, password reset, M365 licence revoked, all hardware collected with a completed condition checklist, and device tagged for reimaging. Manager confirmed completion. No access gaps identified. No security incidents.

Related onboarding ticket: TKT-0094 (completed 14 April 2026).

**Documented by:**
Nnamso Mkpong
IT Support Portfolio
