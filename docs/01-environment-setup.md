# Phase 1: Environment Setup

## Overview
This SOC lab simulates a small-scale Security Operations Center using three virtual machines on a single host laptop (Windows, 16GB RAM), managed with VMware Workstation 17 Player.

## Lab Architecture

| VM | Role | OS | RAM | Purpose |
|---|---|---|---|---|
| SOC Server | Detection & monitoring backend | Ubuntu Server 22.04 LTS | 6GB | Runs Wazuh + Elastic Stack (via Docker) |
| Attacker | Threat simulation | Kali Linux 2025.1 | 2GB | Launches attack simulations against the victim |
| Victim | Monitored target | Metasploitable2 | 512MB | Intentionally vulnerable system that generates real attack telemetry |

All three VMs run on the same virtual network (bridged), allowing them to communicate as if on a shared LAN.

## Why this setup
This mirrors the minimum components of a real SOC:
- A central monitoring/detection platform (SOC server)
- A source of malicious activity to detect (attacker)
- A monitored asset that could realistically be compromised (victim)

Using Metasploitable2 and Kali instead of a Windows victim kept the lab lightweight and avoided a large Windows ISO download, while still providing a realistic, intentionally vulnerable target.

## Setup steps

1. **Hypervisor**: VMware Workstation 17 Player (non-commercial use), already installed
2. **SOC server VM**: Ubuntu Server 22.04.3 LTS ("jammy"), initially provisioned with a 20GB virtual disk and 4GB RAM
3. **Networking verification**: Confirmed internet access inside the Ubuntu VM. Hit an initial DNS resolution failure:
