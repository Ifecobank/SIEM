# Enabling UEBA (User and Entity Behavior Analytics)

## Goal
Enable UEBA in Microsoft Sentinel to build behavioral baselines for accounts 
and devices, enabling anomaly-based detection alongside my existing 
signature-based Analytics Rules.

## What is UEBA
UEBA is fundamentally different from an Analytics Rule. A rule detects a 
*specific known pattern* I define in advance — like "a resource group was 
deleted" or "a new user was created." UEBA instead builds a behavioral 
baseline for each individual user or device (what's normal for THIS 
account specifically — usual sign-in times, locations, activity patterns), 
and flags deviations from that baseline. This means it can catch things I 
never thought to write a rule for — like an account behaving unusually 
compared to its own normal pattern — even when that specific scenario 
doesn't match any fixed detection logic. It's the difference between 
signature-based detection (matching known bad patterns) and anomaly-based 
detection (matching deviations from normal).

## Troubleshooting: the MDI prerequisite confusion
When first opening the Entity behavior settings, I saw a note that syncing 
user entities required Microsoft Defender for Identity (MDI), which sounded 
like a blocker since I don't have that set up. On closer reading (and 
checking Microsoft's documentation), I found this requirement only applies 
to syncing users from an **on-premises Active Directory** domain. Since my 
environment is entirely cloud-based (Microsoft Entra ID only, no on-prem AD 
server), MDI wasn't actually required for my setup.

### Key lesson
Prerequisite warnings in documentation aren't always universal — they're 
often conditional on a specific scenario (in this case, on-premises AD sync 
specifically). Reading the actual condition attached to a requirement, 
rather than assuming it blocks me outright, saved me from thinking a 
feature was unavailable when it actually wasn't.

## What I configured
- Enabled UEBA on Microsoft Entra ID (cloud-based identity source)
- Enabled UEBA analysis on my existing data sources (Azure Activity, 
  Azure AD/Entra ID)

## Verification
Searched for my own account and host machine entity in Sentinel > Entity 
behavior, confirming both appeared with profile pages (Info, Timeline, 
Alerts, Insights tabs).

Note: since UEBA baselines are built from historical behavior, meaningful 
anomaly detection will take time to develop as more activity accumulates in 
this environment — this is expected for a newer lab setup, not a 
configuration issue.

## Status
✅ Complete — UEBA enabled and confirmed active; baseline data will continue 
building over time.
