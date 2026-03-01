# SSH Passwordless Authentication

## Overview

SSH key-based authentication was configured to allow secure logins from the **HP Laptop (Windows client)** to the **Dell Laptop (Debian 12 server)** and the VMs on the Dell Desktop — all without passwords.

Key-based authentication is preferred over passwords because:

- No credentials are transmitted during login
- Brute-force attacks are far less effective
- Access is controlled per user via individual key pairs

---

## Environment

| Machine          | Role          | OS / IP            |
| ---------------- | ------------- | ------------------ |
| HP Laptop        | SSH Client    | Windows            |
| Dell Laptop      | Primary Server| Debian 12 — 192.168.1.147 |
| Debian VM        | Test Server   | Debian (VM on Dell Desktop) |
| Ubuntu Server VM | Test Server   | Ubuntu — 192.168.1.122 |

---

## Key Generation (HP Laptop — Windows)

Keys were generated on the HP Laptop using the Windows built-in OpenSSH client.

```powershell
ssh-keygen -t ed25519 -f $env:USERPROFILE\.ssh\id_ed25519_username -C "username@lab"
```

This produces two files:

| File                      | Purpose                       |
| ------------------------- | ----------------------------- |
| `id_ed25519_username`     | Private key — stays on client |
| `id_ed25519_username.pub` | Public key — copied to server |

**ed25519** was chosen because it is modern, compact, and recommended by current SSH security guidelines.

---

## Installing the Public Key on the Server

The public key is placed in the target user's `authorized_keys` file on the Dell Laptop server.

```bash
mkdir ~/.ssh
chmod 700 ~/.ssh
nano ~/.ssh/authorized_keys     # paste public key here
chmod 600 ~/.ssh/authorized_keys
```

File permissions confirmed:

![File Permissions](screenshots/File_Permissions.png)

---

## Testing the Connection

Login was tested from the HP Laptop (Windows):

```powershell
ssh -i $env:USERPROFILE\.ssh\id_ed25519_josh josh@192.168.1.147
```

Successful passwordless login:

![Passwordless Login](screenshots/Passwordless_Login.png)

---

## SSH Config File

To avoid specifying the key file manually every time, an SSH config file was created on the HP Laptop:

**Location:** `C:\Users\<username>\.ssh\config`

```
Host lab-server
    HostName 192.168.1.147
    User josh
    IdentityFile C:\Users\<username>\.ssh\id_ed25519_josh
```

After this, connecting is as simple as:

```powershell
ssh lab-server
```

This same approach was used to configure shortcuts for the VMs on the Dell Desktop.

---

## Troubleshooting

Real issues encountered during setup are documented in the [Troubleshooting Journal](troubleshooting-journal.md), including:

- Empty `authorized_keys` file causing `Permission denied (publickey)`
- SSH not automatically selecting a custom-named key file
- Missing `.ssh` directory on the Windows client (HP Laptop)
