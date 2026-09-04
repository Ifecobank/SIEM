# Cost & Data Volume Awareness

## Goal
Understand how Microsoft Sentinel/Log Analytics billing actually works, and 
check my own environment's real usage — a practical operational skill, not 
just a detection skill.

## How Sentinel/Log Analytics billing works
Cost is driven mainly by two things: how much data gets **ingested** (sent 
into the workspace, measured in GB) and how long that data is **retained** 
(kept available for querying, measured in days). More data sources, more 
verbose logging, and longer retention all increase cost. A large 
organization can't just "log everything forever" because ingestion volume 
scales with the size of the environment — thousands of devices and users 
generating logs 24/7 can produce enormous daily volumes, and storing years 
of that data indefinitely becomes very expensive very quickly. This is why 
real organizations make deliberate choices about what to log, how verbosely, 
and for how long, rather than defaulting to maximum logging everywhere.

## My environment's actual usage
- **Total data ingested:** ~10 MB
- **Data retention:** 31 days

This is a very small footprint, reflecting a lab environment with a handful 
of test events rather than a live production environment with real user 
traffic, which would generate significantly more data — often measured in 
GB or TB per day rather than MB total.

## Why this matters for a SOC Analyst
Even though analysts usually aren't the ones setting retention or billing 
policy, understanding these constraints affects real investigative work. If 
retention is only 31 or 90 days, an analyst investigating something that 
happened further back may find the data simply isn't there anymore — which 
changes what's actually possible during an investigation. Similarly, 
knowing that ingestion costs money helps explain why some data sources get 
filtered or excluded in real environments, which in turn explains why 
certain attack patterns might have blind spots — not because no one thought 
of them, but because of a cost/coverage tradeoff made upstream.

## Practical cost-management concepts (research-based)
Even without a large-scale environment to test this on directly, these are 
real practices organizations use to manage SIEM costs:
- **Filtering noisy/low-value log sources** before ingestion, rather than 
  sending everything
- **Tiered retention** — keeping recent data in fast/expensive storage, 
  older data in cheaper archive tiers
- **Data collection rules** that only capture specific event types (similar 
  to the "Common" event set I chose when onboarding my host machine, 
  instead of capturing everything)

## Status
✅ Complete — reviewed real usage/retention data in my own environment, and 
researched practical cost-management concepts used in production SIEM 
deployments.
