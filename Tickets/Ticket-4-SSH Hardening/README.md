# Ticket 04 – SSH Hardening

## Description

Secure the Linux server by configuring SSH according to security best practices. This task includes installing and verifying the OpenSSH Server, configuring SSH key-based authentication, hardening the SSH daemon configuration, and validating secure remote access from a Windows client.

---

## Objective

- Install and configure the OpenSSH Server.
- Enable secure SSH key authentication.
- Disable insecure authentication methods.
- Restrict SSH access to authorized users.
- Validate the SSH configuration.
- Verify secure remote administration after hardening.

---

## Implementation

### Step 1 – Install OpenSSH Server

Verified that the SSH service was not available on the system.

```bash
sudo systemctl status ssh
```

Installed the OpenSSH Server package.

```bash
sudo apt update
sudo apt install openssh-server -y
```

Verified that the SSH service was successfully installed and running.

```bash
sudo systemctl status ssh
```

---

### Step 2 – Verify SSH Service

Verified the server IP address and confirmed that SSH was listening on TCP port 22.

```bash
hostname -I
sudo ss -tlnp | grep :22
```

Confirmed:

- SSH service is active.
- Server is reachable through the assigned IP address.
- SSH daemon is listening on the default SSH port.

---

### Step 3 – Generate SSH Key Pair

Generated a new Ed25519 SSH key pair on the Windows client.

```powershell
ssh-keygen -t ed25519 -C "ahmed@cloudnova"
```

Verified the generated keys.

```powershell
dir $env:USERPROFILE\.ssh
```

Generated files:

- id_ed25519 (Private Key)
- id_ed25519.pub (Public Key)

---

### Step 4 – Configure Public Key Authentication

Created the SSH directory and configured secure permissions.

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

Added the public key.

```bash
nano ~/.ssh/authorized_keys
```

Applied secure permissions to the authorized keys file.

```bash
chmod 600 ~/.ssh/authorized_keys
```

---

### Step 5 – Test SSH Authentication

Connected to the Ubuntu server from Windows using SSH.

```powershell
ssh nova@<Server-IP>
```

Verified that remote access was functioning correctly before applying security restrictions.

---

### Step 6 – Backup SSH Configuration

Created a backup of the SSH daemon configuration.

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```

---

### Step 7 – Harden SSH Configuration

Edited the SSH configuration file.

```bash
sudo nano /etc/ssh/sshd_config
```

Applied the following security settings:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
PermitEmptyPasswords no
MaxAuthTries 3
X11Forwarding no
AllowUsers nova
```

Security improvements:

- Disabled direct root login.
- Disabled password authentication.
- Enforced SSH key authentication.
- Prevented empty password logins.
- Limited authentication attempts.
- Disabled X11 forwarding.
- Restricted SSH access to the authorized user only.

---

### Step 8 – Validate Configuration

Verified the SSH configuration before restarting the service.

```bash
sudo sshd -t
```

No output was returned, confirming that the configuration syntax was valid.

---

### Step 9 – Restart SSH Service

Applied the updated configuration.

```bash
sudo systemctl restart ssh
```

Verified the service status.

```bash
sudo systemctl status ssh
```

Confirmed that the SSH service was running successfully.

---

### Step 10 – Final Verification

Opened a new PowerShell session and established a new SSH connection.

```powershell
ssh nova@<Server-IP>
```

Verified:

- SSH service remained operational.
- Key-based authentication worked successfully.
- Password authentication was disabled.
- Secure remote administration was successfully implemented.

---

## Verification

- ✅ OpenSSH Server installed successfully.
- ✅ SSH service running correctly.
- ✅ SSH listening on port 22.
- ✅ Ed25519 SSH key pair generated.
- ✅ Public key configured successfully.
- ✅ Key-based authentication verified.
- ✅ Root login disabled.
- ✅ Password authentication disabled.
- ✅ SSH access restricted to the authorized user.
- ✅ SSH configuration validated successfully.
- ✅ SSH service restarted successfully.
- ✅ Secure remote access verified after hardening.

---

## Result

The Linux server was successfully hardened for secure remote administration using OpenSSH. SSH key-based authentication was implemented, password-based logins and direct root access were disabled, and access was restricted to authorized users. The final configuration was validated and tested to ensure secure and reliable remote connectivity.