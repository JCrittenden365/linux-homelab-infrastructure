# Debian Server Setup

## Overview

This document covers the initial setup of the primary lab server — a **Dell Laptop running Debian 12 on bare metal** (not a VM). This is the machine where all major security hardening, monitoring, and automation was configured.

For hardware and network context, see [Lab Architecture](lab-architecture.md).

---

## Why a Physical Machine?

Using a real laptop as the server (rather than a VM) means the environment more closely resembles a real-world administration scenario — the machine is always on, has its own hardware identity, and is accessed entirely over the network from the HP Laptop client.

---

## Installation

Debian 12 was installed using the standard installer with minimal packages selected.

Choices made during installation:

- OpenSSH Server — installed
- Standard system utilities — installed
- Graphical desktop — **not installed**

Keeping the system headless keeps it lightweight and focused on server administration.

---

## System Identity

```bash
hostnamectl
```

![System Identity](screenshots/System_Identity.png)

The hostname `lab-server` was set during installation to clearly identify this machine in logs and SSH sessions.

---

## User Accounts

Three users were created to simulate a real multi-user environment.

| User   | Role                                   |
| ------ | -------------------------------------- |
| josh   | Primary administrator with sudo access |
| carrie | Standard user                          |
| alex   | Standard user                          |

Full user management and SSH key setup is documented in [User Management](user-management-and-ssh-access.md).

---

## Services Configured

All major configurations on this server are documented separately:

| Service  | Document                                                              |
| -------- | --------------------------------------------------------------------- |
| SSH      | [SSH Passwordless Authentication](ssh-passwordless-authentication.md) |
| SSH      | [SSH Hardening](ssh-hardening.md)                                     |
| UFW      | [UFW Firewall Configuration](ufw-firewall-configuration.md)           |
| Fail2Ban | [Fail2Ban Intrusion Prevention](fail2ban-intrusion-prevention.md)     |
| Cron     | [Cron Automation](cron-automation-and-maintenance.md)                 |
| Logging  | [Log Analysis and Monitoring](log-analysis-and-monitoring.md)         |
