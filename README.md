<!-- BlackRoad SEO Enhanced -->

# esp32 live portfolio

> Part of **[BlackRoad OS](https://blackroad.io)** — Sovereign Computing for Everyone

[![BlackRoad OS](https://img.shields.io/badge/BlackRoad-OS-ff1d6c?style=for-the-badge)](https://blackroad.io)
[![BlackRoad Studio](https://img.shields.io/badge/Org-BlackRoad-Studio-2979ff?style=for-the-badge)](https://github.com/BlackRoad-Studio)
[![License](https://img.shields.io/badge/License-Proprietary-f5a623?style=for-the-badge)](LICENSE)

**esp32 live portfolio** is part of the **BlackRoad OS** ecosystem — a sovereign, distributed operating system built on edge computing, local AI, and mesh networking by **BlackRoad OS, Inc.**

## About BlackRoad OS

BlackRoad OS is a sovereign computing platform that runs AI locally on your own hardware. No cloud dependencies. No API keys. No surveillance. Built by [BlackRoad OS, Inc.](https://github.com/BlackRoad-OS-Inc), a Delaware C-Corp founded in 2025.

### Key Features
- **Local AI** — Run LLMs on Raspberry Pi, Hailo-8, and commodity hardware
- **Mesh Networking** — WireGuard VPN, NATS pub/sub, peer-to-peer communication
- **Edge Computing** — 52 TOPS of AI acceleration across a Pi fleet
- **Self-Hosted Everything** — Git, DNS, storage, CI/CD, chat — all sovereign
- **Zero Cloud Dependencies** — Your data stays on your hardware

### The BlackRoad Ecosystem
| Organization | Focus |
|---|---|
| [BlackRoad OS](https://github.com/BlackRoad-OS) | Core platform and applications |
| [BlackRoad OS, Inc.](https://github.com/BlackRoad-OS-Inc) | Corporate and enterprise |
| [BlackRoad AI](https://github.com/BlackRoad-AI) | Artificial intelligence and ML |
| [BlackRoad Hardware](https://github.com/BlackRoad-Hardware) | Edge hardware and IoT |
| [BlackRoad Security](https://github.com/BlackRoad-Security) | Cybersecurity and auditing |
| [BlackRoad Quantum](https://github.com/BlackRoad-Quantum) | Quantum computing research |
| [BlackRoad Agents](https://github.com/BlackRoad-Agents) | Autonomous AI agents |
| [BlackRoad Network](https://github.com/BlackRoad-Network) | Mesh and distributed networking |
| [BlackRoad Education](https://github.com/BlackRoad-Education) | Learning and tutoring platforms |
| [BlackRoad Labs](https://github.com/BlackRoad-Labs) | Research and experiments |
| [BlackRoad Cloud](https://github.com/BlackRoad-Cloud) | Self-hosted cloud infrastructure |
| [BlackRoad Forge](https://github.com/BlackRoad-Forge) | Developer tools and utilities |

### Links
- **Website**: [blackroad.io](https://blackroad.io)
- **Documentation**: [docs.blackroad.io](https://docs.blackroad.io)
- **Chat**: [chat.blackroad.io](https://chat.blackroad.io)
- **Search**: [search.blackroad.io](https://search.blackroad.io)

---


**The World's First Hardware Portfolio** - Real-time data on every screen, live from production systems.

## Overview

Transform your ESP32-2432S028R into a CEO dashboard that displays:

- **GitHub** - 199+ repos across 15 organizations, PRs, issues, stars
- **Crypto** - BTC, ETH, SOL prices with portfolio tracking
- **CRM** - Hot leads, pipeline value, deals from EspoCRM
- **Infrastructure** - Server health, VPN nodes, sovereignty score
- **AI** - vLLM inference stats, 30,000 agent orchestration
- **Weather** - 5-day forecast with live updates
- **Emergency Pager** - Compliance-grade alerting system

## Apps (20 Touch-Interactive Screens)

| App | Screen | Description |
|-----|--------|-------------|
| CEO | CEO Core | 3×3 executive dashboard |
| EXEC | Exec Grid | 4×4 extended metrics |
| META | Meta | Aggregate all app data |
| WORK | Workflow | Universal Emoji Library |
| AI | AI Inference | vLLM/LocalAI stats |
| MSG | Messages | BlackRoad Messages |
| CRM | CRM | EspoCRM integration |
| VPN | Mesh VPN | Headscale status |
| ID | Identity | Keycloak SSO |
| FILE | Files | File manager |
| API | APIs | API management |
| SET | Settings | System settings |
| CC | Control Center | Quick settings |
| CHAT | Chat | BlackRoad AI Chat |
| TERM | Terminal | Command interface |
| PAGER | Pager | Emergency alerts |
| WX | Weather | 5-day forecast |
| GIT | GitHub | Repo stats, PRs |
| LIN | Linear | Task tracking |

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        DATA SOURCES                              │
├─────────────────────────────────────────────────────────────────┤
│  GitHub API    Cloudflare API    Railway API    Stripe API      │
│  (15 orgs)     (16 zones)        (12 projects)  (revenue)       │
│                                                                  │
│  Linear API    EspoCRM API       Prometheus     Headscale       │
│  (tasks)       (leads/deals)     (metrics)      (VPN nodes)     │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                   AGGREGATOR API (Cloudflare Worker)            │
│  • Polls all APIs every 30-60 seconds                           │
│  • Caches in Cloudflare KV                                      │
│  • Single unified JSON endpoint                                 │
│  Endpoint: https://api.blackroad.io/v1/live-hub                 │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                      ESP32 CEO HUB                               │
│  • Fetches /live-hub every 30 seconds                           │
│  • Parses JSON with ArduinoJson                                 │
│  • Updates all screens with fresh data                          │
│  • Shows LIVE indicator when data < 60s old                     │
└─────────────────────────────────────────────────────────────────┘
```

## Hardware

- **Device:** ESP32-2432S028R (Cheap Yellow Display)
- **Display:** 320x240 ILI9341 TFT
- **Touch:** XPT2046 resistive
- **Connection:** USB-C (CH340 serial)

## Quick Start

1. **Clone & Setup**
```bash
git clone https://github.com/BlackRoad-OS/esp32-live-portfolio.git
cd esp32-live-portfolio
cp firmware/src/secrets.h.example firmware/src/secrets.h
# Edit secrets.h with your WiFi credentials
```

2. **Build & Flash**
```bash
cd firmware
pio run -t upload
```

3. **Deploy API** (optional - for your own instance)
```bash
cd api
wrangler deploy
```

## Live Data Refresh

| Screen | Data Source | Refresh Rate |
|--------|-------------|--------------|
| HOME | summary.* | 30s |
| GITHUB | github.* | 30s |
| INFRA | infrastructure.* | 30s |
| CRM | business.crm.* | 60s |
| CRYPTO | crypto.* | 60s |
| AI | ai.* | 30s |
| ALERTS | alerts[] | 10s |

## Live Indicators

- `● LIVE` (green) - Data < 60s old
- `● STALE` (yellow) - Data 60-300s old
- `● OFFLINE` (red) - Data > 300s old

## Brand System

Uses official BlackRoad colors (RGB565):
- Hot Pink: `#FF1D6C` (`0xF8EA`)
- Amber: `#F5A623` (`0xFD40`)
- Electric Blue: `#2979FF` (`0x14FF`)
- Violet: `#9C27B0` (`0x9A74`)

Golden Ratio spacing: 8, 13, 21, 34, 55, 89, 144px

## Serial Commands

```
PORTFOLIO       # Show full product list
DEMO            # Start demo mode
STATS           # Portfolio statistics
SOVEREIGN       # Sovereignty score
```

---

**This is what sovereignty looks like.** 🖤🛣️

*BlackRoad OS, Inc. - All Rights Reserved*
