# SOC-Triage-Alert
Investigating a Suspicious Login Alert
I put this write‑up together as a practice investigation to sharpen my SOC triage workflow. It’s based on the kind of alert I handled during my cybersecurity internship, but I recreated the scenario so I could walk through it more slowly and document each step. It’s not meant to be perfect — just realistic and useful.

**Scenario**
A SIEM flagged a successful login from an unusual foreign location for user j.smith.
The login happened at 3:14 AM EST from an IP geolocated in Prague, Czech Republic.
The user normally logs in from Philadelphia during business hours.

Alert category: “Impossible Travel / Suspicious Authentication Pattern.”

I’ve seen variations of this alert before, but this one had a couple of interesting details.

Step 1 — Quick Triage
The first thing I always do is make sure the alert itself isn’t misleading.

1.1 Check for VPN or proxy
No corporate VPN ranges match the IP

No common consumer VPN ranges match either (Nord, Proton, etc.)

IP reputation: neutral, but definitely not U.S.-based

1.2 Pull basic authentication metadata
Example log fields:

User: j.smith
Timestamp: 2026-07-09T03:14:22Z
SourceIP: 185.22.58.14
Location: Prague, CZ
Device: Chrome on Windows
MFA: Not Applied
AuthMethod: Password
The “MFA: Not Applied” line jumped out immediately.

Step 2 — Compare Against Normal Behavior
This part is pretty straightforward but important.

User normally logs in between 8 AM – 6 PM EST

Always from Philadelphia

Always on a managed Windows laptop

Device compliance tag is usually present (Intune)

The login in question:

Happened at 3:14 AM

From Prague

On a non‑managed device

With no MFA

So at this point, it’s already looking suspicious.

Step 3 — Look for Related Activity
I checked events before and after the login. I didn’t find:

password reset attempts

MFA enrollment changes

multiple failed logins

token refresh anomalies

unusual file access

SharePoint/OneDrive spikes

privilege escalation attempts

Basically, nothing else weird happened. That’s good, but it doesn’t clear the event.

Step 4 — Assess Likelihood of Compromise
Indicators suggesting compromise:

foreign login

no MFA

non‑corporate device

odd login time

no travel history

no VPN detected

Indicators against compromise:

no lateral movement

no mailbox rule changes

no sensitive data access

My conclusion: likely credential compromise, but not a full-blown breach.

Step 5 — Recommended Actions
Immediate
Force password reset

Kill active sessions

Require MFA enrollment

Contact user to confirm no travel

Follow‑up
Check mailbox rules

Review OAuth tokens

Review recent file access

Add conditional access policy for foreign logins

Add detection rule for repeated failed logins from same IP

This is pretty standard, but it works.

Step 6 — Final Summary
A suspicious login occurred for j.smith from Prague at 3:14 AM EST. The login bypassed MFA and came from a non‑managed device. No VPN indicators were found. No lateral movement or data access anomalies were detected. The event is assessed as a likely credential compromise. Immediate containment and MFA enforcement recommended.
