# Ticket 006 -- Service Troubleshooting

## Scenario

A production Linux web server experienced a service outage after an invalid configuration change prevented the Apache HTTP Server from starting successfully. The issue was investigated by verifying the service status, reviewing system logs, validating the Apache configuration, correcting the configuration error, restoring the service, and confirming successful application availability.

------------------------------------------------------------------------

## Description

Investigate and resolve an Apache HTTP Server outage by verifying service health, reviewing service logs, validating the Apache configuration, identifying the root cause of the failure, restoring the service, and confirming successful web server operation.

------------------------------------------------------------------------

## Objectives

-   Verify Apache service status.
-   Confirm the service is listening on the correct network port.
-   Verify web server availability.
-   Simulate a service outage.
-   Review Apache service logs.
-   Simulate a configuration failure.
-   Validate the Apache configuration.
-   Identify and correct the configuration error.
-   Restore the Apache service.
-   Verify successful service recovery.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Verify Service Health

```bash
sudo systemctl status apache2
```

Verified that the Apache HTTP Server was installed, enabled, and running successfully.

------------------------------------------------------------------------

## Step 2 -- Verify Network Availability

```bash
sudo ss -tulpn | grep :80
```

Confirmed that Apache was actively listening on TCP port **80**, allowing incoming HTTP connections.

Verified web server availability.

```bash
curl http://localhost
```

Successfully received the Apache default web page.

------------------------------------------------------------------------

## Step 3 -- Simulate a Service Outage

Stopped the Apache service.

```bash
sudo systemctl stop apache2
```

Verified the service status.

```bash
sudo systemctl status apache2
```

Observed:

```text
Active: inactive (dead)
```

Confirmed the application became unavailable.

```bash
curl http://localhost
```

------------------------------------------------------------------------

## Step 4 -- Investigate the Incident

Reviewed recent Apache service logs.

```bash
sudo journalctl -u apache2 --since "10 minutes ago"
```

Verified recent service events and confirmed the service stop operation.

------------------------------------------------------------------------

## Step 5 -- Simulate a Configuration Failure

Created a backup of the Apache configuration.

```bash
sudo cp /etc/apache2/apache2.conf /etc/apache2/apache2.conf.bak
```

Introduced an invalid configuration directive into the Apache configuration file.

Restarted Apache.

```bash
sudo systemctl restart apache2
```

Verified the failure.

```bash
sudo systemctl status apache2
```

Observed:

```text
Active: failed (Result: exit-code)
```

------------------------------------------------------------------------

## Step 6 -- Diagnose the Root Cause

Validated the Apache configuration.

```bash
sudo apache2ctl configtest
```

The validation utility identified the exact syntax error.

Example output:

```text
Invalid command 'InvalidDirective'
```

Removed the invalid configuration directive.

Validated the configuration again.

```bash
sudo apache2ctl configtest
```

Output:

```text
Syntax OK
```

------------------------------------------------------------------------

## Step 7 -- Restore the Service

Restarted the Apache HTTP Server.

```bash
sudo systemctl restart apache2
```

Verified successful recovery.

```bash
sudo systemctl status apache2
```

Confirmed:

```text
Active: active (running)
```

Verified application availability.

```bash
curl http://localhost
```

Successfully received the Apache default web page.

------------------------------------------------------------------------

## Outcome

Successfully diagnosed and resolved an Apache HTTP Server startup failure caused by an invalid configuration directive. The configuration was validated, corrected, and the service was restored. Final verification confirmed successful web server operation and application availability.

------------------------------------------------------------------------

## Architecture

```text
Apache Configuration Change
            │
            ▼
 Invalid Configuration Directive
            │
            ▼
 Apache Service Failed
            │
            ▼
 systemctl status
            │
            ▼
 journalctl Logs
            │
            ▼
 apache2ctl configtest
            │
            ▼
 Configuration Corrected
            │
            ▼
 Apache Restarted
            │
            ▼
 curl Verification
            │
            ▼
 Service Restored
```

------------------------------------------------------------------------

## Key Linux Concepts Demonstrated

-   Linux services
-   systemd
-   Service management
-   Service status monitoring
-   Apache HTTP Server
-   Network sockets
-   TCP port verification
-   System logging
-   Configuration validation
-   Root cause analysis
-   Service recovery

------------------------------------------------------------------------

## Linux Utilities Used

-   systemctl
-   journalctl
-   ss
-   curl
-   apache2ctl
-   cp
-   nano

------------------------------------------------------------------------

## Skills Demonstrated

### Linux Administration

-   Service management
-   Apache administration
-   Configuration management
-   Log analysis

### System Administration

-   Service verification
-   Configuration validation
-   Network service verification
-   Incident recovery

### Troubleshooting

-   Root cause analysis
-   Service diagnostics
-   Configuration troubleshooting
-   Log investigation
-   Service recovery validation

------------------------------------------------------------------------

## Verification Checklist

-   [x] Apache service verified
-   [x] Listening port verified
-   [x] Web server tested
-   [x] Service outage simulated
-   [x] Service logs reviewed
-   [x] Configuration backup created
-   [x] Configuration failure simulated
-   [x] Root cause identified
-   [x] Apache configuration validated
-   [x] Configuration corrected
-   [x] Service restored
-   [x] Application availability verified