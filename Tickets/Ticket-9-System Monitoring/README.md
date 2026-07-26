# Ticket 09 -- System Monitoring

## Scenario

A production Linux web server experienced intermittent performance
concerns during routine operations. A system health assessment was
required to monitor CPU utilization, memory consumption, disk usage,
running processes, network status, active user sessions, and system logs
to verify overall server health and identify any potential resource
bottlenecks.

------------------------------------------------------------------------

## Description

Perform a comprehensive health check of the Linux server using standard
system monitoring utilities. Inspect system uptime, load averages,
running processes, CPU and memory utilization, filesystem usage, storage
devices, network interfaces, active connections, logged-in users, and
recent system logs to ensure the server is operating normally.

------------------------------------------------------------------------

## Objectives

-   Verify system uptime and load averages.
-   Monitor CPU and memory utilization.
-   Inspect running processes.
-   Identify CPU-intensive processes.
-   Identify memory-intensive processes.
-   Verify available system memory.
-   Analyze filesystem utilization.
-   Inspect storage devices and mounted partitions.
-   Review active user sessions.
-   Inspect listening network ports.
-   Verify network interface configuration.
-   Review recent system logs.
-   Review recent kernel messages.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Verify System Uptime

``` bash
uptime
```

Verified the current system time, server uptime, logged-in users, and
system load averages.

------------------------------------------------------------------------

## Step 2 -- Review Load Average

``` bash
cat /proc/loadavg
```

Displayed the Linux kernel load averages and scheduler statistics to
evaluate current system workload.

------------------------------------------------------------------------

## Step 3 -- Monitor System Resources

``` bash
top
```

Monitored CPU utilization, memory usage, running processes, and overall
system performance in real time.

Exited the monitoring session using:

``` text
q
```

------------------------------------------------------------------------

## Step 4 -- Inspect Running Processes

``` bash
ps aux
```

Displayed all running processes including CPU utilization, memory usage,
process ownership, and execution status.

Displayed a shortened process list:

``` bash
ps aux | head
```

------------------------------------------------------------------------

## Step 5 -- Identify CPU-Intensive Processes

``` bash
ps aux --sort=-%cpu | head
```

Sorted running processes by CPU utilization to identify the highest CPU
consumers.

------------------------------------------------------------------------

## Step 6 -- Identify Memory-Intensive Processes

``` bash
ps aux --sort=-%mem | head
```

Sorted running processes by memory utilization to identify applications
consuming the most RAM.

------------------------------------------------------------------------

## Step 7 -- Verify Memory Utilization

``` bash
free -h
```

Reviewed total, used, available memory, and swap usage to confirm
healthy memory utilization.

------------------------------------------------------------------------

## Step 8 -- Verify Filesystem Utilization

``` bash
df -h
```

Inspected mounted filesystems, available storage capacity, and disk
utilization.

------------------------------------------------------------------------

## Step 9 -- Inspect Storage Devices

``` bash
lsblk
```

Verified attached storage devices, partitions, and mount points.

------------------------------------------------------------------------

## Step 10 -- Review Active User Sessions

``` bash
who
```

Displayed currently logged-in users.

Reviewed active user sessions and executed commands:

``` bash
w
```

------------------------------------------------------------------------

## Step 11 -- Inspect Listening Network Ports

``` bash
ss -tuln
```

Verified active TCP and UDP listening sockets and confirmed expected
network services.

------------------------------------------------------------------------

## Step 12 -- Verify Network Configuration

``` bash
ip addr
```

Displayed network interfaces, assigned IP addresses, and interface
status.

------------------------------------------------------------------------

## Step 13 -- Review Recent System Logs

``` bash
journalctl -n 20
```

Reviewed the latest system journal entries for warnings, errors, or
abnormal system events.

------------------------------------------------------------------------

## Step 14 -- Review Kernel Messages

``` bash
dmesg | tail
```

Displayed the most recent kernel log entries to verify normal hardware
and kernel activity.

------------------------------------------------------------------------

## Outcome

Successfully completed a comprehensive health assessment of the
production Linux server. System resources, running processes, storage
utilization, network configuration, active sessions, and system logs
were inspected. The monitoring results confirmed that CPU, memory, disk
utilization, networking, and system services were operating normally
with no significant resource bottlenecks or critical errors detected.

------------------------------------------------------------------------

## Architecture

``` text
                    Production Linux Server
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
   CPU Monitoring       Memory Monitoring     Disk Monitoring
        │                     │                     │
        ├──────────────┬──────┴──────────────┐      │
        ▼              ▼                     ▼      ▼
      top          free -h           ps aux --sort  df -h
        │
        ▼
 System Performance Analysis
        │
        ├──────────────────────────────────────────────┐
        ▼                                              ▼
 Network Monitoring                             User Monitoring
        │                                              │
        ▼                                              ▼
 ss -tuln, ip addr                               who, w
        │
        ▼
 System & Kernel Logs
        │
        ▼
 journalctl, dmesg
        │
        ▼
 Overall Server Health Verification
```

------------------------------------------------------------------------

## Key Linux Concepts Demonstrated

-   System monitoring
-   Process management
-   CPU utilization
-   Memory management
-   Load averages
-   Filesystem utilization
-   Storage monitoring
-   Network monitoring
-   User session monitoring
-   System logging
-   Kernel logging
-   Performance analysis

------------------------------------------------------------------------

## Linux Utilities Used

-   uptime
-   cat
-   top
-   ps
-   free
-   df
-   lsblk
-   who
-   w
-   ss
-   ip
-   journalctl
-   dmesg

------------------------------------------------------------------------

## Skills Demonstrated

### Linux Administration

-   System monitoring
-   Process management
-   Performance analysis
-   Resource utilization monitoring
-   Filesystem monitoring
-   Network monitoring

### System Administration

-   Production server health assessment
-   User session monitoring
-   Log analysis
-   Performance verification
-   System diagnostics

### Troubleshooting

-   CPU bottleneck identification
-   Memory utilization analysis
-   Process inspection
-   Disk utilization verification
-   Network verification
-   System log review
-   Kernel log inspection

------------------------------------------------------------------------

## Verification Checklist

-   [x] System uptime verified
-   [x] Load average reviewed
-   [x] CPU utilization monitored
-   [x] Memory utilization verified
-   [x] Running processes inspected
-   [x] CPU-intensive processes identified
-   [x] Memory-intensive processes identified
-   [x] Filesystem utilization verified
-   [x] Storage devices inspected
-   [x] Logged-in users reviewed
-   [x] Listening network ports verified
-   [x] Network configuration inspected
-   [x] System logs reviewed
-   [x] Kernel messages inspected
-   [x] Overall server health validated
