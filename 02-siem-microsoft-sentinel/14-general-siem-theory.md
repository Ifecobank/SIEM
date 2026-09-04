# General SIEM Theory & Industry Landscape

## Goal
Build a solid conceptual foundation of SIEM theory — terminology, related 
technologies, and industry landscape — so I can speak confidently about 
these concepts in interviews, independent of any single tool.

## What is a SIEM, precisely
A SIEM (Security Information and Event Management) is a system that 
collects log/event data from across an organization's systems, correlates 
that data to identify meaningful patterns, and enables detection, 
investigation, and response to security threats — essentially a 
centralized "system of record" for security-relevant activity. This 
matches exactly what I built with Microsoft Sentinel: multiple data 
sources → correlation via Analytics Rules → investigation via Incidents.

## SIEM vs. SOAR vs. XDR vs. EDR
These terms are often confused, but they cover different (sometimes 
overlapping) parts of a security stack:

| Term | Full name | What it actually does |
|---|---|---|
| **SIEM** | Security Information and Event Management | Collects and correlates log data across the environment; the "system of record" |
| **SOAR** | Security Orchestration, Automation, and Response | Automates response actions (e.g., my email Playbook); often built into modern SIEMs rather than separate |
| **XDR** | Extended Detection and Response | Similar goal to SIEM but usually more tightly integrated/vendor-specific across endpoint, email, identity, cloud — trades some flexibility for deeper native integration |
| **EDR** | Endpoint Detection and Response | Focused specifically on endpoints (laptops, servers) — deep visibility into processes, file activity, and behavior on individual machines |

A simple way I think about it: EDR is endpoint-specific, SIEM is 
environment-wide log correlation, SOAR is the automation layer, and XDR is 
a more tightly-integrated evolution that often bundles several of these 
together under one vendor.

## Core SIEM concepts
- **Log normalization:** Different systems log the same type of event in 
  different formats/field names. Normalization maps these into a 
  consistent schema so they can be queried and correlated together — I saw 
  this directly when AzureActivity's flat `Caller` field and AuditLogs' 
  nested `InitiatedBy` JSON structured the "who did this" information 
  completely differently.
- **Correlation:** Connecting related events (possibly from different 
  sources) into a single meaningful pattern — this is what Analytics Rules 
  do, and what Sentinel's built-in "Advanced Multistage Attack Detection" 
  (Fusion) does automatically across data sources.
- **Retention:** How long log data remains queryable — directly tied to 
  cost, as I covered in my cost/data volume entry.

## Industry landscape (as of late 2025 Gartner Magic Quadrant)
Current recognized leaders in the SIEM market include Microsoft, IBM, 
Splunk, Securonix, and Exabeam, with other notable vendors including 
Elastic, LogRhythm, Google (Chronicle), Rapid7, and Graylog (a newer 
entrant recognized for the first time in 2025). This is a genuinely 
competitive, fast-evolving market — worth knowing the names even without 
hands-on experience with all of them, since interviewers may reference 
them by name.

## Why I'm doing Splunk next
Microsoft and Splunk are both recognized market leaders, but they represent 
genuinely different approaches — Sentinel is cloud-native and deeply tied 
into the Azure ecosystem, while Splunk is platform-agnostic and widely used 
across on-premises and multi-cloud environments regardless of vendor. 
Learning both isn't just "another tool on a resume" — it shows I understand 
SIEM concepts well enough to transfer them across different platforms, 
rather than only knowing how to follow one vendor's specific UI. Many job 
postings list either Sentinel or Splunk (or both) as requirements, so 
having real experience with both broadens what roles I can credibly apply 
for.

## Status
✅ Complete — built a working conceptual vocabulary for SIEM-adjacent terms 
and the current industry landscape, grounded in what I actually built with 
Sentinel.
