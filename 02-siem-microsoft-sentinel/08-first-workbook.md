# Building My First Workbook: Environment Activity Overview

## Goal
Create a Sentinel Workbook (dashboard) that visualizes activity across my 
environment at a glance, rather than relying only on manually running 
individual KQL queries.

## What is a Workbook
[Explain in your own words: how is a Workbook different from just running 
a query in Logs? Why is this useful for a SOC Analyst or a SOC team?]

## What I built
Starting from a blank workbook, Sentinel automatically included a default 
chart showing event volume by table type across my entire workspace 
(AzureActivity, SecurityEvent, AuditLogs, etc.) — a useful overview I decided 
to keep. I then added two custom visuals:

**1. Activity over time (Area chart)**
```kql
AzureActivity
| summarize EventCount = count() by bin(TimeGenerated, 1h)
| order by TimeGenerated asc
```
Shows subscription activity volume across time, useful for spotting unusual 
spikes.

**2. Activity by Caller (Pie chart)**
```kql
AzureActivity
| summarize EventCount = count() by Caller
| order by EventCount desc
```
Shows which accounts/identities are generating activity — the same query I 
used during my earlier threat hunting session, now automated into a 
recurring visual instead of something I have to manually re-run.

## Troubleshooting: accidental instruction text in query
When copying a query, I accidentally included instruction text ("Set 
visualization type...") along with the actual KQL, which caused a parse 
error. The fix was simply isolating the real query from any surrounding 
notes/instructions before pasting.

### Key lesson
[Write 1-2 sentences: what's a good habit to avoid this kind of copy-paste 
error in the future?]

## Verification
[Add a screenshot of the finished workbook with all three visuals]

## Status
✅ Complete — Workbook built, saved, and reusable in Sentinel > Workbooks > 
My workbooks.
