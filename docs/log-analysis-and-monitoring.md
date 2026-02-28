
# Log Analysis and Monitoring

## Overview

Monitoring system logs is one of the most important responsibilities of a Linux system administrator. Logs provide visibility into system activity, authentication attempts, service errors, and potential security incidents.

In this lab environment, log analysis was used to:

* Investigate SSH login attempts
* Monitor system services
* Identify authentication failures
* Observe security events triggered by Fail2Ban

Understanding how to read and interpret logs is essential for detecting problems and responding to incidents.

---

## Common Log Locations

Linux stores logs in the `/var/log` directory.

Example:

```
cd /var/log
ls
```

Some commonly used log files include:

| Log File | Purpose                                        |
| -------- | ---------------------------------------------- |
| auth.log | Authentication events (SSH logins, sudo usage) |
| syslog   | General system messages                        |
| kern.log | Kernel-related messages                        |
| dmesg    | Hardware and kernel boot messages              |

Not every Linux distribution stores logs in the same file names, but most follow a similar structure.

---

## Viewing Authentication Logs

Authentication activity can be reviewed using:

```
sudo cat /var/log/auth.log
```

This file records:

* Successful SSH logins
* Failed login attempts
* sudo command usage
* user authentication activity

Example entry:

```
Accepted publickey for user2 from 192.168.1.100 port 52133 ssh2
```

This indicates that a successful SSH login occurred using public key authentication.

---

## Monitoring Logs in Real Time

To monitor activity as it happens:

```
sudo tail -f /var/log/auth.log
```

This command continuously displays new log entries as they are written.

This is useful when:

* testing SSH login behavior
* observing authentication failures
* verifying security tools like Fail2Ban

---

## Using journalctl

Many modern Linux systems use `systemd`, which stores logs in a system journal.

Example:

```
sudo journalctl
```

To view logs for a specific service:

```
sudo journalctl -u ssh
```

Recent entries can be viewed using:

```
sudo journalctl -u ssh -n 50
```

This command displays the last 50 SSH-related log entries.

---

## Detecting Failed Login Attempts

Repeated failed login attempts may indicate:

* incorrect credentials
* misconfigured SSH keys
* automated attack attempts

Example log entry:

```
Failed password for invalid user admin from 192.168.1.55 port 40322 ssh2
```

Monitoring these logs allows administrators to quickly identify suspicious behavior.

---

## Monitoring Fail2Ban Activity

Fail2Ban automatically monitors logs and blocks IP addresses that repeatedly fail authentication attempts.

Fail2Ban status can be checked using:

```
sudo fail2ban-client status
```

To view SSH protection details:

```
sudo fail2ban-client status sshd
```

This shows:

* currently banned IP addresses
* number of failed attempts detected
* configured protection rules

---

## Lessons Learned

Through this lab, several important concepts were demonstrated:

* how Linux stores system logs
* how to inspect authentication activity
* how to monitor logs in real time
* how security tools like Fail2Ban rely on log analysis

Effective log monitoring allows system administrators to detect problems early and respond quickly to potential security threats.

Log analysis is one of the most valuable diagnostic and security skills for managing Linux systems.
