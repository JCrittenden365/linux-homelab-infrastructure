# User Management and SSH Access

## Overview

Multiple user accounts were created on the Dell Laptop (Debian 12 server) to simulate a real multi-user Linux environment. Each user was configured with their own SSH key for secure, independent access.

---

## Creating User Accounts

```bash
sudo adduser carrie
sudo adduser alex
```

This creates home directories at `/home/carrie` and `/home/alex` automatically.

Users confirmed in `/etc/passwd`:

![User Management](screenshots/User_Management.png)

---

## Preparing SSH Directories

Each user needs a properly configured `.ssh` directory before key authentication will work.

```bash
sudo mkdir -p /home/carrie/.ssh
sudo chmod 700 /home/carrie/.ssh
sudo chown carrie:carrie /home/carrie/.ssh
```

Repeat for each user.

---

## Installing SSH Keys

Keys were generated on the client for each user (see [SSH Passwordless Authentication](ssh-passwordless-authentication.md)) and then placed in each user's `authorized_keys` file:

```bash
sudo nano /home/carrie/.ssh/authorized_keys
# paste carrie's public key

sudo chmod 600 /home/carrie/.ssh/authorized_keys
sudo chown carrie:carrie /home/carrie/.ssh/authorized_keys
```

File permissions and key contents verified:

![File Permissions](screenshots/File_Permissions.png)

---

## Client SSH Config

To simplify connecting as different users, entries were added to the client SSH config file:

```
Host lab-carrie
    HostName 192.168.1.147
    User carrie
    IdentityFile ~/.ssh/id_ed25519_carrie

Host lab-alex
    HostName 192.168.1.147
    User alex
    IdentityFile ~/.ssh/id_ed25519_alex
```

Each user can then connect with:

```bash
ssh lab-carrie
ssh lab-alex
```

---

## Restricting SSH Access

The `AllowUsers` directive in `sshd_config` on the Dell Laptop ensures only the configured users can connect via SSH:

```
AllowUsers josh carrie alex
```

Any system account not listed is denied SSH access. See [SSH Hardening](ssh-hardening.md) for the full configuration.

---

## Troubleshooting

Issues encountered during this setup (empty `authorized_keys`, wrong key being selected) are documented in the [Troubleshooting Journal](troubleshooting-journal.md).
