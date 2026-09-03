# Second Analytics Rule: Detecting New User Account Creation

## Goal
Build a second, different type of detection rule — this time using Entra ID 
Audit Logs instead of subscription Activity Logs — to detect new user account 
creation, a common technique attackers use to maintain persistent access.

## Why this matters
Creating a new user account is a classic "persistence" technique in the 
MITRE ATT&CK framework — if an attacker gains temporary access, creating a 
new account lets them keep access even if the original compromised account 
is discovered and disabled. Monitoring for unexpected account creation is a 
standard SOC detection.

## The rule I built
**Query used:**
```kql
AuditLogs
| where OperationName == "Add user"
| where Result == "success"
| extend InitiatorUPN = tostring(InitiatedBy.user.userPrincipalName)
```

**Key settings:**
- Severity: Medium
- Tactic: Persistence
- Run frequency: Every 1 hour
- Entity mapping: Account entity mapped to `InitiatorUPN`

## Troubleshooting: finding the right OperationName
I initially assumed the operation name for user creation would simply be 
"Add user," but my first test (creating a user before I'd confirmed this) 
returned zero results. Rather than guess further, I ran:

```kql
AuditLogs
| distinct OperationName
```

This lists every unique operation name actually present in my data — a much 
more reliable way to find the exact value than guessing based on assumption.

### First attempt showed nothing new
Even after widening the time range, my first test user's creation event never 
appeared — only an unrelated background event ("Remove service principal") 
showed up. This meant the diagnostic setting likely wasn't active yet when 
that first test user was created, so the event was simply never captured — 
not a query problem.

### Second attempt succeeded
I created a fresh test user and waited (Entra ID's AuditLogs pipeline has 
consistently had longer latency than the subscription Activity Log throughout 
this project). This time, `OperationName` correctly showed **"Add user"**, 
confirming both the exact field value and that the pipeline was genuinely 
working.

## Nested field handling
The `InitiatedBy` column in AuditLogs is a nested JSON object, not a simple 
text field. I had to use `tostring(InitiatedBy.user.userPrincipalName)` to 
extract a readable email/username from it for entity mapping — a different 
structure than the flat `Caller` field I used in my first (AzureActivity-based) 
rule.

### Key lesson
Different data tables in Sentinel can structure similar information very 
differently (flat fields vs. nested JSON). Always inspect the actual data 
structure with a manual query before assuming a field will work the same way 
across different tables.

## Testing and verification
Once the rule was live, it correctly detected the real "Add user" event on 
its next scheduled run, generating an incident titled "New User Account 
Created." I investigated the incident (confirmed entities, checked evidence, 
reviewed the underlying event), then closed it as **Benign Positive** since 
it was my own intentional test activity.

## Status
✅ Complete — second Analytics Rule built, tested with real data, and the 
resulting incident properly investigated and closed.
