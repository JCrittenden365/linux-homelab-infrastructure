# # Linux Home Lab Infrastructure

## Overview

This repository documents the design, configuration, and security hardening of a personal Linux home lab environment built to develop practical **System Administration and DevOps skills**.

The lab simulates a small multi-server infrastructure where various Linux administration tasks are performed, including secure SSH access, firewall configuration, intrusion detection, system automation, and log analysis.

The goal of this project is to build real-world experience with Linux systems while documenting each step in a professional and reproducible way.

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
