# Cloud SOC Monitoring Lab — Microsoft Sentinel

**A self-built, end-to-end security monitoring environment covering data 
ingestion, detection engineering, incident response, automation, and 
behavioral analytics — built from a beginner starting point with no prior 
hands-on security tooling experience.**

## Overview
This project is a fully functional Security Operations Center (SOC) 
monitoring lab built on Microsoft Sentinel, covering the complete SIEM 
workflow: ingesting real data from multiple source types, detecting 
security-relevant events with custom rules mapped to MITRE ATT&CK, 
investigating and classifying real incidents, automating response actions, 
and applying behavioral (UEBA) detection — all independently researched, 
built, and troubleshot.

## What was built

**Data ingestion (3 source types)**
- Subscription-level: Azure Activity Log
- Host-level: Windows Security Events from a real machine, connected via 
  Azure Arc (hybrid/non-Azure onboarding)
- Identity-level: Microsoft Entra ID Audit Logs

**Detection engineering**
- 2 custom Analytics Rules, each explicitly mapped to a MITRE ATT&CK 
  technique:
  - New User Account Created → T1136 (Persistence)
  - Resource Group Deletion Detected → T1485 (Impact)
- Manual MITRE ATT&CK coverage analysis, including identified detection gaps

**Incident response**
- Multiple real incidents investigated end-to-end: entity review, evidence 
  correlation, and correct classification (Benign Positive vs. False 
  Positive)

**Automation (SOAR)**
- A Playbook (Azure Logic App) that automatically emails incident details 
  on creation, connected via an Automation Rule, with correctly scoped 
  service-identity permissions (least privilege)

**Behavioral detection**
- UEBA enabled, establishing entity behavior baselines for anomaly-based 
  detection alongside signature-based rules

**Visualization & reference data**
- A custom Workbook dashboard summarizing environment activity
- A Watchlist for reference-data-driven query filtering

**Proactive threat hunting**
- Original KQL hunting queries used to investigate and correctly identify 
  unfamiliar service principal activity as benign

## Technologies used
Microsoft Sentinel · Azure Log Analytics · KQL (Kusto Query Language) · 
Azure Arc · Azure Logic Apps · Microsoft Entra ID · Azure Monitor Agent

## Skills demonstrated
- SIEM architecture and configuration
- Log analysis and correlation across heterogeneous data schemas
- Detection engineering mapped to industry frameworks (MITRE ATT&CK)
- Incident investigation and classification
- Security automation (SOAR) with correct identity/permission scoping
- Behavioral/anomaly-based detection concepts (UEBA)
- Independent technical troubleshooting across networking, licensing, 
  encoding, permissions, and platform bugs

## Full documentation
Every step above — including the real errors encountered and how each was 
diagnosed and resolved — is fully documented in 
[`02-siem-microsoft-sentinel/`](./02-siem-microsoft-sentinel/), starting 
with the [capstone summary](./02-siem-microsoft-sentinel/15-siem-fundamentals-capstone.md).
