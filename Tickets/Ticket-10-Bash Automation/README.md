# Ticket 10 -- Bash Automation

## Scenario

The operations team required a reusable Bash script to automate routine
Linux system health checks. Rather than manually executing multiple
commands to inspect server status, a single script was developed to
collect key system information and present it in a structured, readable
report. The solution improves efficiency, consistency, and reduces the
time required to perform daily administrative tasks.

------------------------------------------------------------------------

## Description

Develop a Bash automation script that generates a Linux system health
report. The script uses variables and reusable functions to display
essential system information, including the server hostname, operating
system, kernel version, uptime, CPU load, memory usage, disk usage,
logged-in users, IP address, and recent failed login attempts.

------------------------------------------------------------------------

## Objectives

-   Create a reusable Bash automation script.
-   Organize the script using variables and functions.
-   Generate a formatted system health report.
-   Retrieve essential Linux system information.
-   Improve script readability and maintainability.
-   Demonstrate Bash scripting best practices.
-   Verify successful execution of the automation script.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Create the Project Directory

```bash
mkdir ~/bash-automation
cd ~/bash-automation
```

Created a dedicated project directory to store the Bash automation
script and related files.

------------------------------------------------------------------------

## Step 2 -- Create the Script

```bash
nano health_check.sh
```

Created a new Bash script that will generate the Linux system health
report.

------------------------------------------------------------------------

## Step 3 -- Add the Shebang and Script Information

```bash
#!/bin/bash
```

Added the Bash interpreter directive to ensure the script executes using
the Bash shell.

Included descriptive comments containing the script title, author, and
purpose to improve readability and maintainability.

------------------------------------------------------------------------

## Step 4 -- Define Variables

```bash
TITLE="Linux System Health Report"
LINE="=================================================="
DATE=$(date)
```

Defined reusable variables that store the report title, separator line,
and current date. Using variables avoids repeating the same values
throughout the script and makes future modifications easier.

------------------------------------------------------------------------

## Step 5 -- Create Reusable Functions

Implemented individual functions to perform specific administrative
tasks.

### Print Report Header

Displays the report title and generation timestamp.

### Display Hostname

Retrieves the current server hostname.

```bash
hostname
```

### Display Operating System

Retrieves the operating system name.

```bash
grep PRETTY_NAME /etc/os-release
```

### Display Kernel Version

Displays the running Linux kernel.

```bash
uname -r
```

### Display System Uptime

Displays how long the server has been running.

```bash
uptime -p
```

### Display CPU Load

Retrieves the current system load average.

```bash
uptime
```

### Display Memory Usage

Displays memory utilization in a human-readable format.

```bash
free -h
```

### Display Disk Usage

Displays filesystem utilization.

```bash
df -h /
```

### Display Logged-in Users

Lists users currently logged into the server.

```bash
who
```

### Display IP Address

Retrieves the server's IP address.

```bash
hostname -I
```

### Display Recent Failed Login Attempts

Searches the authentication log for recent failed SSH login attempts.

```bash
sudo grep "Failed password" /var/log/auth.log | tail -5
```

If the authentication log does not exist, the script displays an
informational message instead of terminating.

------------------------------------------------------------------------

## Step 6 -- Create the Main Program

Executed each function in sequence to produce the complete system health
report.

```bash
print_header
show_hostname
show_os
show_kernel
show_uptime
show_cpu_load
show_memory_usage
show_disk_usage
show_logged_users
show_ip_address
show_failed_logins
print_footer
```

This modular approach separates the program logic from implementation,
making the script easier to maintain and extend.

------------------------------------------------------------------------

## Step 7 -- Make the Script Executable

```bash
chmod +x health_check.sh
```

Granted execute permissions so the script can be run directly.

------------------------------------------------------------------------

## Step 8 -- Execute the Script

```bash
./health_check.sh
```

Executed the Bash automation script and generated the Linux System Health
Report.

------------------------------------------------------------------------

## Outcome

Successfully developed a reusable Bash automation script that collects
and displays important Linux system information in a clean, structured
report. The script demonstrates Bash scripting best practices through
the use of variables, reusable functions, formatted output, and modular
design, making it easier to maintain and expand for future automation
tasks.

------------------------------------------------------------------------

## Workflow

```text
Execute Script
      │
      ▼
Initialize Variables
      │
      ▼
Print Report Header
      │
      ▼
Collect System Information
      │
      ├── Hostname
      ├── Operating System
      ├── Kernel Version
      ├── System Uptime
      ├── CPU Load
      ├── Memory Usage
      ├── Disk Usage
      ├── Logged-in Users
      ├── IP Address
      └── Failed Login Attempts
      │
      ▼
Display Formatted Report
      │
      ▼
Print Completion Message
```

------------------------------------------------------------------------

## Key Linux Concepts Demonstrated

-   Bash scripting
-   Variables
-   Functions
-   Command substitution
-   Script execution
-   File permissions
-   Linux system monitoring
-   Modular programming
-   Process automation
-   Shell scripting best practices

------------------------------------------------------------------------

## Linux Utilities Used

-   bash
-   hostname
-   uname
-   uptime
-   free
-   df
-   who
-   grep
-   awk
-   hostname
-   tr
-   cut
-   chmod
-   nano

------------------------------------------------------------------------

## Skills Demonstrated

### Linux Administration

-   Linux system monitoring
-   System information gathering
-   Bash scripting
-   Command-line automation

### System Administration

-   Health check automation
-   Report generation
-   Server diagnostics
-   Script execution and management

### Bash Scripting

-   Variables
-   Functions
-   Command substitution
-   Formatted output
-   Modular script design

------------------------------------------------------------------------

## Verification Checklist

-   [x] Project directory created
-   [x] Bash script created
-   [x] Shebang added
-   [x] Variables implemented
-   [x] Functions created
-   [x] Report header generated
-   [x] Hostname displayed
-   [x] Operating system displayed
-   [x] Kernel version displayed
-   [x] Uptime displayed
-   [x] CPU load displayed
-   [x] Memory usage displayed
-   [x] Disk usage displayed
-   [x] Logged-in users displayed
-   [x] IP address displayed
-   [x] Failed login check implemented
-   [x] Script made executable
-   [x] System health report successfully generated