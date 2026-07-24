# Ticket 005 -- Storage Management

## Scenario

A production Linux server required additional storage for application
data. A new virtual disk was attached, partitioned, formatted with the
EXT4 filesystem, mounted to the operating system, and configured for
automatic mounting during system startup to ensure persistent storage
availability.

------------------------------------------------------------------------

## Description

Provision and configure a new storage device on the Linux server by
creating a partition, formatting it with the EXT4 filesystem, mounting
it to the system, and configuring persistent mounting using
`/etc/fstab`. Verify that the storage is successfully mounted and
automatically available after system reboot.

------------------------------------------------------------------------

## Objectives

-   Inspect existing storage devices and filesystems.
-   Analyze current disk usage.
-   Add a new virtual disk to the server.
-   Create a new partition on the disk.
-   Format the partition using the EXT4 filesystem.
-   Create a mount point.
-   Mount the filesystem manually.
-   Configure automatic mounting using `/etc/fstab`.
-   Verify persistent mounting after reboot.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Inspect Storage

``` bash
lsblk
df -h
lsblk -f
```

Verified existing disks, partitions, filesystem types, UUIDs, mount
points, and disk utilization before making changes.

## Step 2 -- Provision Additional Storage

-   Added a new **5 GB SCSI virtual disk** in VMware Workstation.
-   Booted the VM and verified Linux detected the new disk using:

``` bash
lsblk
```

------------------------------------------------------------------------

## Step 3 -- Partition the Disk

``` bash
sudo fdisk /dev/sdb
```

Actions:

``` text
n
p
Enter
Enter
Enter
w
```

Created a primary partition using the entire disk.

------------------------------------------------------------------------

## Step 4 -- Create the Filesystem

``` bash
sudo mkfs.ext4 /dev/sdb1
```

Formatted the partition with the EXT4 filesystem.

Verified:

``` bash
lsblk -f
```

------------------------------------------------------------------------

## Step 5 -- Create a Mount Point

``` bash
mkdir ~/data
```

Created the directory that serves as the mount point.

------------------------------------------------------------------------

## Step 6 -- Mount the Filesystem

``` bash
sudo mount /dev/sdb1 ~/data
```

Verified:

``` bash
mount | grep sdb1
```

------------------------------------------------------------------------

## Step 7 -- Retrieve the UUID

``` bash
sudo blkid /dev/sdb1
```

Retrieved the filesystem UUID for persistent mounting.

------------------------------------------------------------------------

## Step 8 -- Configure Persistent Mounting

Reviewed:

``` bash
cat /etc/fstab
```

Edited:

``` bash
sudo nano /etc/fstab
```

Added:

``` text
UUID=<UUID>   /home/nova/data   ext4   defaults   0   2
```

Validated configuration:

``` bash
sudo mount -a
```

No errors were returned.

------------------------------------------------------------------------

## Step 9 -- Verify

``` bash
mount | grep sdb1
```

Output confirmed the partition was mounted as an EXT4 filesystem with
read-write access.

------------------------------------------------------------------------

## Outcome

Successfully provisioned and configured a persistent storage volume on
Ubuntu Linux. The new filesystem was partitioned, formatted, mounted,
validated, and configured to mount automatically after system startup
using UUID-based configuration in `/etc/fstab`.

------------------------------------------------------------------------

## Architecture

``` text
VMware Virtual Machine
        │
        ▼
 New Virtual Disk (5 GB)
        │
        ▼
 Partition (/dev/sdb1)
        │
        ▼
 EXT4 Filesystem
        │
        ▼
 Mounted at /home/nova/data
        │
        ▼
 Configured in /etc/fstab
        │
        ▼
 Automatic Mount After Reboot
```

------------------------------------------------------------------------

## Key Linux Concepts Demonstrated

-   Block devices
-   Disk partitioning
-   Filesystems
-   EXT4
-   Mount points
-   UUID-based mounting
-   Persistent storage
-   `/etc/fstab`
-   Filesystem verification

------------------------------------------------------------------------

## Linux Utilities Used

-   lsblk
-   df
-   fdisk
-   mkfs.ext4
-   blkid
-   mount
-   nano

------------------------------------------------------------------------

## Skills Demonstrated

### Linux Administration

-   Storage management
-   Filesystem administration
-   Mount management
-   Disk partitioning

### System Administration

-   Persistent filesystem configuration
-   UUID-based storage management
-   Storage verification

### Troubleshooting

-   Filesystem validation
-   Mount verification
-   Configuration testing using `mount -a`

------------------------------------------------------------------------

## Verification Checklist

-   [x] Existing storage inspected
-   [x] New disk detected
-   [x] Partition created
-   [x] EXT4 filesystem created
-   [x] Mount point created
-   [x] Filesystem mounted
-   [x] UUID retrieved
-   [x] `/etc/fstab` configured
-   [x] Configuration validated
-   [x] Persistent storage verified
