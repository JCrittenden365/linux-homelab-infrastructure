# Troubleshooting Journal

## Overview

This journal records real problems encountered while building the lab and the steps taken to diagnose and resolve each one. Troubleshooting is documented here as its own skill — systems rarely behave perfectly during initial configuration.

---

## Issue 1 — SSH Key Authentication Failing

**Symptom:**

```
Permission denied (publickey)
```

SSH login for a user failed despite keys having been generated.

**Investigation:**

```bash
ssh -vvv josh@192.168.1.147          # verbose output revealed no key was being offered
cat /home/user/.ssh/authorized_keys  # file was empty
```

**Root Cause:**

The public key had not been correctly copied into `authorized_keys`.

**Resolution:**

```bash
sudo nano /home/user/.ssh/authorized_keys   # pasted correct public key
chmod 600 /home/user/.ssh/authorized_keys
chown user:user /home/user/.ssh -R
```

Login succeeded after correcting the file.

---

## Issue 2 — SSH Login Only Worked With `-i` Flag

**Symptom:**

This worked:

```bash
ssh -i ~/.ssh/id_ed25519_josh josh@server-ip
```

But this failed:

```bash
ssh josh@server-ip
```

**Investigation:**

```bash
ssh -vvv josh@server-ip
```

Verbose output showed the SSH client was not offering the correct key automatically.

**Root Cause:**

The key file used a custom name (`id_ed25519_josh`) rather than the SSH default (`id_ed25519`). The client only auto-loads default key names.

**Resolution:**

An SSH config entry was created on the client:

```
Host lab-server
    HostName 192.168.1.147
    User josh
    IdentityFile ~/.ssh/id_ed25519_josh
```

After this, `ssh lab-server` worked without specifying the key manually.

---

## Issue 3 — Missing `.ssh` Directory on Windows Client

**Symptom:**

`ssh-keygen` on the HP Laptop (Windows) reported that the `.ssh` directory did not exist.

**Root Cause:**

The `.ssh` directory had never been created on the HP Laptop.

**Resolution:**

```powershell
mkdir C:\Users\<username>\.ssh
```

Key generation then proceeded normally.

---

## Issue 4 — Ubuntu Repository Warning During Update

**Symptom:**

```
Tried to start delayed item http://archive.ubuntu.com ... but failed
```

**Root Cause:**

A temporary connectivity issue with one Ubuntu mirror repository.

**Resolution:**

Running the update again resolved it:

```bash
sudo apt update
```

No further action was needed.

---

## Key Debugging Tools Used

| Tool              | Purpose                                         |
| ----------------- | ----------------------------------------------- |
| `ssh -vvv`        | Verbose SSH output for diagnosing auth failures |
| `cat authorized_keys` | Verify key file contents                    |
| `chmod` / `chown` | Fix permission and ownership issues             |
| `systemctl status` | Check service state                            |
| `sudo sshd -t`    | Validate SSH config before restart              |
