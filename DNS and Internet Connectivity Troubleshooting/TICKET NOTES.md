# Help Desk Ticket #0055

**Category:** Network Connectivity - DNS Name Resolution Fault
**Priority:** Standard
**Status:** Resolved

---

## Ticket Details

| Field | Value |
|------|------|
| Ticket ID | 0055 |
| Date Opened | March 2026 |
| Date Resolved | March 2026 |
| Assigned To | Nnamso Mkpong — IT Support |
| Machine | WIN11_CLIENT01 |
| Client IP | [CLIENT_IP] |
| Default Gateway | [DEFAULT_GATEWAY] |
| Incorrect DNS Used | 10.10.10.10 and 10.10.10.11 |
| Correct DNS Restored | 8.8.8.8 and 8.8.4.4 |
| Domain | [DOMAIN_NAME] |

---

## Issue Reported

User on **WIN11_CLIENT01** reported that websites were not loading in the browser. Microsoft Teams was still receiving messages and appeared connected. The user described the issue as the internet being down.

Browser error displayed on all sites attempted:

> **Hmmm... can't reach this page**
> www.google.com's server IP address could not be found.
> DNS_PROBE_FINISHED_BAD_CONFIG

---

## Investigation

**Baseline check performed before fault simulation:**

1. Confirmed google.com loaded normally in the browser.
2. `ping 8.8.8.8` — Pass. 4/4 replies at 22–31ms. Internet path confirmed working.
3. `nslookup microsoft.com 8.8.8.8` — Pass. Resolved to 13.107.246.56.
4. `nslookup google.com 8.8.8.8` — Pass. Resolved to 142.251.216.46.

Baseline confirmed: both internet connectivity and DNS resolution working before fault was introduced.

**Fault simulation:**

5. DNS server changed manually to `10.10.10.10` and `10.10.10.11` - non-existent addresses.
6. Attempted to browse google.com - Failed. DNS_PROBE_FINISHED_BAD_CONFIG.
7. Attempted to browse microsoft.com — Failed. Same error on both tabs.
8. `ping 8.8.8.8` - **Pass.** 4/4 replies. Internet path still fully working.
9. `nslookup microsoft.com` - **Failed.** DNS request timed out. Server shown as Unknown at 10.10.10.10.
10. `nslookup google.com` - **Failed.** DNS request timed out. Same unreachable server.

**Root Cause Identified:**

DNS server was manually set to `10.10.10.10` and `10.10.10.11`, neither of which exist on the network. Every DNS query timed out. The internet path was intact throughout. The fault was isolated entirely to DNS name resolution. Teams remained connected because it uses cached connection tokens from the previous session and does not require a fresh DNS lookup for every message.

---

## Actions Taken

1. Ran baseline ping and nslookup to confirm healthy state before changes.
2. Set DNS server manually to 10.10.10.10 and 10.10.10.11 to simulate the fault.
3. Confirmed browser returned DNS_PROBE_FINISHED_BAD_CONFIG on all sites.
4. Ran `ping 8.8.8.8` to prove internet was up during the browser failure.
5. Ran `nslookup microsoft.com` and `nslookup google.com` — both timed out, confirming DNS fault.
6. Ran `ipconfig /flushdns` to clear the DNS resolver cache.
7. Restored DNS to `8.8.8.8` (Preferred) and `8.8.4.4` (Alternate) in adapter settings.
8. Ran `nslookup microsoft.com` and `nslookup google.com` — both resolved correctly.
9. Opened microsoft.com in browser — page loaded fully. Connectivity restored.

---

## Outcome

Browsing restored on **WIN11_CLIENT01** after correcting the DNS server settings and flushing the resolver cache.

No changes were required to:

- Network adapter
- Default gateway
- Internet connection
- Router or switch configuration

Root cause was confirmed as **incorrect DNS server configuration**. The internet path was working throughout the entire fault. The machine was unable to translate domain names into IP addresses because the DNS server it was querying did not exist.

---

## Validation Evidence

- Baseline ping 8.8.8.8 confirmed internet working before and after fault
- Browser returned DNS_PROBE_FINISHED_BAD_CONFIG during fault on both google.com and microsoft.com
- ping 8.8.8.8 returned 4/4 replies while browser was failing — proves internet was up
- nslookup timed out on both domains during fault — confirms DNS server unreachable
- nslookup resolved both domains correctly after DNS restore
- microsoft.com loaded fully in browser after restore

---

## Troubleshooting Logic

| Check | Command | Result |
|------|------|------|
| Internet baseline | `ping 8.8.8.8` | Pass |
| DNS baseline | `nslookup microsoft.com 8.8.8.8` | Pass |
| Browse google.com (fault active) | Browser | Failed — DNS_PROBE_FINISHED_BAD_CONFIG |
| Browse microsoft.com (fault active) | Browser | Failed — DNS_PROBE_FINISHED_BAD_CONFIG |
| Internet during fault | `ping 8.8.8.8` | Pass — internet up, DNS broken |
| DNS during fault | `nslookup microsoft.com` | Failed — timed out, server 10.10.10.10 unreachable |
| DNS cache cleared | `ipconfig /flushdns` | Pass |
| DNS after restore | `nslookup microsoft.com` | Pass |
| DNS after restore | `nslookup google.com` | Pass |
| Browse after restore | microsoft.com in browser | Pass — page loaded fully |
| Root cause | DNS settings | Incorrect server — non-existent IP |
| Resolution | Restore correct DNS server | Access restored |

---

## Real World Relevance

DNS faults account for a significant proportion of browsing complaints raised to the helpdesk. The symptom is always described as the internet is down, which leads less experienced technicians to check routers, raise network tickets, or restart machines without resolving anything.

The correct first response is to run `ping 8.8.8.8`. If that succeeds, the internet is up and the investigation moves immediately to DNS. This diagnosis takes under 60 seconds and avoids unnecessary escalation. Knowing that Teams and other persistent applications can survive a DNS fault while the browser fails completely is the key piece of context that makes the symptom make sense.

---

## Ticket Closure Note

Browsing connectivity restored for affected user on WIN11_CLIENT01. Root cause identified as incorrect DNS server configuration pointing to non-existent addresses. Resolved by restoring correct DNS entries and flushing the resolver cache. No hardware or infrastructure changes required. Ticket closed.

**Documented by:**
Nnamso Mkpong
IT Support Portfolio
