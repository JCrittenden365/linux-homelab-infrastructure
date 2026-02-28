# # Linux Home Lab Infrastructure

## Overview

This repository documents the design, configuration, and security hardening of a personal Linux home lab environment built to develop practical **System Administration and DevOps skills**.

The lab simulates a small multi-server infrastructure where various Linux administration tasks are performed, including secure SSH access, firewall configuration, intrusion detection, system automation, and log analysis.

The goal of this project is to build real-world experience with Linux systems while documenting each step in a professional and reproducible way.

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

## Lab Environment

### Host Machine

Dell OptiPlex Desktop

### Virtualization Platform

VirtualBox

### Servers

**Debian Server**
Primary administration and security testing environment.

**Ubuntu Server VM**
Secondary environment used for testing configuration changes, SSH hardening, and automation.

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

## Skills Demonstrated

* Linux server installation and configuration
* Secure SSH authentication using ed25519 keys
* Multi-user access configuration
* Firewall hardening with UFW
* Intrusion prevention using Fail2Ban
* Log analysis and incident detection
* Scheduled maintenance automation using cron
* Infrastructure documentation

---

## Network Overview

Example lab addressing:

Debian Server: 192.168.1.147
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

Each document explains not only *how* a configuration was implemented, but also *why* it is important in real-world environments.
