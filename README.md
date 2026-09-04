📖 **Start here:** [SIEM Fundamentals — What I Learned](./15-siem-fundamentals-capstone.md)
# Microsoft Sentinel — Learning Journey

This folder documents my hands-on journey learning Microsoft Sentinel as part 
of my path toward becoming a SOC Analyst. Each file below covers a specific 
milestone, including the real troubleshooting I worked through along the way.

📖 **New here? Start with the [SIEM Fundamentals capstone summary](./15-siem-fundamentals-capstone.md)** for a full reflection tying everything below together.

## 📚 Contents

| File | What it covers |
|---|---|
| [`00-what-is-siem.md`](./00-what-is-siem.md) | Core concepts: what a SIEM is and why it matters |
| [`02-connecting-azure-activity.md`](./02-connecting-azure-activity.md) | Connecting Azure Activity logs; troubleshooting diagnostic settings scope confusion |
| [`03-onboarding-host-via-arc.md`](./03-onboarding-host-via-arc.md) | Connecting a non-Azure host machine via Azure Arc; troubleshooting a PowerShell download failure |
| [`04-first-analytics-rule-and-incident.md`](./04-first-analytics-rule-and-incident.md) | Building a custom detection rule; investigating and closing real incidents |
| [`05-connecting-entra-id-auditlogs.md`](./05-connecting-entra-id-auditlogs.md) | Connecting Entra ID Audit Logs; working around a free-tier licensing limitation |
| [`06-second-analytics-rule-new-user.md`](./06-second-analytics-rule-new-user.md) | Second detection rule (new user creation); handling nested JSON fields and finding exact operation names |
| [`07-threat-hunting-session-1.md`](./07-threat-hunting-session-1.md) | First proactive threat hunting session; investigating unfamiliar service principal identities |
| [`08-first-workbook.md`](./08-first-workbook.md) | Building a Sentinel Workbook (dashboard) to visualize environment activity |
| [`09-watchlist-monitored-accounts.md`](./09-watchlist-monitored-accounts.md) | Building a Watchlist for account monitoring; troubleshooting CSV file encoding issues |
| [`10-first-playbook-email-notification.md`](./10-first-playbook-email-notification.md) | Building a Playbook (SOAR automation) for email notifications; fixing a service identity permission issue |
| [`11-enabling-ueba.md`](./11-enabling-ueba.md) | Enabling User and Entity Behavior Analytics; clarifying a misleading prerequisite warning |
| [`12-mitre-attack-mapping.md`](./12-mitre-attack-mapping.md) | Manually mapping Analytics Rules to MITRE ATT&CK techniques; working around a broken Preview feature |
| [`13-cost-data-volume-awareness.md`](./13-cost-data-volume-awareness.md) | Understanding SIEM billing, data ingestion, and retention using real environment data |
| [`14-general-siem-theory.md`](./14-general-siem-theory.md) | SIEM vs SOAR vs XDR vs EDR, core concepts, and the current industry landscape |
| [`15-siem-fundamentals-capstone.md`](./15-siem-fundamentals-capstone.md) | Capstone summary reflecting on the full journey documented in this folder |

## 🧠 Key skills demonstrated
- Deploying and configuring a Log Analytics Workspace and Microsoft Sentinel
- Connecting multiple data source types (subscription-level, host-level, identity-level)
- Writing and testing KQL (Kusto Query Language) queries, including nested JSON field extraction
- Building custom Analytics Rules with entity mapping across different data schemas
- Investigating, classifying, and closing security incidents
- Proactive threat hunting — writing original exploratory queries and investigating unfamiliar identities
- Building Workbooks (dashboards) to visualize environment activity
- Building and integrating Watchlists as reusable reference data in KQL queries
- Building Playbooks (SOAR automation) with Logic Apps, including service identity permissions
- Enabling and understanding UEBA (behavioral/anomaly-based detection)
- Mapping detections to MITRE ATT&CK techniques and identifying coverage gaps
- Understanding SIEM cost/data volume tradeoffs
- General SIEM theory: SIEM vs SOAR vs XDR vs EDR, industry landscape
- Real-world troubleshooting: diagnostic setting misconfigurations, agent 
  installation failures, licensing constraints, pipeline latency differences, 
  KQL syntax debugging, file encoding issues, cloud service permissions, and 
  broken Preview features

## 🔍 A note on troubleshooting
I've intentionally kept the troubleshooting sections in each file, even the 
messy parts — I think showing how a problem was diagnosed and solved is more 
valuable than just showing the "happy path." Real SOC and cloud work involves 
constant troubleshooting, and I wanted this repo to reflect that honestly.

## ⏭️ What's next
- (Planned) Splunk — a second SIEM platform, to compare approaches

## 🛠️ Environment notes
- SIEM: Microsoft Sentinel
- Primary Log Analytics workspace: `SOCAnalyst`
- Data sources connected: Azure Activity, Windows Security Events (via Azure Arc), Entra ID Audit Logs
