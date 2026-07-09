# 🌐 Hybrid Cloud Lab – Azure Arc & Azure Backup

## 📌 Project Overview

This lab demonstrates how to prepare an on-premises Windows Server and integrate it with Microsoft Azure Hybrid Cloud services.

The project includes:

- Windows Server 2025 deployment in VMware Workstation
- Basic server configuration
- Static network configuration
- VMware Tools installation
- Snapshot creation
- Azure Arc onboarding
- Azure Backup (MARS Agent)

The goal is to simulate a real on-premises server that can be managed and protected through Microsoft Azure.

---

# 🛠 Environment

| Component | Value |
|-----------|-------|
| Hypervisor | VMware Workstation Pro 25H2 |
| Operating System | Windows Server 2025 Standard Evaluation (Desktop Experience) |
| Azure Subscription | Azure for Students |
| Region | West Europe |
| Network | NAT |
| Recovery Services Vault | Azure Backup |
| Hybrid Management | Azure Arc |

---

# 📖 Part 1 – Windows Server Preparation

## 1. Create Windows Server VM

Created a new virtual machine using VMware Workstation.

Configuration:

- Windows Server 2025
- 2 vCPUs
- 2 GB RAM
- 60 GB Virtual Disk
- NAT Networking

---

## 2. Install Windows Server

Installed Windows Server 2025 Standard Evaluation (Desktop Experience).

Configured:

- Administrator password
- Initial setup
- Desktop Experience

---

## 3. Rename Server

Changed the computer name to:

```text
SRV-HYBRID01
```

Restarted the server.

---

## 4. Configure Static Network

Assigned a static IPv4 configuration.

| Setting | Value |
|----------|------|
| IP Address | 192.168.100.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.100.2 |
| Preferred DNS | 8.8.8.8 |

Verified Internet connectivity using:

```cmd
ping 8.8.8.8
```

---

## 5. Windows Update

Installed all available Windows Updates.

---

## 6. Install VMware Tools

Installed VMware Tools to enable:

- Better display resolution
- Mouse integration
- Clipboard sharing
- Drag & Drop support

---

## 7. Create Snapshot

Created a VMware snapshot.

Snapshot Name:

```text
Basis fertig – bereit für Arc Backup Migrate
```

This snapshot provides a clean recovery point before configuring Azure services.

---

# 📖 Part 2 – Azure Arc

## Objective

Register the on-premises Windows Server as an Azure Arc-enabled server.

---

## Steps

### Generate Onboarding Script

In Azure Portal:

Azure Arc

↓

Servers

↓

Add Server

↓

Generate Script

Downloaded:

```text
OnboardingScript.ps1
```

---

### Execute Script

Copied the script to the Windows Server VM.

Opened PowerShell as Administrator.

Executed:

```powershell
.\OnboardingScript.ps1
```

The script:

- Installed Azure Connected Machine Agent
- Connected the server to Azure
- Registered the machine in Azure Arc

---

### Verification

Verified inside Azure Portal:

Azure Arc

↓

Servers

↓

SRV-HYBRID01

Status:

```text
Connected
```

Successfully managed as an Azure Arc-enabled Server.

---

# 📖 Part 3 – Azure Backup

## Objective

Protect local files using Microsoft Azure Recovery Services (MARS Agent).

---

## Create Recovery Services Vault

Created:

- Resource Group
- Recovery Services Vault

Changed Storage Replication:

```text
GRS → LRS
```

to minimize Azure costs.

---

## Install MARS Agent

Downloaded:

- Microsoft Azure Recovery Services Agent
- Vault Credentials

Installed the agent.

Registered the server.

Configured an encryption passphrase.

---

## Backup Test

Created folder:

```text
C:\BackupTest
```

Added test files.

Created a backup schedule.

Executed:

```text
Back Up Now
```

---

## Verification

Confirmed:

- Successful backup job
- Recovery Point created
- Backup visible inside Azure Portal

---

# 📖 Troubleshooting

During the lab several issues were encountered and resolved.

### Network

Problem:

```
Media disconnected
```

Resolution:

Reset VMware network adapter.

Reconfigured NAT networking.

Internet connectivity restored.

---

### Azure Arc Installation

Problem:

```
Installation failed
Disk full
```

Cause:

The Windows partition was only 18 GB although the virtual disk had already been expanded to 60 GB.

Resolution:

Extended the Windows partition to use the unallocated space.

Azure Connected Machine Agent installed successfully afterwards.

---

# 📚 Skills Practiced

- VMware Workstation
- Windows Server 2025
- Static IP Configuration
- DNS
- NAT Networking
- Windows Administration
- Azure Arc
- Azure Connected Machine Agent
- Recovery Services Vault
- Azure Backup
- MARS Agent
- Hybrid Cloud
- Microsoft Azure

---

# 📷 Screenshots

The repository contains screenshots for the following steps:

- Windows Server installation
- Server configuration
- Static IP configuration
- VMware Tools installation
- Snapshot creation
- Azure Arc onboarding
- Azure Arc Connected status
- Recovery Services Vault
- MARS Agent installation
- Backup completed successfully

---

# 🎯 Learning Outcome

This project demonstrates how to prepare an on-premises Windows Server and integrate it with Azure Hybrid Cloud services.

The server can now:

- Be centrally managed through Azure Arc
- Be monitored from Azure
- Be protected using Azure Backup
- Serve as a foundation for future Hybrid Cloud scenarios such as Azure Migrate and Microsoft Entra Connect.

---
