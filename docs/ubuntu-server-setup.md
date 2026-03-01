# Ubuntu Server Setup

## Overview

This document covers the Ubuntu Server VM hosted on the **Dell Desktop** using VirtualBox. Unlike the main Dell Laptop server, this VM was not fully hardened — it was used primarily to practice passwordless SSH authentication and to run experimental configurations safely.

For hardware and network context, see [Lab Architecture](lab-architecture.md).

---

## Virtual Machine Setup

The Ubuntu Server VM was created in VirtualBox on the Dell Desktop alongside a Debian VM.

![VirtualBox VMs](screenshots/VMs.png)

**OS:** Ubuntu Server 24.04 LTS  
**Installation type:** Minimal server install  
**Components installed:** OpenSSH Server, standard utilities  
**Graphical interface:** Not installed

---

## Network

The VM received an IP address on the local network via DHCP.

```
192.168.1.122
```

SSH is the only remote access method used.

---

## SSH Key Authentication

Passwordless SSH authentication was configured so the HP Laptop client could log in without a password. This followed the same key setup process used on the main Debian server.

Refer to [SSH Passwordless Authentication](ssh-passwordless-authentication.md) for the full process.

---

## Purpose in the Lab

The Ubuntu VM (along with the Debian VM on the same Desktop) served as a safe sandbox for:

- Practicing SSH key setup without risk to the main hardened server
- Testing configurations and observing results before applying them to the Dell Laptop
- Multi-host SSH administration from the HP Laptop client
- Comparing behavior between Ubuntu and Debian in a controlled environment
