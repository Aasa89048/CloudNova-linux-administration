# Ticket 008 -- Backup Strategy

## Scenario

A production Linux server stores critical application data and
configuration files that must be protected against accidental deletion,
hardware failure, or software corruption. A backup strategy was
implemented to create compressed backups, verify archive integrity,
restore data when required, and automate recurring backups using the
Linux cron scheduler.

------------------------------------------------------------------------

## Description

Implement a backup strategy using native Linux utilities. Create a
compressed archive of application files, verify the backup contents,
restore deleted data, and automate scheduled backups using `cron` to
ensure regular protection of application data.

------------------------------------------------------------------------

## Objectives

-   Create sample application data.
-   Create a dedicated backup directory.
-   Generate a compressed backup archive.
-   Verify archive integrity.
-   Simulate data loss.
-   Restore application data from the backup.
-   Automate recurring backups using `cron`.
-   Validate the backup strategy.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Create Sample Application Data

Created a sample application directory:

```bash
mkdir -p ~/projects/webapp
```

Created sample application files:

```bash
echo "Application Configuration" > ~/projects/webapp/config.txt
echo "Application Log" > ~/projects/webapp/app.log
echo "Database Connection Settings" > ~/projects/webapp/database.conf
```

Verified the files:

```bash
ls -lh ~/projects/webapp
```

------------------------------------------------------------------------

## Step 2 -- Create a Backup Directory

Created a dedicated directory to store backup archives.

```bash
mkdir -p ~/backups
```

Verified:

```bash
ls -ld ~/backups
```

------------------------------------------------------------------------

## Step 3 -- Create a Compressed Backup

Created a compressed archive of the application directory.

```bash
tar -czvf ~/backups/webapp.tar.gz ~/projects/webapp
```

This generated a compressed **tar.gz** archive containing the complete
application directory.

------------------------------------------------------------------------

## Step 4 -- Verify the Backup Archive

Verified that the archive was successfully created.

```bash
ls -lh ~/backups
```

Verified archive contents without extracting:

```bash
tar -tzvf ~/backups/webapp.tar.gz
```

Confirmed that all application files were present inside the archive.

------------------------------------------------------------------------

## Step 5 -- Simulate Data Loss

Removed the original application directory to simulate accidental data
loss.

```bash
rm -rf ~/projects/webapp
```

Verified removal:

```bash
ls ~/projects
```

------------------------------------------------------------------------

## Step 6 -- Restore the Backup

Restored the archived data to its original location.

```bash
tar -xzvf ~/backups/webapp.tar.gz -C /
```

Verified successful restoration:

```bash
ls -R ~/projects/webapp
```

All application files were successfully restored.

------------------------------------------------------------------------

## Step 7 -- Configure Automatic Backups

Opened the user's crontab:

```bash
crontab -e
```

Configured a daily backup job:

```cron
0 2 * * * tar -czf /home/nova/backups/webapp.tar.gz /home/nova/projects/webapp
```

This schedule performs a compressed backup every day at **2:00 AM**.

Verified the scheduled task:

```bash
crontab -l
```

------------------------------------------------------------------------

## Step 8 -- Final Verification

Verified:

```bash
tar -tzvf ~/backups/webapp.tar.gz
```

Verified:

```bash
ls -R ~/projects/webapp
```

Verified:

```bash
crontab -l
```

Confirmed that:

- Backup archive was successfully created.
- Archive contents were valid.
- Application files were restored successfully.
- Automatic backup scheduling was configured.

------------------------------------------------------------------------

## Issue Encountered

During implementation, the application directory was initially owned by
the **root** user, preventing the normal user from creating files within
the directory.

Verified ownership:

```bash
ls -ld ~/projects/webapp
```

Resolved by changing ownership:

```bash
sudo chown nova:nova ~/projects/webapp
```

After updating ownership, the application files were created
successfully.

------------------------------------------------------------------------

## Outcome

Successfully implemented a Linux backup strategy using native command-line
utilities. Application data was archived, validated, restored after
simulated data loss, and scheduled for automatic daily backups using
`cron`.

------------------------------------------------------------------------

## Architecture

```text
        Application Files
               │
               ▼
        tar + gzip Compression
               │
               ▼
      Backup Archive (.tar.gz)
               │
               ▼
      Backup Verification
               │
               ▼
      Restore When Required
               │
               ▼
     Automated Daily Backup
           (cron Scheduler)
```

------------------------------------------------------------------------

## Key Linux Concepts Demonstrated

- File archiving
- Compression
- Data backup
- Data restoration
- Backup verification
- Linux scheduling
- Cron jobs
- Disaster recovery
- File ownership
- Backup automation

------------------------------------------------------------------------

## Linux Utilities Used

- tar
- gzip
- cron
- crontab
- mkdir
- ls
- rm
- chown

------------------------------------------------------------------------

## Skills Demonstrated

### Linux Administration

- Backup management
- Archive creation
- Data restoration
- File ownership management
- Backup verification

### System Administration

- Backup scheduling
- Cron configuration
- Disaster recovery
- Data protection

### Troubleshooting

- File permission troubleshooting
- Ownership correction using `chown`
- Archive validation
- Restore verification

------------------------------------------------------------------------

## Verification Checklist

-   [x] Sample application data created
-   [x] Backup directory created
-   [x] Compressed backup archive created
-   [x] Archive contents verified
-   [x] Data loss simulated
-   [x] Backup successfully restored
-   [x] Cron job configured
-   [x] Scheduled backup verified
-   [x] Backup strategy validated