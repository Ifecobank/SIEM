# Building a Watchlist: Monitored Accounts

## Goal
Create a Watchlist in Sentinel to maintain a reusable reference list of 
accounts requiring closer security monitoring, and confirm it can be 
referenced from KQL queries.

## What is a Watchlist
A Watchlist is a reusable, centrally-managed list of reference data (like 
account names, IP addresses, or asset names) that can be checked against in 
any query or Analytics Rule. Instead of hardcoding a fixed value directly 
into every query, a Watchlist lets you maintain one central list and update 
it in one place — every rule or hunt that references it automatically stays 
current. This is especially useful for things like VIP/privileged accounts, 
where a SOC team wants consistent, elevated monitoring without having to 
manually update dozens of separate rules whenever the list changes.

## What I built
Created a watchlist named "Monitored Accounts" (alias: `MonitoredAccounts`) 
containing one entry: my own account, flagged as "Lab owner - baseline 
monitoring."

**Structure:**
| AccountUPN | Reason |
|---|---|
| ifekwuifeanyi1@outlook.com | Lab owner - baseline monitoring |

**SearchKey:** `AccountUPN`

## Troubleshooting: file upload issues
Ran into two separate file-related problems getting the CSV uploaded:

1. **Hidden .txt extension**: Notepad silently saved the file as 
   `monitored-accounts.csv.txt` instead of `.csv`, despite typing `.csv` in 
   the filename — needed to explicitly set "Save as type: All Files."

2. **"Uploaded file cannot be empty" despite real content**: Even after 
   fixing the extension, Azure's parser reported the file as empty. 
   Investigated file size vs. "size on disk" (76 bytes vs. 0 bytes on disk), 
   which pointed toward a sync/encoding issue. Recreated the file using 
   PowerShell's `Set-Content` with explicit `-Encoding UTF8`, which resolved 
   it — Azure's watchlist parser appears to require plain UTF-8, and 
   Notepad/PowerShell defaults weren't matching that.

### Key lesson
A file "looking" correct when opened isn't the same as it being in the 
right format for a specific tool to parse — encoding is invisible until 
something breaks. When a cloud platform rejects a file that looks fine 
locally, checking file size, size-on-disk, and encoding explicitly (rather 
than assuming the file itself is the problem) is a faster path to the real 
cause.

## Testing the watchlist in KQL

**Confirming the watchlist is readable:**
```kql
_GetWatchlist('MonitoredAccounts')
```

**Using it to filter real data:**
```kql
AzureActivity
| where Caller in ((_GetWatchlist('MonitoredAccounts') | project AccountUPN))
```
This successfully returned matching AzureActivity events, confirming the 
watchlist can be used to filter/cross-reference real log data — exactly how 
it would be used inside an Analytics Rule in a real environment (e.g., 
"only alert if the account involved is NOT on the approved list").

## Verification
Ran the integration query above and confirmed multiple matching 
`AzureActivity` events returned, including `MICROSOFT.SECURITYINSIGHTS/INCIDENTS/WRITE` 
operations tied to the monitored account — confirming the watchlist 
correctly cross-references real log data end-to-end.

## Status
✅ Complete — Watchlist created, populated, and confirmed working via KQL 
integration with real AzureActivity data.
