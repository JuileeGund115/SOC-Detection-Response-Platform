# Phase 2: Wazuh + Elastic Stack Installation

## Overview
Wazuh (manager, indexer, and dashboard) was deployed on the Ubuntu SOC server VM using Wazuh's official Docker Compose single-node configuration, which bundles all three components together.

## Steps

1. Cloned the official Wazuh Docker repository (v4.9.0):
```bash
   git clone https://github.com/wazuh/wazuh-docker.git -b v4.9.0
   cd wazuh-docker/single-node
```

2. Applied a required kernel parameter for the OpenSearch-based indexer to run reliably:
```bash
   sudo sysctl -w vm.max_map_count=262144
   echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf
```

3. Launched the stack:
```bash
   docker compose up -d
```

   This deploys three containers:
   - `wazuh.manager` — core detection engine, rule evaluation
   - `wazuh.indexer` — OpenSearch-based data store for events/alerts
   - `wazuh.dashboard` — web UI for visualizing alerts

## Issue encountered: dashboard crash loop (EISDIR error)

**Problem**: The first deployment attempt ran out of disk space mid-download (see `01-environment-setup.md`). After the disk was expanded and the stack relaunched, the dashboard container repeatedly crashed with:

