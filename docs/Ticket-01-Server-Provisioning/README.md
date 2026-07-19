Description

A new Ubuntu Server has been deployed in the production environment. Before it can be handed over to the application team, it must be configured according to the company's Linux administration standards.


## Verify the OS

# commands used 
``` bash
cat /etc/os-release
hostnamectl
uname -r
uname -m
```

# Result

| **Item**                |  **Result**            |
|-------------------------|-----------------------|
| Linux Distribution      | Ubuntu                |
| Ubuntu Version          | 24.04.3 LTS           |
| Kernel Version          | 5.15.0-139-generic    |
| System Architecture     | x86_64                |
| Current Hostname        | ubuntu                |


![alt text](image.png)

## 2. System Update

### Objective

Update the operating system to ensure all installed packages have the latest security patches and bug fixes before the server is placed into production.

### Commands Executed

```bash
sudo apt update
sudo apt upgrade -y
sudo apt autoremove -y
sudo apt list --upgradable
```

### Verification

| **Check**                      | **Result** |
|--------------------------------|------------|
| Package lists updated          | ✅ Pass    |
| Installed available updates    | ✅ Pass    |
| Removed obsolete packages      | ✅ Pass    |
| No pending package updates     | ✅ Pass    |

### Notes

During the initial update, the Ubuntu repository temporarily failed to respond. After verifying network connectivity and rerunning the command, the package lists were updated successfully without requiring any configuration changes.

![alt text](image-1.png)

## 3. Hostname Configuration

### Objective

Configure the server hostname according to the company's naming convention.

### Commands Executed

```bash
hostnamectl
sudo hostnamectl set-hostname prod-web-01
sudo nano /etc/hosts
cat /etc/hosts
sudo reboot
```

![alt text](image-2.png)

### Verification

|              **Check**          | **Result** |
|---------------------------------|------------|
| Hostname changed successfully   |   ✅ Pass  |
| `/etc/hosts` updated            |   ✅ Pass  |
| Hostname persisted after reboot |   ✅ Pass  |

### Notes

The server hostname was changed from the default value to `prod-web-01` using `hostnamectl`. The local hostname mapping in `/etc/hosts` was updated, and the configuration was verified after a reboot.

![alt text](image-3.png)


# 4. Create Administrator Account

## Objective

Create a dedicated administrator account named `novaadmin` for system administration instead of using the default user account.

---

## Commands Executed

```bash
sudo adduser cloudadmin
ls -ld /home/cloudadmin
grep "^cloudadmin:" /etc/passwd
```


---

## Verification

|               Check                  |  Result  |
|--------------------------------------|----------|
| User account created                 | ✅ Pass |
| Password configured                  | ✅ Pass |
| Home directory created               | ✅ Pass |
| Default Bash shell assigned          | ✅ Pass |
| User entry verified in `/etc/passwd` | ✅ Pass |

---

## Notes

A dedicated administrator account named `novaadmin` was created. The account was configured with a home directory located at `/home/novaadmin`, the default Bash shell, and a secure password.


# 5. Grant Administrative Privileges

## Objective

Grant the `novaadmin` account administrative privileges by adding it to the `sudo` group and verify that it can execute commands with elevated permissions.

---

## Commands Executed

```bash
groups cloudadmin
sudo usermod -aG sudo cloudadmin
groups cloudadmin
su - cloudadmin
whoami
sudo whoami
exit
```


## Verification

|               Check                |   Result |
|------------------------------------|----------|
| User added to `sudo` group         | ✅ Pass |
| Group membership verified          | ✅ Pass |
| Login as `cloudadmin` successful   | ✅ Pass |
| `sudo` authentication successful   | ✅ Pass |
| Administrative privileges verified | ✅ Pass |

---

## Notes

The `novaadmin` account was successfully added to the `sudo` group using `usermod -aG`. Administrative access was verified by executing `sudo whoami`, which returned `root`, confirming that the user can perform privileged system administration tasks.



# 6. Verify User Access

## Objective

Verify that the `novaadmin` account can log in successfully, access its home directory, and execute commands with administrative privileges.

---

## Commands Executed

```bash
su - novaadmin
pwd
whoami
echo $HOME
sudo whoami
exit
```


## Verification

| Check | Result |
|--------|--------|
| Login successful | ✅ Pass |
| Home directory loaded | ✅ Pass |
| Current user verified | ✅ Pass |
| HOME environment variable verified | ✅ Pass |
| Administrative privileges verified | ✅ Pass |

---

## Notes

The `novaadmin` account successfully authenticated and loaded its user environment. The session started in the correct home directory, and the account was able to execute privileged commands using `sudo`.


![alt text](image.png)


# 7. Verify System Configuration

## Objective

Perform a final health check to verify that the server is correctly configured and ready for production deployment.

---

## Commands Executed

```bash
hostnamectl
hostname
whoami
hostname -I
ip a
ip route
df -h
free -h
uptime
sudo systemctl --failed
sudo apt list --upgradable
```


## Verification

|              Check             |  Result  |
|--------------------------------|----------|
| Hostname verified              | ✅ Pass |
| Logged-in user verified        | ✅ Pass |
| IP address assigned            | ✅ Pass |
| Network configuration verified | ✅ Pass |
| Routing table verified         | ✅ Pass |
| Disk usage healthy             | ✅ Pass |
| Memory usage verified          | ✅ Pass |
| System uptime verified         | ✅ Pass |
| No failed services             | ✅ Pass |
| No pending package updates     | ✅ Pass |

---

## Notes

A comprehensive system health check was performed after provisioning. The hostname, network configuration, storage, memory, service status, and package state were verified. The server satisfies all requirements for Ticket #001 and is ready for production deployment.

![alt text](image-4.png)
![alt text](image-5.png)


## Completion Summary

The following tasks were completed successfully:

- ✅ Verified Ubuntu operating system and kernel version
- ✅ Updated package lists
- ✅ Installed all available system updates
- ✅ Removed unnecessary packages
- ✅ Configured the server hostname
- ✅ Created a new administrator account
- ✅ Added the administrator account to the sudo group
- ✅ Verified sudo privileges
- ✅ Confirmed the hostname change
- ✅ Confirmed no pending package updates

Completion Date: 19 July 2026

Result: Server is ready for production use according to the requirements of Ticket and the company's Linux administration standards #001.