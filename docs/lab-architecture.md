# Lab Architecture

## Overview

This home lab was built to practice Linux system administration, security hardening, and automation in a safe environment.

The lab consists of a physical desktop system running virtual machines along with additional client machines used to simulate real SSH access from different systems.

The goal is to simulate a small multi-user Linux environment where tasks such as SSH hardening, firewall configuration, intrusion detection, and automation can be practiced.

---

                Home Network
                 192.168.1.0/24
                       |
                ┌─────────────┐
                │  Router     │
                └─────┬───────┘
                      │
        ┌──────────────────────────────┐
        │ Dell OptiPlex (Host Machine) │
        │ VirtualBox Hypervisor        │
        └────────────┬─────────────────┘
                     │
        ┌──────────────────────────────┐
        │ Debian Server VM             │
        │ 192.168.1.147                │
        │ SSH / UFW / Fail2Ban         │
        └──────────────────────────────┘
                     │
        ┌──────────────────────────────┐
        │ Ubuntu Server VM             │
        │ 192.168.1.122                │
        │ SSH Hardening Lab            │
        └──────────────────────────────┘

Clients:
HP Laptop / Windows Desktop → SSH access

---

## Hardware Used

### Dell OptiPlex Desktop

Primary lab machine.

Responsibilities:

* Runs VirtualBox
* Hosts the Ubuntu Server virtual machine
* Used as a main SSH client for testing

---

### HP Laptop

Secondary client system used for:

* SSH testing
* Generating SSH keys
* Testing passwordless authentication

---

## Servers

### Debian Server

This server was the first system configured in the lab and acts as the primary system administration practice machine.

Key tasks performed on this server:

* Multi-user SSH access configuration
* Passwordless SSH authentication
* SSH hardening
* Firewall configuration using UFW
* Intrusion prevention using Fail2Ban
* Log analysis and auditing
* Cron automation and system maintenance scripts

Example Address:

Debian Server
192.168.1.147

---

### Ubuntu Server VM

The Ubuntu Server virtual machine was created later in the project to provide a second environment for testing configurations and comparing behavior across Linux distributions.

This VM is hosted on the Dell OptiPlex using VirtualBox.

Example Address:

Ubuntu Server VM
192.168.1.122

---

## User Accounts

Multiple users were created to simulate a real multi-user Linux environment.

Each user was configured with their own SSH key for secure login.

---

## SSH Access Model

The lab uses **SSH key authentication instead of passwords**.

Each client machine generates an ed25519 key pair.

The public key is copied to the server in:

```
~/.ssh/authorized_keys
```

Permissions are restricted to ensure SSH security requirements are met.

Example permissions:

```
~/.ssh
700
```

```
authorized_keys
600
```

---

## Purpose of the Lab

This lab environment was created to practice real Linux system administration tasks including:

* Secure remote access
* User management
* Firewall configuration
* Intrusion detection
* Log monitoring
* System automation
* troubleshooting authentication issues

All configurations were performed manually to better understand how Linux systems behave in real environments.

