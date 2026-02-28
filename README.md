# Linux Home Lab Infrastructure

## Overview

This repository documents the design, configuration, and security hardening of a personal Linux home lab environment built to develop practical **System Administration and DevOps skills**.

The lab simulates a small multi-server infrastructure where various Linux administration tasks are performed, including secure SSH access, firewall configuration, intrusion detection, system automation, and log analysis.

The goal of this project is to build real-world experience with Linux systems while documenting each step in a professional and reproducible way.

---

## Skills Demonstrated

Linux system administration  
SSH configuration and hardening  
Firewall configuration (UFW)  
Intrusion detection and prevention (Fail2Ban)  
User and access management  
Log analysis and monitoring  
Cron automation and system maintenance  
Virtual machine infrastructure (VirtualBox)  
Network troubleshooting and debugging

---

## Lab Environment

This project was built using a small home lab designed to practice real-world Linux system administration tasks such as SSH hardening, firewall configuration, intrusion prevention, and automation.

### Physical Systems

| Device                | Role                                                             |
| --------------------- | ---------------------------------------------------------------- |
| Dell OptiPlex Desktop | Primary lab host and virtualization platform                     |
| HP Laptop             | SSH client used for remote administration and key authentication |

### Virtual Machines

| System           | Purpose                                                                                           |
| ---------------- | ------------------------------------------------------------------------------------------------- |
| Debian Server    | Main lab server used for SSH configuration, user management, firewall rules, and Fail2Ban testing |
| Ubuntu Server VM | Secondary system used to practice secure SSH configuration and multi-host administration          |

### Networking

| Component          | Details                          |
| ------------------ | -------------------------------- |
| Network Type       | Local home network               |
| Access Method      | SSH remote administration        |
| Key Authentication | ed25519 public/private key pairs |

## Lab Topology

```
                Home Network
                     │
                     │
        ┌──────────────────────────┐
        │ Dell OptiPlex Desktop    │
        │ (Virtualization Host)    │
        │                          │
        │  VirtualBox              │
        │   ├─ Debian Server       │
        │   │   SSH / UFW / Fail2Ban
        │   │   Users: user1, user2, user3
        │   │
        │   └─ Ubuntu Server VM    │
        │       SSH Hardening Lab
        └──────────────────────────┘
                     │
                     │ SSH Key Authentication
                     │
           ┌──────────────────────┐
           │ HP Laptop            │
           │ SSH Administration   │
           │ Client               │
           └──────────────────────┘
```


### Security Tools Implemented

* SSH key authentication
* SSH configuration hardening
* Firewall rule management (UFW)
* Intrusion prevention using Fail2Ban
* Log monitoring and analysis
* Cron-based system automation

### Project Goals

The goal of this lab is to simulate common tasks performed by junior Linux system administrators, including:

* securing remote access
* managing multiple users
* monitoring authentication activity
* detecting intrusion attempts
* automating maintenance tasks

---

## Quick Navigation

Project documentation can be found in the following sections:

| Topic                                                                      | Description                                      |
| -------------------------------------------------------------------------- | ------------------------------------------------ |
| [Lab Architecture](docs/lab-architecture.md)                               | Overview of the lab environment and systems      |
| [Debian Server Setup](docs/debian-server-setup.md)                         | Initial installation and configuration           |
| [Ubuntu Server VM](docs/ubuntu-server-setup.md)                            | Creation and setup of the Ubuntu virtual machine |
| [SSH Passwordless Authentication](docs/ssh-passwordless-authentication.md) | Configuring ed25519 key authentication           |
| [SSH Hardening](docs/ssh-hardening.md)                                     | Securing SSH access                              |
| [UFW Firewall Configuration](docs/ufw-firewall-configuration.md)           | Firewall rules and protection                    |
| [Fail2Ban Intrusion Prevention](docs/fail2ban-intrusion-prevention.md)     | Detecting and blocking brute-force attacks       |
| [User Management](docs/user-management-and-ssh-access.md)                  | Multi-user SSH configuration                     |
| [Cron Automation](docs/cron-automation-and-maintenance.md)                 | Automated maintenance scripts                    |
| [Log Analysis](docs/log-analysis-and-monitoring.md)                        | Investigating system logs and events             |

---

## Core Technologies Used

* Linux (Debian & Ubuntu)
* SSH
* UFW Firewall
* Fail2Ban
* Cron Automation
* Systemd
* Linux Log Analysis

---

## Network Overview

Example lab addressing:

Debian Server:    192.168.1.147
Ubuntu Server VM: 192.168.1.122

Multiple users connect to these systems using secure SSH authentication.

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
```

---

## Learning Goals

This project is part of an ongoing effort to build professional-level Linux administration skills while studying for IT certifications and pursuing a career path toward **System Administration and DevOps**.

---

## Future Improvements

- Centralized logging
- Automated backups
- Docker container deployment
- Infrastructure as Code experimentation
- Monitoring with Prometheus/Grafana
  

Each document explains not only *how* a configuration was implemented, but also *why* it is important in real-world environments.

---

**Note:** This lab was built to practice real Linux administration, security hardening, and troubleshooting.  
All configurations are performed manually to reinforce foundational skills.  
Future improvements will expand automation and monitoring across multi-server setups.
