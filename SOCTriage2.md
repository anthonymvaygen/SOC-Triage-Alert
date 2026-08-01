## Scenario 2
Step 1 — Quick Triage
A second alert came in for the same user, j.smith. It was flagged as:

Alert category: “Suspicious File Download Activity.”

The SIEM detected an unusually large download from SharePoint tied to the same account.

Event details:

Timestamp: 3:36 AM EST

SourceIP: 185.22.58.14 (same Prague IP)

File count: 42

Total size: ~1.8 GB

Location: Prague, CZ

Device: Chrome on Windows

MFA: Not Applied

The matching IP and timestamp made this worth immediate attention.

Step 2 — Baseline Comparison
I checked the user’s normal SharePoint behavior:

Typically accesses only two project folders

Rarely downloads more than 2–3 files at once

No history of bulk exports

No off‑hours activity

No foreign logins ever recorded

The alert activity:

Bulk download

Off‑hours

Foreign IP

Non‑managed device

No MFA

Nothing about this matched the user’s normal pattern.

Step 3 — Related Activity Check
I pulled surrounding events:

No upload activity

No file deletions

No permission changes

No sharing links created

No sync client usage

No Teams message spikes

No OneDrive sync anomalies

It was strictly a download event — no signs of staging or exfil beyond that.

Step 4 — Assess Likelihood of Compromise
Indicators supporting compromise:

Same foreign IP as previous incident

Same device fingerprint

No MFA

Bulk download

Off‑hours

No business justification

No prior history of similar behavior

Indicators against compromise:

No lateral movement

No privilege escalation

No mailbox anomalies

No external sharing

Conclusion: High‑confidence unauthorized access, likely the attacker attempting data collection after the initial login.

Step 5 — Recommended Actions
Immediate:

Block account

Revoke all tokens

Kill active sessions

Disable SharePoint access temporarily

Notify IR team

Contact user for confirmation

Follow‑up:

Review downloaded file list

Check for sensitive data exposure

Audit SharePoint permissions

Add detection for bulk downloads from new locations

Add conditional access rules for foreign access

Step 6 — Final Summary
A second alert for j.smith occurred at 3:36 AM EST, involving a bulk SharePoint download from the same Prague IP used in the earlier unauthorized login. The activity was inconsistent with the user’s normal behavior and occurred without MFA on a non‑managed device. No additional malicious actions were detected, but the download itself indicates attempted data collection. The event is assessed as a confirmed compromise requiring immediate containment and a full review of downloaded content.
