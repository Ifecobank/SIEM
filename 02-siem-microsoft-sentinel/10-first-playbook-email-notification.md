# Building My First Playbook: Email Notification on New Incidents

## Goal
Build a Playbook (automated response) that sends an email notification 
automatically whenever a new Sentinel incident is created, rather than 
relying on manually checking the Incidents page.

## What is a Playbook
A Playbook is an automated workflow that runs in response to something 
happening in Sentinel — powered under the hood by Azure Logic Apps. While an 
Analytics Rule is responsible for detecting something and creating an 
incident, a Playbook is responsible for what happens next automatically, 
without a human needing to manually take action first. This is the "SOAR" 
(Security Orchestration, Automation, and Response) side of Sentinel — 
turning "we noticed something" into "and here's what we automatically did 
about it," whether that's sending a notification, disabling an account, or 
enriching an incident with extra data.

## What I built
A Logic App (Consumption plan) named `notify-on-new-incident`, with:
- **Trigger:** Microsoft Sentinel incident (fires when a new incident is created)
- **Action:** Send an email (V2) via the Outlook.com connector, using dynamic 
  content to include the incident's Title, Severity, and Description in the 
  email automatically

Then created an Automation Rule ("Trigger email notification") to actually 
connect this Playbook to real incidents — set to trigger on "When incident 
is created" for all incidents, running the Playbook as its action.

## Troubleshooting #1: blocked popup during connector sign-in
The Outlook.com connector required signing in via a popup window, which my 
browser blocked by default. Fixed by allowing popups specifically for 
portal.azure.com and retrying.

## Troubleshooting #2: wrong identity granted permission
When first setting up the Automation Rule, selecting my Playbook under 
"Run playbook" showed a "no Microsoft Sentinel permission" warning. My first 
attempt at fixing this went to the Logic App's Access Control (IAM) and 
added a role assignment — but I nearly granted the role to **my own user 
account** instead of the correct identity.

### Key lesson
The permission needed to belong to **Sentinel's own service identity** 
("Azure Security Insights"), not to me personally — since it's Sentinel's 
automation engine running in the background that needs to invoke the 
Playbook, not a human user. This is a good example of the principle of 
least privilege in practice: permissions should be granted to the specific 
identity that actually performs an action, not broadly to a convenient 
human account. Granting it to myself instead would have meant the 
automation still wouldn't have actually worked, since Sentinel's engine — 
not me — is what triggers the Playbook at run time.

**Fix:** Went to the Logic App > Access control (IAM) > Add role assignment, 
selected role "Microsoft Sentinel Automation Contributor," and this time 
searched for and selected "Azure Security Insights" as the member instead 
of my own account. After this, the playbook became selectable in the 
Automation Rule without the warning.

## Verification
Triggered a fresh incident by creating and immediately deleting a test 
resource group (`test-playbook-trigger`), to confirm the full pipeline: 
AzureActivity → Analytics Rule → Incident created → Automation Rule fires → 
Playbook runs → Email received. Confirmed the notification email arrived 
successfully, containing the incident's Title, Severity, and Description as 
configured.

## Status
✅ Complete — Playbook built, connected via Automation Rule, permissions 
correctly configured, and end-to-end email notification confirmed working 
on a real triggered incident.
