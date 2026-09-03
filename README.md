# Microsoft Sentinel — Learning Journey

This folder documents my hands-on journey learning Microsoft Sentinel as part 
of my path toward becoming a SOC Analyst. Each file below covers a specific 
milestone, including the real troubleshooting I worked through along the way.

## 📚 Contents

| File | What it covers |
|---|---|
| [`00-what-is-siem.md`](./00-what-is-siem.md) | Core concepts: what a SIEM is and why it matters |
| [`02-connecting-azure-activity.md`](./02-connecting-azure-activity.md) | Connecting Azure Activity logs; troubleshooting diagnostic settings scope confusion |
| [`03-onboarding-host-via-arc.md`](./03-onboarding-host-via-arc.md) | Connecting a non-Azure host machine via Azure Arc; troubleshooting a PowerShell download failure |
| [`04-first-analytics-rule-and-incident.md`](./04-first-analytics-rule-and-incident.md) | Building a custom detection rule; investigating and closing real incidents |
| [`05-connecting-entra-id-auditlogs.md`](./05-connecting-entra-id-auditlogs.md) | Connecting Entra ID Audit Logs; working around a free-tier licensing limitation |
| [`06-second-analytics-rule-new-user.md`](./06-second-analytics-rule-new-user.md) | Second detection rule (new user creation); handling nested JSON fields and finding exact operation names |

## 🧠 Key skills demonstrated
- Deploying and configuring a Log Analytics Workspace and Microsoft Sentinel
- Connecting multiple data source types (subscription-level, host-level, identity-level)
- Writing and testing KQL (Kusto Query Language) queries, including nested JSON field extraction
- Building custom Analytics Rules with entity mapping across different data schemas
- Investigating, classifying, and closing security incidents
- Real-world troubleshooting: diagnostic setting misconfigurations, agent 
  installation failures, licensing constraints, and pipeline latency differences

## 🔍 A note on troubleshooting
I've intentionally kept the troubleshooting sections in each file, even the 
messy parts — I think showing how a problem was diagnosed and solved is more 
valuable than just showing the "happy path." Real SOC and cloud work involves 
constant troubleshooting, and I wanted this repo to reflect that honestly.

## ⏭️ What's next
- Threat hunting queries using KQL
- More diverse Analytics Rules (e.g., failed login patterns, privilege escalation)
- (Planned) Splunk — a second SIEM platform, to compare approaches

## 🛠️ Environment notes
- SIEM: Microsoft Sentinel
- Primary Log Analytics workspace: `SOCAnalyst`
- Data sources connected: Azure Activity, Windows Security Events (via Azure Arc), Entra ID Audit Logs
