
# Ubuntu Server Setup

## Overview

This document explains how the Ubuntu Server virtual machine was created and configured for the home lab.

The Ubuntu server acts as a **secondary Linux host** used for testing remote administration and practicing multi-server management.

---

# Virtual Machine Environment

The Ubuntu server runs as a virtual machine on the Dell OptiPlex lab computer using **VirtualBox**.

Purpose of the VM:

* practice server deployment
* compare Linux distributions
* simulate managing multiple systems

---

# Operating System

Ubuntu Server 24.04 LTS

The system was installed using the **minimal server installation** option.

Installed components include:

* OpenSSH Server
* standard utilities

No graphical interface was installed.

---

# Network Configuration

After installation the server received an IP address on the local network.

Example IP:

```
192.168.1.122
```

This allows the server to be accessed remotely using SSH.

---

# Remote Administration

SSH is the primary management method.

Example connection:

```
ssh user1@192.168.1.122
```

Passwordless login was later configured using SSH keys.

---

# SSH Key Authentication

Public key authentication was configured so the administrator can log in without entering a password.

Keys are stored in:

```
~/.ssh/authorized_keys
```

This allows secure and convenient remote administration.

---

# Security Hardening

Basic SSH security improvements were applied including:

* disabling password authentication
* verifying key-based login
* restricting unnecessary access

These changes help protect the system from unauthorized login attempts.

---

# Purpose of This Server

The Ubuntu VM allows the lab environment to simulate **multiple systems communicating over a network**.

This helps practice skills such as:

* managing remote servers
* troubleshooting SSH connections
* testing configuration differences between Linux distributions
* learning multi-system administration
