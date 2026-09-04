# SIEM Fundamentals: What I Learned Building a SOC Monitoring Lab

## Why I built this
Starting from zero hands-on experience, my goal was to actually build and 
operate a working SIEM environment — not just read about SIEM concepts, 
but deploy one, connect real data, detect real events, investigate real 
incidents, and automate a real response. This document reflects on what I 
learned across that whole process, using Microsoft Sentinel as my platform.

## The core SIEM workflow, as I actually experienced it

**1. Ingestion** — Getting data INTO the system
I connected three fundamentally different types of data sources: 
subscription-level (Azure Activity), host-level (a real machine via Azure 
Arc, not just a throwaway VM), and identity-level (Entra ID Audit Logs). 
Each had a different connection method, and each taught me something about 
how differently systems represent "the same idea" (e.g., "who did this 
action" was a flat field in one table and a nested JSON object in another).

**2. Detection** — Turning raw data into something actionable
Raw logs are useless without rules to interpret them. I built two custom 
Analytics Rules from scratch, mapped to real MITRE ATT&CK techniques 
(T1136 - Create Account, T1485 - Data Destruction), and learned that 
Sentinel also ships with automatic correlation (Fusion) out of the box.

**3. Investigation** — What happens when something fires
Detecting something isn't the end of the process — I learned to actually 
investigate incidents: checking entities, reviewing underlying evidence, 
using the investigation graph, and correctly classifying outcomes 
(Benign Positive vs. False Positive), which taught me these aren't 
interchangeable labels — they mean different things and drive different 
next steps.

**4. Proactive hunting** — Not waiting for rules to fire
Rules only catch what you thought to write a rule for. My threat hunting 
session taught me to proactively search my own data, and to properly 
investigate unfamiliar identities (two service principal GUIDs) rather 
than dismissing or panicking about them.

**5. Response automation** — Closing the loop
Detection without response is only half the job. Building a Playbook 
taught me the SOAR side of SIEM — and taught me a real lesson about 
permissions: automation needs to run as its OWN identity, not mine, which 
is a genuinely important cloud security principle (least privilege).

**6. Behavioral detection** — Beyond fixed patterns
UEBA showed me a second detection philosophy entirely — not "does this 
match a known bad pattern" but "is this unusual for this specific account." 
Real SOC teams use both approaches together.

**7. Strategic awareness** — Coverage, cost, and context
Mapping my rules to MITRE ATT&CK taught me to think about detection 
*coverage* and *gaps*, not just individual rules in isolation. Reviewing 
real cost/retention data taught me that logging everything forever isn't 
actually how real environments operate — there are always tradeoffs.

## The most important thing I learned
It wasn't any single feature — it was that **troubleshooting IS the job**. 
Nearly every entry in this journey involved something breaking: wrong 
diagnostic settings scope, blocked popups, wrong file encoding, wrong 
identity granted permissions, a broken Preview feature, licensing walls I 
had to work around. A real SOC Analyst doesn't get a clean, pre-solved 
environment — they get exactly this: things that don't work the first 
time, and the job is figuring out why.

## What I'd tell someone starting this same journey
Expect almost nothing to work perfectly on the first try — that's normal, 
not a sign you're doing something wrong. I started as a complete beginner 
with no cybersecurity background, and nearly every single step in this 
repo involved an error message, a confusing UI, or a wrong assumption I had 
to correct. The progress didn't come from avoiding mistakes — it came from 
slowing down, checking one thing at a time, and writing down what actually 
fixed each problem. If you're starting exactly where I started: don't wait 
until you feel "ready" to build something real. Build it now, break it, and 
document the breaking — that's the part that actually teaches you, and it's 
also the part that makes your work worth showing to someone else.

## What's next
This lab covered Microsoft Sentinel in depth. My next step is learning 
Splunk — a different platform with a different philosophy — to build 
cross-platform SIEM fluency rather than single-vendor knowledge.

---
*This summary reflects hands-on work across 14 documented entries in this 
repository, each with full technical detail and real troubleshooting 
preserved.*
