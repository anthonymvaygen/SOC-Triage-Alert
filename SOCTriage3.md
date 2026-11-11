## Scenario 3

### Step 1 — New Alert

Approximately 20 minutes after the SharePoint download activity, a new alert was generated:

Alert category: “Mailbox Rule Created.”

The alert indicated that a new inbox rule had been added to the user's Exchange Online mailbox.

Event details:

Timestamp: 3:58 AM EST

User: j.smith

SourceIP: 185.22.58.14

Action: New Inbox Rule Created

Rule Name: Archive-Processing

Behavior:
- Move incoming messages to RSS Feeds folder
- Mark messages as read
- Apply to messages containing financial keywords

The activity originated from the same Prague IP observed in the previous two alerts.

### Step 2 — Rule Inspection

I reviewed the mailbox configuration to understand the purpose of the newly created rule.

Findings:

- Rule created outside of business hours
- User had no prior custom mailbox rules
- Rule was not created by an administrator
- Rule targeted messages containing invoice and payment-related terms
- Rule immediately became active

The naming convention appeared generic and intended to avoid attention.

### Step 3 — Related Activity

Additional checks showed:

- No mailbox delegation changes
- No new OAuth application consent grants
- No MFA enrollment activity
- No privilege escalation attempts
- No additional user accounts involved

However:

- Multiple mailbox access events appeared after the suspicious login
- The rule creation occurred after the SharePoint download activity
- Activity timeline suggested the actor was attempting to maintain access while avoiding detection

### Step 4 — Assess Likelihood of Compromise

Indicators supporting compromise:

- Same malicious IP across all alerts
- Previously confirmed unauthorized login
- Bulk SharePoint download activity
- New mailbox rule creation
- Non-managed device
- No MFA protection

Indicators against compromise:

- No evidence of privilege escalation
- No lateral movement
- No persistence mechanisms beyond mailbox manipulation

Conclusion:

At this point, confidence is extremely high that the account was compromised. The mailbox rule appears to be an attempt to hide potentially important messages from the user and establish a low-noise persistence mechanism.

### Step 5 — Recommended Actions

Immediate:

- Disable account access
- Remove malicious inbox rule
- Revoke active sessions and refresh tokens
- Force password reset
- Require MFA before re-enablement

Follow-up:

- Review mailbox activity for missed communications
- Search for similar rules across tenant mailboxes
- Investigate whether additional accounts were targeted
- Audit Exchange Online administrative actions
- Tune detections for suspicious mailbox rule creation

### Step 6 — Final Summary

A third alert revealed the creation of a suspicious mailbox rule on the compromised account. The activity originated from the same Prague IP involved in the unauthorized login and SharePoint download events. The rule appeared designed to automatically hide potentially valuable email communications from the user. Combined with previous findings, the incident is assessed as a confirmed account compromise involving unauthorized access, data collection, and attempted persistence within the user's Microsoft 365 environment.
