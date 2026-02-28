
# SSH Hardening

## Overview

After configuring passwordless SSH authentication, the next step in the lab was to harden the SSH service.

SSH hardening reduces the attack surface of the server and protects against common threats such as:

* brute force login attempts
* password guessing attacks
* unauthorized root access

These configurations were tested in a home lab environment to simulate basic Linux server security practices.

---

## Checking the SSH Configuration File

The SSH daemon configuration file is located at:

```
/etc/ssh/sshd_config
```

The configuration was edited using:

```
sudo nano /etc/ssh/sshd_config
```

Before restarting the service, the configuration was validated using:

```
sudo sshd -t
```

This verifies that the configuration contains no syntax errors.

---

## Disable Root Login

Direct root login through SSH is considered insecure.

Configuration:

```
PermitRootLogin no
```

This forces administrators to log in using a normal user account and escalate privileges using sudo.

---

## Disable Password Authentication

Once SSH keys were confirmed working, password authentication was disabled.

Configuration:

```
PasswordAuthentication no
```

This prevents attackers from attempting password-based brute force attacks.

---

## Disable Challenge Response Authentication

Challenge-response authentication was also disabled.

Configuration:

```
ChallengeResponseAuthentication no
```

This prevents alternate password authentication methods from being used.

---

## Restrict Allowed Users

SSH access was restricted to specific users.

Configuration:

```
AllowUsers user1 user2 user3
```

This prevents other system accounts from attempting to log in via SSH.

---

## Restarting the SSH Service

After configuration changes were made, the SSH service was restarted.

Example:

```
sudo systemctl restart ssh
```

Service status can be verified with:

```
sudo systemctl status ssh
```

---

## Testing Configuration Changes

After applying hardening settings, SSH access was tested from client machines.

Successful login:

```
ssh user@192.168.1.147
```

Testing ensured:

* authorized users could log in
* password authentication was disabled
* key-based authentication functioned correctly

---

## Troubleshooting

Several issues were encountered during testing.

### Connection Refused

This can occur if the SSH service is not running or if the configuration contains errors.

Verification command:

```
sudo systemctl status ssh
```

Configuration validation:

```
sudo sshd -t
```

---

### User Access Restrictions

When the `AllowUsers` directive is used, any user not listed will be denied access.

This was observed during testing when certain users could not connect until the configuration was corrected.

---

## Security Improvements

These changes significantly improve the security posture of the server:

* Root login disabled
* Password authentication disabled
* SSH restricted to authorized users
* SSH configuration validated before restart

Combined with additional protections such as firewall rules and intrusion detection, this provides a strong baseline for secure remote administration.

---

## Lessons Learned

Key takeaways from this lab:

* SSH configuration must always be validated before restarting the service
* Disabling password authentication greatly reduces attack risk
* User access restrictions help limit exposure
* Testing after each change prevents accidental lockouts
