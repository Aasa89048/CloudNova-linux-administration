# Ticket #003 - Shared Development Environment

## Description

The development team requires a shared workspace where multiple administrators can collaborate on application files. Configure a shared project directory, assign the appropriate ownership and group permissions, and verify that all authorized users can create and modify files while maintaining secure access controls.

---

## Environment

- Ubuntu Server 24.04.3 LTS
- VMware Workstation
- Administrator Account: `nova`
- Existing Users:
  - `rashid`
  - `cloudadmin`
- Shared Group: `developers`
- Shared Directory: `/projects/webapp`

---

# Work Performed

## Shared Group Verification

Verified the shared development group and confirmed the assigned members.

```bash
getent group developers
```

Output

```
developers:x:1003:rashid,cloudadmin
```

---

## Shared Directory Verification

Verified the ownership and existing permissions of the shared project directory.

```bash
ls -ld /projects/webapp
```

The directory ownership was confirmed as:

```
Owner : nova
Group : developers
```

---

## Directory Ownership Configuration

Updated the ownership of the shared project directory.

```bash
sudo chown nova:developers /projects/webapp
```

Verified the configuration.

```bash
ls -ld /projects/webapp
```

---

## Shared Directory Permission Configuration

Configured collaborative permissions using the SetGID bit.

```bash
sudo chmod 2770 /projects/webapp
```

Verified the applied permissions.

```bash
ls -ld /projects/webapp
```

Configured permissions:

```
drwxrws---
```

This configuration provides:

- Full access for the directory owner
- Full access for members of the `developers` group
- No access for other users
- Automatic inheritance of the `developers` group for newly created files and directories

---

## Collaborative Access Validation

Logged in using the `cloudadmin` account.

```bash
su - cloudadmin
```

Created a test file inside the shared project directory.

```bash
touch /projects/webapp/cloudadmin.txt
```

Verified file creation.

```bash
ls -l /projects/webapp
```

---

## Group Ownership Validation

Updated the group ownership of the application files.

```bash
sudo chgrp developers /projects/webapp/app.py
sudo chgrp developers /projects/webapp/rashid.txt
```

Verified the updated ownership.

```bash
ls -l /projects/webapp
```

All shared files now belong to the `developers` group.

---

## Shared Access Verification

Logged in using the `rashid` account.

```bash
su - rashid
```

Created an additional test file.

```bash
touch /projects/webapp/test.txt
```

Verified successful file creation.

```bash
ls -l /projects/webapp
```

Confirmed that authorized users within the `developers` group can create files inside the shared directory without requiring elevated privileges.

---

# Validation

The following checks were completed successfully:

- Developers group verified
- Shared directory ownership configured
- Shared directory permissions configured
- SetGID permission applied
- Group inheritance verified
- Shared file ownership updated
- Collaborative write access validated
- Multiple user access successfully verified

---

# Result

The shared development environment has been successfully configured.

The environment now provides:

- Dedicated shared project directory
- Centralized group-based access control
- Secure collaborative permissions
- Automatic group inheritance using SetGID
- Multi-user write access for authorized developers
- Restricted access for unauthorized users

The shared development environment is ready for collaborative application development in accordance with the company's Linux administration standards.