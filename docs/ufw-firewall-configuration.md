
# UFW Firewall Configuration

## Overview

After securing SSH access, the next step in the lab environment was configuring a host-based firewall.

Ubuntu and Debian systems commonly use **UFW (Uncomplicated Firewall)** as a simplified interface for managing iptables firewall rules.

The firewall was configured to:

* allow secure remote administration via SSH
* block all other incoming connections by default
* provide a basic layer of network protection

This configuration simulates how a typical Linux server is secured in a real environment.

---

## Installing UFW

First, verify whether UFW is installed.

Command:

```
sudo ufw status
```

If UFW is not installed, install it using:

```
sudo apt update
sudo apt install ufw
```

---

## Default Firewall Policies

Before enabling the firewall, default policies were configured.

Command:

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Explanation:

* **deny incoming** → blocks all unsolicited connections
* **allow outgoing** → allows the system to reach external services

This creates a secure baseline.

---

## Allowing SSH Access

Since SSH is used to manage the server remotely, it must be allowed before enabling the firewall.

Command:

```
sudo ufw allow ssh
```

Alternatively, the port can be specified directly:

```
sudo ufw allow 22/tcp
```

This rule allows remote administrators to connect to the system.

---

## Enabling the Firewall

Once SSH access is confirmed, the firewall can be enabled.

Command:

```
sudo ufw enable
```

The system will warn that enabling the firewall may interrupt existing SSH connections. Because SSH was allowed beforehand, remote access remains functional.

---

## Verifying Firewall Rules

Firewall rules can be verified using:

```
sudo ufw status verbose
```

Example output:

```
Status: active

To      Action   From
--      ------   ----
22/tcp  ALLOW    Anywhere
```

This confirms that the firewall is active and SSH access is permitted.

---

## Testing Firewall Protection

Testing was performed by verifying:

* SSH access remained available
* unauthorized ports were blocked

Example connection attempt:

```
ssh user@192.168.1.147
```

Successful connection confirms the firewall rule is working correctly.

---

## Additional Useful Commands

List rules with numbering:

```
sudo ufw status numbered
```

Delete a rule:

```
sudo ufw delete <rule_number>
```

Disable the firewall (if troubleshooting is required):

```
sudo ufw disable
```

---

## Security Benefits

Using a host-based firewall provides several advantages:

* blocks unnecessary open ports
* reduces attack surface
* provides simple rule management
* adds an additional security layer

When combined with SSH hardening and intrusion detection tools such as Fail2Ban, UFW helps form a basic defensive security posture.

---

## Lessons Learned

Key takeaways from this lab:

* Always allow SSH before enabling the firewall
* Default deny policies improve server security
* Firewall rules should be verified after configuration
* Host-based firewalls are a standard security practice for Linux servers
