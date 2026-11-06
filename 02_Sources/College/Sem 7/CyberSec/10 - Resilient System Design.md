---
Source: IF4033 - Cyber Security
Topic: Security Architecture
Date: 2026-11-02
---

## Raw
**Cysec vs Resilience**
- Cybersecurity: prevention based
- Resilience: accepts breaches will happen, reduce impact

**Case study**
- GitlLab.com 2017
- `rm -rf` on the wrong server, causing production data deletion
- They have backups
	- Data is fine, but, restorin from backups are way longer than deleting the data
	- Additionally, backups can be **wrong**, meaning you backup with incorrect setup.

**Business Impact Analysis (BIA)**
- A process to determine:
	- Which systems and functions are critical
	- The impact of their disruption (financial, reputation, regulation)
	- How fast recovery must happen (RTO)
	- How stale should the data be to be acceptable (RPO)
- Processes
	- Dependency mapping
	- RPO and RTO
		- RTO $\leq$ MTD (max. tolerable disruption)
	- Recovery tiers
		- Active-active
		- Hot standby
		- Cold standby
		- Backup only
	- Backup types
		- Full
		- Differential
		- Incremental
	- 3-2-1-1-0 Rule
		- Atleast:
		- 3 copies
		- 2 media types
		- 1 offsite copy
		- 1 offline and immutable
		- 0 backup errors

**Cloud Native Continuity**
- Continuity involves saving or backing up data to be able to be restored later when needed.
- When backups are compromised:
	- 3-2-1-1-0 does not defend attackers

**High Availability vs Disaster Recovery**
- HA - component, DR - site level
- DR is on site, like data centers safety

## Key Snippets / Equations
-