
# User Management and SSH Access

## Overview

One of the key goals of this lab was to simulate a real Linux server environment where multiple users can securely access a system using SSH.

This required creating user accounts, configuring SSH key authentication, and ensuring proper permissions were applied to each user's `.ssh` directory.

---

## Creating User Accounts

Users were created on the Debian server using the standard Linux user management tools.

Example:

```
sudo adduser user1
sudo adduser user2
```

This automatically created the user home directories:

```
/home/user1
/home/user2
```

Each user received their own login shell and environment.

---

## Preparing SSH Directories

For key authentication to work, each user requires a properly configured `.ssh` directory.

```
sudo mkdir -p /home/user1/.ssh
sudo mkdir -p /home/user2/.ssh
```

Permissions were restricted for security:

```
sudo chmod 700 /home/user1/.ssh
sudo chmod 700 /home/user2/.ssh
```

Ownership was set to the correct user:

```
sudo chown user1:user1 /home/user1/.ssh
sudo chown user2:user2 /home/user2/.ssh
```

---

## SSH Key Authentication

SSH keys were generated on the client machine using the ED25519 algorithm.

Example:

```
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_user1
```

The public key was copied to the server and placed in:

```
/home/user1/.ssh/authorized_keys
```

Permissions were then restricted:

```
chmod 600 authorized_keys
```

---

## Client SSH Configuration

To simplify SSH connections, a local SSH config file was created on the client system.

Example:

```
Host lab-user1
    HostName 192.168.1.147
    User user1
    IdentityFile ~/.ssh/id_ed25519_user1
```

This allows login using:

```
ssh lab-user1
```

instead of specifying the key manually.

---

## Troubleshooting Encountered

During setup, several issues occurred that required troubleshooting.

### Empty authorized_keys File

At one point, the `authorized_keys` file for user1 was empty.
This caused SSH login attempts to fail with:

```
Permission denied (publickey)
```

After verifying the file contents using:

```
cat /home/user1/.ssh/authorized_keys
```

the public key was correctly re-added and permissions verified.

---

### Key Not Automatically Selected

Another issue occurred where SSH only worked when manually specifying the key:

```
ssh -i ~/.ssh/id_ed25519_user2 user2@server
```

This was resolved by adding the key to the SSH client configuration file.

---

## Lessons Learned

This exercise demonstrated several important system administration concepts:

* Linux user management
* SSH key authentication
* secure file permissions
* troubleshooting authentication failures
* simplifying SSH access using client configuration files

These skills are essential for securely managing remote Linux servers.
