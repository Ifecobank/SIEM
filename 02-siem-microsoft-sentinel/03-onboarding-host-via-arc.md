# Onboarding My Host Machine to Sentinel via Azure Arc

## Goal
Connect my personal Windows host machine (not an Azure VM) to Microsoft Sentinel, 
so I can analyze real, everyday security event data instead of relying on an 
idle test VM.

## Why Azure Arc
Sentinel data connectors like "Windows Security Events via AMA" are designed 
for Azure resources. Since my host machine isn't hosted in Azure, it needs to 
be registered as an Azure resource first — this is what Azure Arc does. Once 
Arc-enabled, a non-Azure machine can be treated like any other Azure resource 
for monitoring and management purposes.

This is also realistic, job-relevant experience — many organizations use Azure 
Arc to bring on-premises and hybrid machines under centralized security 
monitoring.

## Steps I took
1. Went to Azure Arc > Servers > Add a machine, generated a Windows onboarding 
   script through the portal wizard.
2. Downloaded and ran the script in PowerShell (as Administrator) on my host 
   machine.

## Troubleshooting: script download failure (400 Bad Request)
The onboarding script failed at a specific line — downloading the actual agent 
installer script via `Invoke-WebRequest`, with a `400 Bad Request` error.

**What I ruled out:**
- Regenerated a completely fresh script — same error, so it wasn't a stale/expired script.
- Ran `Test-NetConnection` against the target endpoint on port 443 — succeeded, 
  ruling out a basic network/firewall block.
- Opened the exact same URL directly in my browser — it loaded fine and 
  returned the actual script content, confirming the server and URL were healthy.

**Conclusion:** The issue was isolated to how PowerShell's `Invoke-WebRequest` 
specifically was making that one request — not a network or account problem.

**Workaround:** Instead of relying on the automated bootstrap script, I:
1. Manually downloaded the Azure Connected Machine Agent installer (.msi) directly.
2. Installed it like a normal Windows program.
3. Ran `azcmagent connect` manually via PowerShell, passing in my subscription ID, 
   tenant ID, resource group, and region directly as parameters.

This bypassed the failing download step entirely while still completing the 
same registration process.

### Follow-up hiccup: 'azcmagent' not recognized
After installing the agent, running `azcmagent connect` immediately failed with 
"term not recognized." This was simply because my existing PowerShell window 
hadn't refreshed its PATH environment variable after the install. Closing and 
reopening a fresh Administrator PowerShell window resolved it immediately.

### Key lesson
When a script fails at a specific step, it's worth isolating *exactly* which 
part is failing (network vs. server vs. client tool) rather than assuming the 
whole process is broken. Testing the same URL through a different method 
(browser vs. PowerShell) was the key step that revealed this was a tool-specific 
issue, not a real connectivity problem.

## Verification
Confirmed the machine appeared as "Connected" in Azure Arc > Servers. Then 
created a Data Collection Rule in Sentinel targeting this Arc-enabled machine, 
and ran `SecurityEvent | take 10` in Sentinel Logs to confirm data ingestion.

## Status
✅ Complete — host machine connected via Azure Arc and streaming Security 
Events into Microsoft Sentinel (SOCAnalyst workspace).
