
# Fail2Ban Intrusion Prevention

## Overview

After configuring SSH hardening and firewall protection, the next security layer added to the lab environment was **Fail2Ban**.

Fail2Ban is an intrusion prevention system that monitors system logs and automatically blocks IP addresses that show malicious behavior.

In this lab, Fail2Ban was configured to protect the SSH service from brute-force login attacks.

---

## What Fail2Ban Does

Fail2Ban monitors log files for repeated authentication failures. If an IP address exceeds a defined number of failed login attempts, the system automatically blocks that IP address using firewall rules.

Typical protections include:

* brute-force SSH login attempts
* automated attack scripts
* repeated authentication failures

The offending IP address is temporarily banned for a defined period of time.

---

## Installing Fail2Ban

Fail2Ban was installed using the package manager.

Command:

```
sudo apt update
sudo apt install fail2ban
```

After installation, the service automatically starts.

Verify the service status:

```
sudo systemctl status fail2ban
```

---

## Default Configuration

Fail2Ban uses configuration files located in:

```
/etc/fail2ban/
```

Important files include:

* **jail.conf** → default configuration
* **jail.local** → custom configuration

Best practice is to avoid modifying `jail.conf` directly and instead create a `jail.local` file.

---

## Creating a Local Configuration

A custom configuration file was created:

```
sudo nano /etc/fail2ban/jail.local
```

Example configuration used for SSH protection:

```
[sshd]
enabled = true
port = ssh
logpath = /var/log/auth.log
maxretry = 3
bantime = 600
findtime = 600
```

Explanation:

* **enabled** → activates protection for SSH
* **maxretry** → number of failed login attempts allowed
* **bantime** → how long the attacker is blocked (seconds)
* **findtime** → time window for counting failed attempts

---

## Restarting Fail2Ban

After configuration changes, the Fail2Ban service was restarted.

Command:

```
sudo systemctl restart fail2ban
```

Verify that the service is active:

```
sudo systemctl status fail2ban
```

---

## Checking Active Jails

Fail2Ban protections are organized into **jails**.

To view active jails:

```
sudo fail2ban-client status
```

Example output:

```
Status
|- Number of jail: 1
`- Jail list: sshd
```

To inspect the SSH jail:

```
sudo fail2ban-client status sshd
```

---

## Simulating an Attack

To test the system, multiple failed SSH login attempts were generated.

Example test:

```
ssh fakeuser@192.168.1.147
```

After several failed login attempts, Fail2Ban automatically banned the attacking IP.

---

## Viewing Banned IP Addresses

To see which IPs have been banned:

```
sudo fail2ban-client status sshd
```

Example output:

```
Banned IP list: 192.168.1.100
```

This confirms that Fail2Ban detected the attack and blocked the source.

---

## Unbanning an IP Address

If a legitimate user is accidentally banned, the IP address can be removed.

Command:

```
sudo fail2ban-client set sshd unbanip <IP_ADDRESS>
```

Example:

```
sudo fail2ban-client set sshd unbanip 192.168.1.100
```

---

## Security Benefits

Fail2Ban adds an important layer of protection:

* detects brute-force login attempts
* automatically blocks malicious IPs
* integrates with firewall rules
* reduces noise in authentication logs

When combined with SSH hardening and firewall rules, Fail2Ban helps create a layered security model.

---

## Lessons Learned

Key takeaways from this lab:

* Log monitoring can automatically detect attacks
* Security tools can respond without administrator intervention
* Intrusion prevention systems improve server resilience
* Testing security tools helps verify real-world behavior
