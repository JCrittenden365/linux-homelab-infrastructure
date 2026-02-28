# SSH Passwordless Authentication

## Overview

In this lab, SSH key-based authentication was configured to allow secure logins to Linux servers without using passwords.

Using SSH keys significantly improves security because:

* Passwords are not transmitted during login
* Brute-force attacks are far less effective
* Access can be tightly controlled per user

This setup was implemented for multiple users in the lab environment.

---

## Environment

Server:
Debian Server
192.168.1.147

Client systems:
Windows machines using the built-in OpenSSH client.

Key type used:

```
ed25519
```

This key type was chosen because it is modern, secure, and recommended by most current SSH security guidelines.

---

## Generating SSH Keys (Windows)

Keys were generated using the Windows OpenSSH client.

Example command:

```
ssh-keygen -t ed25519 -f $env:USERPROFILE\.ssh\id_ed25519_username -C "username@lab"
```

This created two files:

Private key

```
id_ed25519_username
```

Public key

```
id_ed25519_username.pub
```

The private key stays on the client machine.
The public key is copied to the server.

---

## Installing the Public Key on the Server

The public key must be placed in the user's `authorized_keys` file.

Example:

```
/home/user/.ssh/authorized_keys
```

Steps performed:

1. Create the `.ssh` directory

```
mkdir ~/.ssh
```

2. Set proper permissions

```
chmod 700 ~/.ssh
```

3. Add the public key to the authorized_keys file

```
nano ~/.ssh/authorized_keys
```

4. Set correct permissions

```
chmod 600 ~/.ssh/authorized_keys
```

---

## Testing SSH Login

The connection was tested from the Windows client.

Example:

```
ssh -i $env:USERPROFILE\.ssh\id_ed25519_user user@192.168.1.147
```

Successful login indicates the server accepted the key.

---

## Troubleshooting Encountered

Several issues occurred during setup that required troubleshooting.

### Empty authorized_keys File

During initial testing, the `authorized_keys` file for one user was empty.

This prevented SSH authentication even though the key had been generated correctly.

Verification command:

```
cat ~/.ssh/authorized_keys
```

Fix:

The correct public key was copied into the file.

---

### SSH Using the Wrong Key

When connecting using:

```
ssh user@192.168.1.122
```

Authentication failed.

However, the following worked:

```
ssh -i $env:USERPROFILE\.ssh\id_ed25519_user user@192.168.1.122
```

Reason:

SSH only automatically loads default key names such as:

```
id_rsa
id_ed25519
```

Because the key file had a custom name, it had to be specified manually.

---

## SSH Config Shortcut

To simplify login commands, an SSH config file was created on the client machine.

Location:

```
C:\Users\<username>\.ssh\config
```

Example configuration:

```
Host lab-user
    HostName 192.168.1.147
    User user
    IdentityFile C:\Users\<username>\.ssh\id_ed25519_user
```

After creating this file, SSH connections could be made with:

```
ssh lab-user
```

This greatly simplifies connecting to multiple systems.

---

## Security Benefits

Key-based authentication provides several important security advantages:

* No passwords transmitted over the network
* Strong cryptographic authentication
* Easier auditing of user access
* Compatible with automation tools

This configuration is widely used in production Linux environments.

---

## Lessons Learned

Key takeaways from this setup:

* SSH permissions are strict and must be correct
* The `authorized_keys` file must contain the correct public key
* Custom key names require either `-i` or an SSH config entry
* Debugging with `ssh -vvv` is extremely helpful when troubleshooting authentication problems

