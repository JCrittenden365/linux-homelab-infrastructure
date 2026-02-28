# Troubleshooting Journal

## Overview

This document records problems encountered while building the Linux home lab environment and explains how each issue was diagnosed and resolved.

The purpose of this journal is to document real troubleshooting scenarios and the steps taken to investigate and fix them.

Troubleshooting is an important skill for system administrators because systems rarely behave perfectly during initial configuration.

---

# Issue 1 — SSH Key Authentication Failing

## Problem

SSH login attempts for the user **user2** resulted in the following error:

```
Permission denied (publickey)
```

Even though SSH keys had been generated and copied to the server.

---

## Investigation

The following steps were used to diagnose the issue:

1. Checked SSH debug output using:

```
ssh -vvv user2@server-ip
```

2. Verified the contents of the authorized keys file:

```
cat /home/user2/.ssh/authorized_keys
```

3. The file returned **no output**, indicating that the key had not been copied correctly.

---

## Root Cause

The `authorized_keys` file for the user2 user was empty, meaning the server had no public key available for authentication.

---

## Resolution

The correct public key was copied into the file:

```
sudo nano /home/user2/.ssh/authorized_keys
```

File permissions were then verified:

```
chmod 700 /home/user2/.ssh
chmod 600 /home/user2/.ssh/authorized_keys
chown user2:user2 /home/user2/.ssh -R
```

After correcting the file contents and permissions, passwordless login worked successfully.

---

# Issue 2 — SSH Login Only Worked With Identity File

## Problem

SSH login worked when specifying the identity file:

```
ssh -i ~/.ssh/id_ed25519_user1 user1@server-ip
```

But failed when using a normal connection:

```
ssh user1@server-ip
```

---

## Investigation

SSH verbose mode was used to observe authentication behavior:

```
ssh -vvv user1@server-ip
```

The output showed that the SSH client was **not automatically selecting the correct key**.

---

## Root Cause

The SSH client configuration did not include an entry specifying which key should be used for the host.

---

## Resolution

An SSH config file was created on the client system:

```
~/.ssh/config
```

Example configuration:

```
Host lab-server
    HostName 192.168.1.147
    User user1
    IdentityFile ~/.ssh/id_ed25519_user1
```

This allowed connections using a simple command:

```
ssh lab-server
```

---

# Issue 3 — Missing SSH Directory on Windows Client

## Problem

When attempting to generate new SSH keys, the system reported that the `.ssh` directory did not exist.

---

## Investigation

The expected directory location was checked:

```
C:\Users\<username>\.ssh
```

The directory was missing on the client machine.

---

## Root Cause

The SSH configuration directory had not yet been created on the Windows system.

---

## Resolution

The directory was created manually:

```
mkdir C:\Users\<username>\.ssh
```

After creating the directory, SSH keys could be generated normally.

---

# Issue 4 — Ubuntu Repository Warnings During Update

## Problem

The Ubuntu server displayed warnings similar to:

```
Tried to start delayed item http://archive.ubuntu.com ... but failed
```

during package updates.

---

## Investigation

Repository configuration and network connectivity were checked.

The system still successfully retrieved package lists from other mirrors.

---

## Root Cause

The warning was caused by a temporary issue contacting one of the Ubuntu mirror repositories.

---

## Resolution

Running the update command again resolved the issue:

```
sudo apt update
```

Package updates continued normally afterward.

---

# Lessons Learned

Several important troubleshooting techniques were practiced during these exercises:

* using verbose SSH output (`ssh -vvv`)
* verifying file contents
* checking file permissions
* confirming directory structures
* testing network connectivity
* validating configuration files

These troubleshooting skills are essential for diagnosing issues in Linux server environments.

---

# Future Troubleshooting Notes

Additional troubleshooting scenarios will be added to this journal as the lab environment grows and new systems are introduced.
