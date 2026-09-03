# Connecting Microsoft Entra ID Audit Logs to Sentinel

## Goal
Connect Microsoft Entra ID (Azure AD) logs to Sentinel to monitor identity 
and access-related activity — a critical data source for a SOC Analyst, 
since most real-world attacks involve compromised or misused accounts.

## Two types of Entra ID logs
- **Sign-in Logs**: every login attempt, successful or failed, including 
  location and device info. Requires a Microsoft Entra ID Premium P1 or P2 
  license to export.
- **Audit Logs**: administrative actions like user creation, role changes, 
  and app registrations. Exportable on the free tier, no premium required.

## Licensing roadblock
My Azure account only has the free tier, so Sign-in Logs export wasn't 
available. I looked into activating a free Entra ID P2 trial to unlock this, 
but discovered my account is tied to a personal Microsoft account (outlook.com), 
which doesn't have access to the Microsoft 365 admin center (admin.microsoft.com) 
required to activate that trial — that portal requires a proper work/school 
organizational account.

### Key lesson
Free/personal Azure trial accounts have real limitations beyond just cost — 
some licensing and admin features simply aren't accessible without an 
organizational account. Rather than getting stuck, I pivoted to what was 
actually available: Audit Logs.

## Connecting Audit Logs
1. Opened Microsoft Entra ID > Diagnostic settings
2. Created a new diagnostic setting named 'audit-logs-to-sentinel'
3. Selected only the 'AuditLogs' category (not 'SignInLogs', which needs 
   the premium license)
4. Set destination to Log Analytics workspace: SOCAnalyst
5. Saved

## Troubleshooting: longer sync latency than expected
Unlike the subscription Activity Log (which typically synced within 
15-30 minutes), AuditLogs took noticeably longer to start appearing — 
this pipeline runs through a different backend than subscription Activity 
Logs. Rather than assume something was broken, I:
- Verified the diagnostic setting was correctly configured (right category, 
  right destination workspace)
- Confirmed via the workspace's Tables list whether AuditLogs existed yet
- Generated a fresh test event (creating a test user) to have something 
  new for the pipeline to pick up
- Waited it out rather than repeatedly re-troubleshooting a correctly 
  configured setting

## Verification
Ran `AuditLogs | take 10` in Sentinel Logs — data returned successfully, 
confirming the pipeline: Entra ID → Diagnostic Setting → SOCAnalyst 
(Log Analytics Workspace) → Microsoft Sentinel.

## Status
✅ Complete — Entra ID AuditLogs connector live and streaming data into 
Microsoft Sentinel. Sign-in Logs remain unavailable due to free-tier 
licensing limitations.
