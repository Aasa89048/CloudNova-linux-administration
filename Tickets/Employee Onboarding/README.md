
## Part-1 discription

Provision a new developer account with administrative privileges, verify access, perform account security validation, and configure the required login shell.

---

## Environment

- Ubuntu Server 20.04 LTS
- VMware Workstation
- Administrator Account: `nova`
- Target User: `rashid`

---

# Work Performed

## User Provisioning

Created a new local user account.

```bash
sudo adduser rashid
```

---

## Administrative Access

Granted administrative privileges by adding the user to the sudo group.

```bash
sudo usermod -aG sudo rashid
```

Verified group membership.

```bash
groups rashid
```

---

## Access Validation

Logged into the newly created account.

```bash
su - rashid
```

Verified the active user.

```bash
whoami
```

Output

```
rashid
```

Verified sudo privileges.

```bash
sudo whoami
```

Output

```
root
```

Administrative access confirmed.

---

## Account Security Validation

Locked the account.

```bash
sudo passwd -l rashid
```

Verified status.

```bash
sudo passwd -S rashid
```

Unlocked the account after validation.

```bash
sudo passwd -u rashid
```

---

## Home Directory Verification

Verified that the home directory was created successfully.

```bash
ls -la /home/rashid
```

---

## Login Shell Configuration

Updated the default login shell.

```bash
sudo usermod -s /bin/sh rashid
```

Verified the configuration.

```bash
getent passwd rashid
```

The default login shell is now configured as:

```
/bin/sh
```

This shell was selected to ensure POSIX-compliant script execution where portability is required.

---




# Validation

The following checks were completed successfully:

- User account created
- Home directory created
- Password configured
- Sudo access granted
- Administrative access verified
- Account lock/unlock tested
- Login shell updated
- Account configuration verified

---

# Result

The requested user account was successfully provisioned and configured.

The account has:

- Administrative privileges
- Functional authentication
- Verified home directory
- Updated default login shell
- Successful security validation

The account is ready for operational use.