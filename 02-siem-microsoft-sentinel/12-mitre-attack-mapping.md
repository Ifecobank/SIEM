# MITRE ATT&CK Coverage Mapping

## Goal
Map my existing Analytics Rules to official MITRE ATT&CK techniques, to 
understand detection coverage the way a real SOC team would — not just 
"what does this rule do" but "which specific attacker technique does this 
actually detect."

## Troubleshooting: Sentinel's built-in MITRE ATT&CK page failed to load
Sentinel has a built-in "MITRE ATT&CK (Preview)" page meant to visualize 
this automatically, but it consistently failed with a script loading 
timeout error (`Manual require of the following modules failed... script 
timeout`). I tried refreshing, hard-refreshing, and switching browsers, but 
the error persisted — this appears to be a temporary issue with this 
specific Preview feature on Microsoft's side, not a configuration problem 
on mine.

### Key lesson
When a specific tool or feature is broken and outside my control, the 
better move is to accomplish the same underlying goal a different way 
rather than getting stuck waiting for it to be fixed. Real analysts don't 
always have every dashboard working perfectly — knowing how to fall back to 
manual research (in this case, directly referencing MITRE's own technique 
documentation) is itself a useful skill.

## My manual mapping
Since the built-in visualization wasn't available, I mapped my rules 
manually by researching the official MITRE ATT&CK technique definitions.

| My Analytics Rule | Tactic | Technique | Technique ID |
|---|---|---|---|
| New User Account Created | Persistence | Create Account (Cloud Account) | T1136 / T1136.003 |
| Resource Group Deletion Detected | Impact | Data Destruction | T1485 |

**T1136 (Create Account):** Adversaries create accounts to maintain access 
to a victim's systems, often as backup access that doesn't require ongoing 
use of an initially compromised account. The cloud-specific sub-technique 
(T1136.003) specifically covers creating accounts within a cloud tenant 
like Entra ID — directly matching what my rule detects.

**T1485 (Data Destruction):** Adversaries destroy data/infrastructure to 
disrupt availability. MITRE's own documentation explicitly calls out cloud 
environments, noting adversaries may delete cloud storage, accounts, or 
other infrastructure to damage an organization — directly matching a 
resource group deletion scenario.

## Coverage gap awareness
With only two rules, my coverage is intentionally narrow — I'm covering 
exactly two techniques out of MITRE's hundreds. Some obvious gaps in my 
current environment:
- **Initial Access** (e.g., T1078 - Valid Accounts / suspicious sign-ins) — 
  not yet covered, though I do have Entra ID Sign-in Logs unavailable due 
  to licensing, which limits this
- **Privilege Escalation** (e.g., role/permission changes) — not yet covered
- **Defense Evasion** (e.g., log/audit tampering) — not yet covered

### Key lesson
Thinking in terms of gaps rather than just "rules I've built" is what 
separates checkbox-style detection from real coverage strategy. A SOC 
analyst's job isn't just knowing their existing rules work — it's knowing 
what an attacker could still do that nothing would catch, and using that 
awareness to prioritize what to build next.

## Status
✅ Complete — manually mapped current rules to official MITRE ATT&CK 
techniques; noted the Sentinel Preview UI bug encountered along the way, 
and identified coverage gaps for future rule-building.
