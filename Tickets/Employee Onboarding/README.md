
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


## Part-2 Description

A new web application is scheduled for deployment on the server. Before deployment, the required application directory structure must be provisioned, ownership assigned to the application administrator, access permissions configured, and the administrator's access validated according to the company's Linux administration standards.

---

# Work Performed

## Application Directory Provisioning

Created the application directory structure.

```bash
sudo mkdir -p /projects/webapp
```

Verified the directory.

```bash
ls -ld /projects/webapp
```

---

## Directory Ownership Configuration

Assigned ownership of the application directory to the application administrator.

```bash
sudo chown rashid:rashid /projects/webapp
```

Verified the ownership configuration.

```bash
ls -ld /projects/webapp
```

The application directory is now owned by:

```
Owner : rashid
Group : rashid
```

---

## Application Access Validation

Logged into the administrator account.

```bash
su - rashid
```

Created a test application file.

```bash
touch /projects/webapp/app.py
```

Verified file ownership.

```bash
ls -l /projects/webapp
```

The test file was successfully created under the administrator account, confirming write access to the application directory.

---

## Directory Permission Configuration

Configured secure permissions for the application directory.

```bash
sudo chmod 750 /projects/webapp
```

Verified the applied permissions.

```bash
ls -ld /projects/webapp
```

Configured permissions:

```
drwxr-x---
```

This configuration grants full access to the directory owner, read and execute permissions to the assigned group, and denies access to all other users.

---

## User Account Verification

Verified the administrator account configuration.

```bash
getent passwd rashid
```

Confirmed the following information:

- Username
- User ID (UID)
- Group ID (GID)
- Home directory
- Default login shell

---

## Administrative Privilege Verification

Verified the administrator's assigned sudo privileges.

```bash
sudo -l -U rashid
```

Administrative permissions were successfully validated.

---

## Group Management

Created a dedicated application group.

```bash
sudo groupadd developers
```

Added the administrator account to the group.

```bash
sudo usermod -aG developers rashid
```

Verified group membership.

```bash
groups rashid
```

Verified the group ownership of the application directory.

```bash
sudo chown :developers /projects/webapp
```

Confirmed the updated ownership.

```bash
ls -ld /projects/webapp
```

The application directory is now configured with:

```
Owner : rashid
Group : developers
```

This configuration enables future members of the **developers** group to access the application directory without changing the directory owner.

---

# Validation

The following checks were completed successfully:

- Application directory created
- Directory ownership assigned
- Application administrator write access verified
- Directory permissions configured
- Administrator account information verified
- Administrative privileges validated
- Application group created
- Administrator added to the application group
- Directory group ownership updated successfully

---

# Result

The application directory has been successfully provisioned and configured for deployment.

The environment now includes:

- Dedicated application directory
- Administrator ownership
- Secure directory permissions
- Verified administrator write access
- Dedicated application group
- Group ownership configured for collaborative administration

The server is prepared for application deployment in accordance with the company's Linux administration standards.




