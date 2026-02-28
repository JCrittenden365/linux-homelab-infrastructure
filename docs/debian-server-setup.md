
# Debian Server Setup

## Overview

This document explains how the primary Debian lab server was installed and configured for the home lab environment.

This server acts as the **main administration and security testing system** where SSH configuration, firewall management, monitoring, and automation labs are performed.

---

# System Role

Primary purposes of this server:

* SSH security practice
* firewall configuration
* log monitoring
* Fail2Ban intrusion detection
* system automation using cron
* Linux user management

---

# System Information

Operating System: Debian 12
Role: Primary Linux Lab Server
Environment: Home Lab Virtual / Local Network

Example server IP:

```
192.168.1.147
```

---

# Initial Installation

Debian was installed using the standard installer with minimal packages.

During installation the following decisions were made:

* OpenSSH Server installed
* standard system utilities installed
* graphical desktop environment NOT installed

This keeps the system lightweight and focused on administration tasks.

---

# User Accounts

Three users were created for testing multi-user SSH access.

| User   | Role          |
| ------ | ------------- |
| user1  | administrator |
| user2  | standard user |
| user3  | standard user |

The **user1** account is used for system administration and has sudo privileges.

---

# SSH Configuration

SSH is used as the primary method for managing the server.

Key features configured:

* public key authentication
* password authentication disabled
* user access control
* multi-user SSH key setup

Each user has their own SSH key stored in:

```
~/.ssh/authorized_keys
```

This allows secure passwordless login.

---

# Firewall Configuration

The server firewall is managed using UFW.

Basic configuration:

```
sudo ufw allow ssh
sudo ufw enable
```

Default policy:

* deny incoming
* allow outgoing

This protects the server while still allowing administrative SSH access.

---

# Intrusion Protection

Fail2Ban was installed to monitor login attempts and protect the server from brute-force attacks.

Fail2Ban watches authentication logs and temporarily bans IP addresses after repeated failed login attempts.

---

# Logging and Monitoring

System logs are monitored using tools such as:

```
journalctl
tail
cat
```

Important logs include:

```
/var/log/auth.log
```

These logs help detect suspicious login activity.

---

# Automation

Cron jobs were implemented for:

* automated logging
* maintenance tasks
* testing scheduled automation

This allows routine administrative tasks to run automatically.

---

# Purpose of This Server

This Debian server acts as the **core learning platform** for practicing real-world Linux administration tasks in a safe environment.

It provides a place to experiment with system configuration, security practices, and troubleshooting techniques.
