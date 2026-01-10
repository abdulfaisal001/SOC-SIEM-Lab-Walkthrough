# SOC-SIEM-Lab-Walkthrough


# SOC-SIEM Lab - Complete Walkthrough

A performance-optimized, beginner-friendly SOC lab setup using Splunk SIEM on Ubuntu Server with Windows endpoints and Active Directory. Designed for 8GB and 16GB RAM systems.

[

## 🚀 Quick Start

**Minimum Requirements**

- Host: Windows 11 (150-200GB free disk)
- RAM: 16GB recommended (8GB constrained mode supported)
- Hypervisor: VirtualBox (preferred) or VMware Workstation

**Core Components**

```
Ubuntu Server (Splunk SIEM) ← Windows 10 Endpoint + Sysmon
                          ← Windows Server 2019 (AD DC)
                          ← Kali Linux (Phase 1 attacks only)
```


## 📋 Table of Contents

- [Phase 1: Foundation (SIEM + Linux Logs)](#phase-1)
- [Phase 2: Windows Endpoint](#phase-2)
- [Phase 3: Active Directory](#phase-3)
- [Networking Setup](#networking)
- [8GB RAM Guide](#8gb-ram)
- [Daily Operations](#operations)


## 🖥️ Host Preparation

### Hardware Check

```
RAM: 16GB (8GB constrained mode)
Disk: 150-200GB free
Virtualization: Enabled in BIOS (VT-x/AMD-V)
```


### Hypervisor Install

```powershell
# Use ONE only
Option 1: VirtualBox 7.x (Recommended)
Option 2: VMware Workstation Player/Pro
```


## 📥 Required ISOs (Download Only)

| OS | Purpose | Source |
| :-- | :-- | :-- |
| Ubuntu Server 24.04 LTS | Splunk SIEM | ubuntu.com |
| Kali Linux 2024.x | Phase 1 Attacker | kali.org |
| Windows 10 22H2 | Endpoint | microsoft.com |
| Windows Server 2019 | AD Domain Controller | microsoft.com |

> **⚠️ Do NOT download Windows Server 2022** - 2019 is lighter, perfect for labs.

## 🗂️ Phase-by-Phase Deployment

### Phase 1: Foundation (SIEM + Linux Logs)

**Goal**: Splunk basics + Linux log ingestion (6GB RAM)

**VMs to Install**:

```
1. Ubuntu Server (FIRST)
   RAM: 4GB | CPU: 2c/2t | Disk: 50GB
   Network: NAT + Host-Only
   Notes: No GUI, SSH enabled, normal user

2. Kali Linux (SECOND - Temporary)
   RAM: 2GB | CPU: 1-2c | Disk: 30GB
```

**Running**: Ubuntu + Kali only

```
Shut down everything else
```


### Phase 2: Windows Endpoint

**Goal**: Windows logs + Sysmon + Endpoint detection (8GB RAM)

**VMs Running**:

```
Ubuntu Server + Windows 10 (Kali OFF)
```

**Windows 10 Config**:

```
RAM: 3GB | CPU: 2c | Disk: 50GB
Post-install:
✓ Disable animations
✓ Disable OneDrive  
✓ Install Sysmon (later)
✓ Splunk Universal Forwarder (later)
```


### Phase 3: Active Directory (Final Core)

**Goal**: Domain auth logs + Identity detections (11GB RAM)

**VMs Running**:

```
Ubuntu + Win10 + WinServer 2019
```

**Windows Server 2019 (Minimal AD)**:

```
RAM: 4GB | CPU: 2c | Disk: 50GB
Roles: AD DS only
Domain: Single domain
Users: 1 admin account
❌ No extra roles/DC
```


## 🌐 Networking (Simple \& Stable)

```
All VMs: NAT + Host-Only Adapter
Why: Internet + Internal comms + Static IPs

Verification Checklist:
✅ All VMs ping Ubuntu (Splunk)
✅ Host browser → Splunk UI (https://ubuntu-ip:8000)
```


## 💾 8GB RAM Constrained Mode

| Phase | Running VMs | Total RAM | Status |
| :-- | :-- | :-- | :-- |
| 1 | Ubuntu(3GB) + Kali(2GB) | 5GB | ✅ Safe |
| 2 | Ubuntu(3GB) + Win10(3GB) | 6GB | ✅ Safe |
| 3 | Ubuntu(3GB) + Win10(3GB) + Server(3GB) | 9GB | ⚠️ Short sessions |

**Hard Rules**:

- Max 2 VMs normally
- Phase 3: 30-60min sessions only
- Shut down Kali immediately after use


## 🚫 Common Beginner Mistakes

| ❌ Wrong | ✅ Correct |
| :-- | :-- |
| Install all VMs first | Phase-by-phase |
| Ubuntu Server w/ GUI | CLI only |
| 6-8GB RAM per VM | Follow specs |
| Run Kali 24/7 | Phase 1 only |
| Install Splunk everywhere | Ubuntu only |

## 📊 Learning Outcomes by Phase

**Phase 1**: Splunk Search | Linux Syslog | Basic correlation
**Phase 2**: Sysmon parsing | Windows Event Logs | Endpoint hunting
**Phase 3**: Kerberos attacks | AD log analysis | Identity threats

## 🔧 Daily Operations Checklist

```
Daily Startup (8GB mode):
[ ] Phase 1: Ubuntu + Kali only
[ ] Phase 2: Ubuntu + Win10 (Kali OFF)
[ ] Phase 3: All 3 (short session)

Splunk Access:
Browser → https://ubuntu-ip:8000
Default: admin/changeme
```


## 🎯 Next Steps After Setup

1. **Install Splunk Enterprise** (Ubuntu Server)
2. **Configure Forwarders** (Win10/Server)
3. **Deploy Sysmon** (Win10 baseline)
4. **Phase 1 Attacks** (Kali → Ubuntu)
5. **Splunk Searches** (Detection rules)

## 📈 Resource Usage Matrix

| Phase | VMs | 16GB RAM | 8GB RAM |
| :-- | :-- | :-- | :-- |
| 1 | Ubuntu+Kali | ~6GB ✅ | ~5GB ✅ |
| 2 | Ubuntu+Win10 | ~8GB ✅ | ~6GB ✅ |
| 3 | All 3 | ~11GB ✅ | ~9GB ⚠️ |

## 🤝 Contributing

```
Issues → Security findings, performance tips
PRs → Detection rules, new attack scenarios
Docs → Missing setup steps
```


## 📄 License

MIT License - Free for personal, educational, and portfolio use.

***

**Built for cybersecurity freshers building SOC analyst skills**
**Portfolio-ready lab with professional-grade documentation**

> **Status**: Production-ready | **Tested**: Windows 11 + VirtualBox 7.0 | **Splunk**: 9.2+ compatible
<span style="display:none">[^1]</span>

<div align="center">⁂</div>



