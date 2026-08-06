# SOC Detection & Response Platform

A home-lab Security Operations Center (SOC) built to practice blue team / detection engineering skills - using Wazuh, the Elastic Stack, Sigma rules, and MITRE ATT&CK-mapped attack simulations.

## What this project does

You build a mini alarm system (Wazuh + Elastic), teach it what to look for (Sigma detection rules), then safely simulate real attacker behavior to prove the alarm actually works — and map every detection back to the industry-standard MITRE ATT&CK framework to show exactly what's covered.

## Outcome

By the end of this project, the platform can:
- Detect a simulated attack (e.g. credential dumping, brute force, privilege escalation) against a vulnerable lab target
- Surface that detection in real time on a Kibana/Wazuh dashboard
- Identify which MITRE ATT&CK technique the attack maps to (e.g. `T1003 – OS Credential Dumping`)
- Show a coverage map of which attack techniques the SOC can and can't currently detect
- Point to the specific Sigma rule behind each detection and explain why it fires

## Architecture

| VM | Role | OS | RAM | Purpose |
|---|---|---|---|---|
| SOC Server | Detection & monitoring backend | Ubuntu Server 22.04 LTS | 6GB | Runs Wazuh + Elastic Stack via Docker |
| Attacker | Threat simulation | Kali Linux 2025.1 | 2GB | Launches simulated attacks |
| Victim | Monitored target | Metasploitable2 | 512MB | Intentionally vulnerable system, generates real attack telemetry |

All VMs run on VMware Workstation 17 Player, on a shared virtual network.

## Build log

Each phase of the build, including issues hit and how they were resolved, is documented in `/docs`:

- [`01-environment-setup.md`](docs/01-environment-setup.md) — VM setup, networking, Docker install
- [`02-wazuh-installation.md`](docs/02-wazuh-installation.md) — Wazuh + Elastic Stack deployment
- `03-victim-connection.md` — *(coming soon)*
- `04-sigma-rules.md` — *(coming soon)*
- `05-attack-simulation.md` — *(coming soon)*
- `06-mitre-attack-mapping.md` — *(coming soon)*

## Tools used

- [Wazuh](https://wazuh.com/) — detection engine, log analysis, alerting
- [Elastic Stack](https://www.elastic.co/elastic-stack) — data storage and visualization (Kibana-based)
- [Sigma rules](https://github.com/SigmaHQ/sigma) — vendor-agnostic detection rule format
- [MITRE ATT&CK](https://attack.mitre.org/) — attack technique reference framework
- Metasploitable2 / Kali Linux — vulnerable target and attack simulation

## Status

🚧 In progress — Phases 1 & 2 complete.
