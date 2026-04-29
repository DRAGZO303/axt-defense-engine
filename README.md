# AXT Defense Engine
### Next-Generation SIEM Platform — Built From Scratch




![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.109-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Built by](https://img.shields.io/badge/Built%20by-Mohamed%20Amir%20M-0A66C2?style=for-the-badge)

**[📹 3-Minute Demo](YOUR_LOOM_LINK) · [🌐 Live Demo](YOUR_LIVE_URL) · [💼 LinkedIn](https://www.linkedin.com/in/mohdamir32/)**




---

> A production-grade Security Operations Center platform I built entirely from scratch as a cybersecurity trainer and SOC practitioner.
> Equivalent in capability to commercial SIEM platforms (Splunk, IBM QRadar) that cost **$50,000+/year**.
> Deployed on Ubuntu with Nginx, PostgreSQL, Redis, and Celery — 15,000+ lines of Python and React.

---

## 🎯 What Is This?

AXT Defense Engine is a **full-stack Next-Generation SIEM** (Security Information and Event Management) platform built to solve real SOC challenges:

- Alert fatigue from uncorrelated noise
- Manual triage consuming analyst time
- No visibility into attack kill chains
- Siloed threat intelligence
- Reactive instead of automated response

I built every component from scratch — ingestion, detection, correlation, SOAR, AI triage, reporting, and the frontend dashboard — to deeply understand what SOC analysts need at the code level.

---

## ✨ Core Features

### 🔍 Detection Engine
- **24+ Sigma-compatible detection rules** covering: SSH brute force, privilege escalation (sudo), DNS C2 tunnelling, reverse shell attempts, port scanning, lateral movement, new user creation, and firewall rule changes
- **Pattern matching** (regex against log messages) + **threshold detection** (sliding time-window counters per source IP)
- **MITRE ATT&CK mapping** — every alert tagged with tactic (TA0001–TA0040) and technique automatically
- **Confidence scoring** (0–100%) per alert with explainable detection reason
- **Sigma rule importer** — bulk import community detection rules from SigmaHQ

### 🧠 AI-Powered Triage
- Integrated **Anthropic Claude AI** — reads full alert context and returns: what happened, why dangerous, 3 immediate actions, false-positive likelihood
- **AI-generated Attack DNA** — narrative describing multi-stage attack campaigns in plain language
- **AI report summaries** — executive paragraphs auto-generated from security metrics
- **Log summarisation** — Claude condenses 50+ log lines into a 3-sentence analyst brief

### ⚡ SOAR Automation
- **IP blocking** via iptables (confidence-threshold gated to prevent false-positive blocking)
- **Process termination** by PID
- **Full host isolation** (quarantine — blocks all inbound, outbound, and forwarded traffic)
- **Discord webhook** alerts with severity-coloured embeds
- **SMTP email** alerts with full context
- **Alert playbooks** — step-by-step analyst guidance + auto-triggered response actions per rule type
- **Auto-response rules** — configurable per severity and confidence threshold

### 🔗 Correlation Engine
- Groups related alerts from same source IP into **incident campaigns**
- Reconstructs **MITRE ATT&CK kill chain sequence** across all correlated alerts
- Generates **Attack DNA narrative** (AI-written campaign description)
- Calculates overall incident severity from component alert severities

### 📊 UEBA (User & Entity Behavior Analytics)
- 7-day rolling **behavioral baseline profiling** per source IP
- Hourly activity distribution analysis
- **Anomaly detection** — traffic spikes, off-hours activity, new destination IPs
- **0–100 risk scoring engine** weighting: failed logins, sudo events, reverse shell patterns, DNS anomalies

### 🌍 Threat Intelligence
- Real-time **IP/domain reputation** (AbuseIPDB, ip-api.com)
- Interactive **GeoIP attack origin map** (Leaflet)
- **Feodo Tracker** botnet C2 feed ingestion (free, no key required)
- **Bulk IOC CSV upload** for custom intelligence lists
- Per-alert automatic threat enrichment

### 📋 Log Ingestion & Normalisation
- **Linux host agent** — Python watchdog, real-time log tailing (`auth.log`, `syslog`, custom)
- **Windows host agent** — PowerShell, Security Event Log (Event IDs 4625, 4624, 4688, 4720, 4726, 4732)
- **SSH agentless collection** — pull logs from remote hosts without agent installation
- **Network sniffer** — Scapy-based packet capture (TCP, UDP, DNS)
- **ECS-inspired normalisation** — consistent schema across all log source types

### 📈 Analytics & Reporting
- 6 chart types: alerts over time, top attacker IPs, severity distribution, attack types, MITRE heatmap, log volume
- **Defense Score** (0–100) across 5 weighted components with specific improvement recommendations
- **PDF executive reports** — AI-written summaries, top attackers, attack types, security score
- **Excel exports** — structured multi-sheet workbooks for compliance
- **Scheduled delivery** — daily/weekly reports via email and Discord
- **30-day report history** with download links

### 🎮 Gamification
- **Analyst leaderboard** — points for investigating alerts (+10), true positives (+25), resolving incidents (+50)
- Rank titles: Trainee → Junior Analyst → Analyst → Senior Analyst → Elite Defender

### 🧪 Cyber Range (Attack Simulation)
- 5 realistic attack simulations for detection validation and analyst training:
  - SSH Brute Force (threshold rule validation)
  - Port Scan (firewall rule validation)
  - DNS Exfiltration (C2 tunnelling detection)
  - Reverse Shell (pattern rule validation)
  - Privilege Escalation (multi-step sequence)

---

## 🏗️ Architecture

```
Agents / Log Sources
        ↓
Ingestion & Normalisation (ECS schema)
        ↓
Detection Engine ←─── Threat Intel ←─── GeoIP
        ↓
Correlation Engine ──→ MITRE ATT&CK Mapping
        ↓
UEBA / Behavior Analytics
        ↓
AI Triage (Claude) ←─────────────────────┐
        ↓                                │
SOAR Automation                          │
        ↓                            FastAPI (22 routes)
SOC Dashboard (React 18)                 │
        ↑                                │
WebSocket (real-time) ───────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3.11, FastAPI, SQLAlchemy (async), Alembic |
| Frontend | React 18, TypeScript, Material UI, Recharts, Leaflet |
| Database | PostgreSQL 15 (primary), Redis (queues + cache) |
| Task Queue | Celery + Celery Beat (scheduled reports) |
| Real-time | WebSocket (FastAPI native) |
| AI | Anthropic Claude API (claude-sonnet-4-6) |
| Infrastructure | Ubuntu 24.04, Nginx, systemd, Docker |
| Security | JWT auth, bcrypt, iptables, UFW, fail2ban, Let's Encrypt |
| Monitoring | Prometheus + FastAPI Instrumentator, Grafana |

---

## 🚀 Quick Start

```bash
# 1. Clone
git clone https://github.com/YOUR_USERNAME/axt-defense-engine
cd axt-defense-engine

# 2. Configure
cp .env.example .env
nano .env   # set DATABASE_URL, SECRET_KEY, AGENT_API_TOKEN

# 3. Install everything (deps + DB + frontend build + services)
sudo bash scripts/install.sh

# 4. Open dashboard
# http://YOUR-SERVER-IP/
# Login: admin / AxtAdmin2024!  ← change this immediately
```

**Full setup guide:** See [INSTALL.md](./INSTALL.md)

---

## 📸 Screenshots

> *Dashboard · Alerts · Investigation · Simulation · Reports · Analytics*

*(Add 6 screenshots here)*

---

## 📊 Project Stats

| Metric | Value |
|---|---|
| Lines of code | 15,000+ |
| API routes | 22 |
| Frontend pages | 17 |
| Database tables | 12 |
| Detection rules | 24+ |
| Attack simulations | 5 |
| Build time | 3 months solo |

---

## 🔐 Security Note

AXT Defense Engine is built for **educational and professional SOC use**. The attack simulation module sends synthetic log data only to your own SIEM instance — no real attacks are performed against any external system.

---

## 👤 About the Builder

**Mohamed Amir M** — Cybersecurity Trainer (VAPT & SOC) at RedTeam Hacker Academy

- 🏅 Recognised by **NCIIPC** for responsible vulnerability disclosure
- 🐛 Bug bounty hunter on **HackerOne**
- 🎓 CEH (EC-Council) · CPT · CICSA · Certified RedTeam Instructor
- 🔬 Specialties: SOC operations, detection engineering, VAPT, web app pentesting

💼 [LinkedIn](https://www.linkedin.com/in/mohdamir32/) · 📧 connect.amr00@gmail.com

---

## 📄 License

MIT License — see [LICENSE](./LICENSE)

---



  Built with 🔐 by Mohamed Amir M · If this helped you, please ⭐ the repo
