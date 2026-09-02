# Connecting Azure Activity to Microsoft Sentinel

## Goal
Connect Azure Activity logs (subscription-level admin actions) to my Sentinel 
workspace as my first data source.

## What Azure Activity logs
Azure Activity logs record actions taken at the subscription level — things 
like who created, modified, or deleted a resource, and role/permission changes. 
As a SOC Analyst, this matters because it's often the first place to notice 
suspicious admin behavior, such as someone deleting security resources or 
granting themselves elevated access they shouldn't have.

## Steps I took
1. Went to Microsoft Sentinel > Content Hub, searched for "Azure Activity," 
   and installed the solution.
2. Went to Microsoft Sentinel > Data connectors, opened the Azure Activity 
   connector page to configure it.

## Troubleshooting #1: the diagnostic settings mix-up
Azure has multiple pages that all look similar but do different things:

- **Wrong attempt #1:** I first landed on the Log Analytics workspace's OWN 
  diagnostic settings page (accessed from within the workspace resource itself). 
  This page configures monitoring for the workspace as a resource — things 
  like Audit logs and Job logs about the workspace's own operations — not the 
  subscription's Activity Log.
- **Wrong attempt #2:** I then landed on Monitor > Settings > Diagnostic 
  settings, which lists individual resources (my workspaces, network interface, 
  etc.) to configure diagnostics for. Activity Log isn't in this list because 
  it isn't a regular "resource" — it needed its own dedicated setup path.
- **What worked:** I found the correct path by going to the Activity Log page 
  directly and clicking "Export Activity Logs" in the TOP toolbar (not the 
  left sidebar). This opened a diagnostic settings page scoped specifically 
  to the subscription's Activity Log.

### Key lesson
A resource-level diagnostic setting only captures logs about that specific 
resource's own operations, while a subscription-level diagnostic setting 
captures activity across the whole subscription. For a SOC Analyst, this 
distinction matters a lot — pointing a diagnostic setting at the wrong scope 
means you could think you're monitoring your environment when you're actually 
only seeing a tiny, irrelevant slice of it.

## Mid-project pivot: switching workspaces
Partway through, I had two Log Analytics workspaces active from earlier 
experimentation — "egom" and "SOCAnalyst" — both with Sentinel enabled and 
both receiving diagnostic settings. I decided to standardize on **SOCAnalyst** 
going forward and deleted the diagnostic setting pointing to "egom" to avoid 
duplicate/confusing data. This kept my environment clean and my documentation 
easier to follow.

## Troubleshooting #2: data not appearing immediately
After correctly configuring the diagnostic setting to point to SOCAnalyst, 
running `AzureActivity | take 10` returned no results for about 15-30 minutes. 
This turned out to be normal first-sync latency, not a configuration error — 
I confirmed the diagnostic setting itself was correct (right subscription, 
right workspace, "Administrative" category checked) before concluding it was 
just a timing issue.

To confirm and speed things up, I generated a fresh action (created a new, 
empty resource group) so the Activity Log had something new and timestamped 
to capture. After waiting roughly 15-20 minutes, data appeared successfully.

## Verification
Ran the query `AzureActivity | take 10` in Sentinel Logs. Data returned 
successfully, confirming the pipeline: 
**Azure subscription → Activity Log → Diagnostic Setting → SOCAnalyst 
(Log Analytics Workspace) → Microsoft Sentinel.**

## Status
✅ Complete — Azure Activity connector is live and streaming data into 
Microsoft Sentinel (SOCAnalyst workspace).
