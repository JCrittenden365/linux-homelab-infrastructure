# Linux Home Lab Infrastructure

## Overview

This repository documents the design, configuration, and security hardening of a personal Linux home lab environment built to develop practical **System Administration and DevOps skills**.

The lab simulates a small multi-server infrastructure where SSH access, firewall configuration, intrusion detection, system automation, and log analysis are practiced hands-on.

Each document explains not only *how* a configuration was implemented, but also *why* it matters in real-world environments.

---

## Skills Demonstrated

- Linux system administration
- SSH configuration and hardening
- Firewall configuration (UFW)
- Intrusion detection and prevention (Fail2Ban)
- User and access management
- Log analysis and monitoring
- Cron automation and system maintenance
- Virtual machine infrastructure (VirtualBox)
- Network troubleshooting and debugging

---

## Lab Environment

### Physical Systems

| Device       | OS              | Role                                                                        |
| ------------ | --------------- | --------------------------------------------------------------------------- |
| Dell Laptop  | Debian 12       | Primary lab server — hardened with SSH, UFW, Fail2Ban, cron, and logging    |
| HP Laptop    | Windows         | Main SSH client — used for remote administration and key authentication      |
| Dell Desktop | Windows         | Virtualization host — runs VMs for passwordless auth and experimental testing |

### Virtual Machines (hosted on Dell Desktop)

| System           | Purpose                                                                      |
| ---------------- | ---------------------------------------------------------------------------- |
| Debian VM        | Passwordless SSH authentication practice and experimental testing            |
| Ubuntu Server VM | Passwordless SSH authentication practice and experimental testing            |

![VirtualBox VMs](docs/screenshots/VMs.png)

### Networking

| Component          | Details                             |
| ------------------ | ----------------------------------- |
| Network Type       | Local home network (192.168.1.0/24) |
| Access Method      | SSH remote administration           |
| Key Authentication | ed25519 public/private key pairs    |

### Lab Topology

```
                Home Network
                192.168.1.0/24
                     │
        ┌────────────────────────────┐
        │ Dell Laptop (Debian 12)    │
        │ Primary Hardened Server    │
        │ 192.168.1.147              │
        │ SSH / UFW / Fail2Ban       │
        │ Cron / Logging             │
        └────────────────────────────┘
                     │
                     │ SSH Key Authentication
                     │
           ┌──────────────────────┐
           │ HP Laptop (Windows)  │
           │ Main SSH Client      │
           └──────────────────────┘

        ┌────────────────────────────────┐
        │ Dell Desktop (VirtualBox Host) │
        │                                │
        │  ├─ Debian VM                  │
        │  │   Passwordless SSH / Testing│
        │  │                             │
        │  └─ Ubuntu Server VM           │
        │      Passwordless SSH / Testing│
        └────────────────────────────────┘
```

---

## Quick Navigation

| Topic                                                                      | Description                                      |
| -------------------------------------------------------------------------- | ------------------------------------------------ |
| [Lab Architecture](docs/lab-architecture.md)                               | Overview of the lab environment and systems      |
| [Debian Server Setup](docs/debian-server-setup.md)                         | Initial installation and configuration           |
| [Ubuntu Server Setup](docs/ubuntu-server-setup.md)                         | Creation and setup of the Ubuntu virtual machine |
| [SSH Passwordless Authentication](docs/ssh-passwordless-authentication.md) | Configuring ed25519 key authentication           |
| [SSH Hardening](docs/ssh-hardening.md)                                     | Securing the SSH service                         |
| [UFW Firewall Configuration](docs/ufw-firewall-configuration.md)           | Firewall rules and host-based protection         |
| [Fail2Ban Intrusion Prevention](docs/fail2ban-intrusion-prevention.md)     | Detecting and blocking brute-force attacks       |
| [User Management](docs/user-management-and-ssh-access.md)                  | Multi-user SSH configuration                     |
| [Cron Automation](docs/cron-automation-and-maintenance.md)                 | Scheduled maintenance scripts                    |
| [Log Analysis](docs/log-analysis-and-monitoring.md)                        | Investigating system logs and events             |
| [Lessons Learned](docs/lessons-learned.md)                                 | Key takeaways from building the lab              |
| [Troubleshooting Journal](docs/troubleshooting-journal.md)                 | Real issues encountered and how they were solved |

---

## Project Structure

```
docs/
    lab-architecture.md
    debian-server-setup.md
    ubuntu-server-setup.md
    ssh-passwordless-authentication.md
    ssh-hardening.md
    ufw-firewall-configuration.md
    fail2ban-intrusion-prevention.md
    user-management-and-ssh-access.md
    cron-automation-and-maintenance.md
    log-analysis-and-monitoring.md
    lessons-learned.md
    troubleshooting-journal.md
    screenshots/
```

---

## Future Improvements

- Centralized logging (in progress)
- Automated backups
- Docker container deployment
- Infrastructure as Code experimentation
- Monitoring with Prometheus/Grafana

---

**Note:** This lab was built to practice real Linux administration, security hardening, and troubleshooting. The primary server is a physical Dell Laptop running Debian 12 — not a VM. All configurations were performed manually to reinforce foundational skills.

*Author*
Josh Crittenden
Aspiring IT professional focused on Linux, automation, and hands-on technical development
