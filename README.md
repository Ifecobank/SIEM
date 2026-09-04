📖 **Start here:** [SIEM Fundamentals — What I Learned](./02-siem-microsoft-sentinel/15-siem-fundamentals-capstone.md)
# Microsoft Sentinel — Learning Journey

This folder documents my hands-on journey learning Microsoft Sentinel as part 
of my path toward becoming a SOC Analyst. Each file below covers a specific 
milestone, including the real troubleshooting I worked through along the way.

📖 **New here? Start with the [SIEM Fundamentals capstone summary](./02-siem-microsoft-sentinel/15-siem-fundamentals-capstone.md)** for a full reflection tying everything below together.

## 📚 Contents

| File | What it covers |
|---|---|
| [`00-what-is-siem.md`](./02-siem-microsoft-sentinel/00-what-is-siem.md) | Core concepts: what a SIEM is and why it matters |
| [`02-connecting-azure-activity.md`](./02-siem-microsoft-sentinel/02-connecting-azure-activity.md) | Connecting Azure Activity logs; troubleshooting diagnostic settings scope confusion |
| [`03-onboarding-host-via-arc.md`](./02-siem-microsoft-sentinel/03-onboarding-host-via-arc.md) | Connecting a non-Azure host machine via Azure Arc; troubleshooting a PowerShell download failure |
| [`04-first-analytics-rule-and-incident.md`](./02-siem-microsoft-sentinel/04-first-analytics-rule-and-incident.md) | Building a custom detection rule; investigating and closing real incidents |
| [`05-connecting-entra-id-auditlogs.md`](./02-siem-microsoft-sentinel/05-connecting-entra-id-auditlogs.md) | Connecting Entra ID Audit Logs; working around a free-tier licensing limitation |
| [`06-second-analytics-rule-new-user.md`](./02-siem-microsoft-sentinel/06-second-analytics-rule-new-user.md) | Second detection rule (new user creation); handling nested JSON fields and finding exact operation names |
| [`07-threat-hunting-session-1.md`](./02-siem-microsoft-sentinel/07-threat-hunting-session-1.md) | First proactive threat hunting session; investigating unfamiliar service principal identities |
| [`08-first-workbook.md`](./02-siem-microsoft-sentinel/08-first-workbook.md) | Building a Sentinel Workbook (dashboard) to visualize environment activity |
| [`09-watchlist-monitored-accounts.md`](./02-siem-microsoft-sentinel/09-watchlist-monitored-accounts.md) | Building a Watchlist for account monitoring; troubleshooting CSV file encoding issues |
| [`10-first-playbook-email-notification.md`](./02-siem-microsoft-sentinel/10-first-playbook-email-notification.md) | Building a Playbook (SOAR automation) for email notifications; fixing a service identity permission issue |
| [`11-enabling-ueba.md`](./02-siem-microsoft-sentinel/11-enabling-ueba.md) | Enabling User and Entity Behavior Analytics; clarifying a misleading prerequisite warning |
| [`12-mitre-attack-mapping.md`](./02-siem-microsoft-sentinel/12-mitre-attack-mapping.md) | Manually mapping Analytics Rules to MITRE ATT&CK techniques; working around a broken Preview feature |
| [`13-cost-data-volume-awareness.md`](./02-siem-microsoft-sentinel/13-cost-data-volume-awareness.md) | Understanding SIEM billing, data ingestion, and retention using real environment data |
| [`14-general-siem-theory.md`](./02-siem-microsoft-sentinel/14-general-siem-theory.md) | SIEM vs SOAR vs XDR vs EDR, core concepts, and the current industry landscape |
| [`15-siem-fundamentals-capstone.md`](./02-siem-microsoft-sentinel/15-siem-fundamentals-capstone.md) | Capstone summary reflecting on the full journey documented in this folder |
