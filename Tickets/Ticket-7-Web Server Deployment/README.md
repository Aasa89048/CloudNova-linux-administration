# Ticket 007 -- Web Server Deployment

## Scenario

A development team required a web server to host a static landing page
before the application backend was ready. A Linux server was configured
to deploy the Nginx web server, host static web content, allow HTTP
traffic through the firewall, and ensure the service automatically
started during system boot. During deployment, an existing Apache web
server caused a port conflict, which was identified and resolved as part
of the deployment process.

------------------------------------------------------------------------

## Description

Deploy and configure the Nginx web server on Ubuntu Linux. Verify the
service is operational, deploy a custom static website, configure the
firewall to allow HTTP traffic, enable automatic service startup, and
troubleshoot service startup issues caused by a conflicting web server.

------------------------------------------------------------------------

## Objectives

- Update the package repository.
- Install the Nginx web server.
- Verify the service status.
- Troubleshoot service startup failures.
- Identify processes using network ports.
- Resolve web server port conflicts.
- Deploy a custom static website.
- Verify website accessibility using both the browser and command line.
- Configure automatic service startup.
- Configure firewall rules for HTTP and HTTPS access.
- Validate the complete deployment.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Update Package Repository

```bash
sudo apt update
```

Updated the package index to retrieve the latest package information
before installing software.

------------------------------------------------------------------------

## Step 2 -- Install Nginx

```bash
sudo apt install nginx -y
```

Installed the Nginx web server and its required dependencies using the
APT package manager.

------------------------------------------------------------------------

## Step 3 -- Verify Service Status

```bash
sudo systemctl status nginx
```

Verified the service status after installation.

The initial verification showed that the service failed to start because
TCP port **80** was already occupied by another process.

------------------------------------------------------------------------

## Step 4 -- Identify the Port Conflict

```bash
sudo ss -tulpn | grep :80
```

Inspected listening network sockets and identified that the Apache web
server (`apache2`) was already listening on TCP port **80**, preventing
Nginx from starting.

------------------------------------------------------------------------

## Step 5 -- Resolve the Service Conflict

Stopped the Apache web server:

```bash
sudo systemctl stop apache2
```

Started the Nginx service:

```bash
sudo systemctl start nginx
```

Verified successful startup:

```bash
sudo systemctl status nginx
```

Output confirmed:

```text
Active: active (running)
```

------------------------------------------------------------------------

## Step 6 -- Verify the Default Web Root

Listed the default web content directory:

```bash
ls -l /var/www/html
```

Verified that Nginx serves website content from:

```text
/var/www/html
```

------------------------------------------------------------------------

## Step 7 -- Deploy a Static Website

Edited the default website:

```bash
sudo nano /var/www/html/index.html
```

Replaced the default Nginx welcome page with a custom HTML page
containing project information.

------------------------------------------------------------------------

## Step 8 -- Verify Website Deployment

Verified the website using the command line:

```bash
curl http://localhost
```

Confirmed that the custom HTML page was successfully served by the Nginx
web server.

The deployment was also verified through the Firefox web browser.

------------------------------------------------------------------------

## Step 9 -- Configure Automatic Startup

Verified that Nginx was configured to start automatically during system
boot.

```bash
sudo systemctl is-enabled nginx
```

Output:

```text
enabled
```

------------------------------------------------------------------------

## Step 10 -- Configure the Firewall

Verified firewall status:

```bash
sudo ufw status
```

Allowed HTTP and HTTPS traffic:

```bash
sudo ufw allow "Nginx Full"
```

Enabled the firewall:

```bash
sudo ufw enable
```

Verified the firewall configuration:

```bash
sudo ufw status
```

Output confirmed:

```text
Status: active

To                         Action      From
--                         ------      ----
Nginx Full                 ALLOW       Anywhere
Nginx Full (v6)            ALLOW       Anywhere (v6)
```

------------------------------------------------------------------------

## Step 11 -- Final Verification

Verified the Nginx service:

```bash
sudo systemctl status nginx
```

Verified website accessibility:

```bash
curl http://localhost
```

Verified firewall configuration:

```bash
sudo ufw status
```

Confirmed that:

- Nginx service was running.
- Custom website was successfully deployed.
- Website was accessible locally.
- Firewall rules allowed HTTP and HTTPS traffic.
- Nginx was configured to start automatically after reboot.

------------------------------------------------------------------------

## Issue Encountered

During deployment, Nginx failed to start because TCP port **80** was
already being used by an existing Apache web server.

The issue was diagnosed using:

```bash
sudo ss -tulpn | grep :80
```

Apache was identified as the conflicting service.

The conflict was resolved by stopping Apache:

```bash
sudo systemctl stop apache2
```

After the port was released, Nginx started successfully:

```bash
sudo systemctl start nginx
```

This troubleshooting exercise demonstrates practical Linux
administration skills including service diagnostics, port inspection,
and conflict resolution.

------------------------------------------------------------------------

## Outcome

Successfully deployed and configured the Nginx web server on Ubuntu
Linux. A custom static website was deployed and verified, firewall rules
were configured, automatic service startup was enabled, and a production
service startup issue caused by an Apache port conflict was diagnosed
and resolved.

------------------------------------------------------------------------

## Architecture

```text
                Client Browser
                      │
                      ▼
              HTTP Request (Port 80)
                      │
                      ▼
                Ubuntu Linux Server
                      │
                      ▼
                 UFW Firewall
          (Nginx Full Rule Allowed)
                      │
                      ▼
                 Nginx Web Server
                      │
                      ▼
             /var/www/html/index.html
                      │
                      ▼
            Static HTML Website Served
```

------------------------------------------------------------------------

## Key Linux Concepts Demonstrated

- Package management
- Nginx web server
- Linux services (systemd)
- TCP/IP networking
- Listening ports
- Network sockets
- Firewall management
- Static website hosting
- HTTP service verification
- Service persistence
- Linux troubleshooting

------------------------------------------------------------------------

## Linux Utilities Used

- apt
- systemctl
- ss
- nginx
- curl
- nano
- ufw
- ls

------------------------------------------------------------------------

## Skills Demonstrated

### Linux Administration

- Package installation
- Web server deployment
- Service management
- Firewall configuration
- Static website deployment

### System Administration

- Service verification
- Automatic service startup
- HTTP service validation
- Network service management

### Networking

- TCP port inspection
- HTTP service verification
- Firewall rule management
- Network troubleshooting

### Troubleshooting

- Diagnosed service startup failure
- Identified port conflicts
- Resolved Apache and Nginx service conflict
- Verified successful service deployment

------------------------------------------------------------------------

## Verification Checklist

- [x] Package repository updated
- [x] Nginx installed
- [x] Service status verified
- [x] Port conflict identified
- [x] Apache service stopped
- [x] Nginx started successfully
- [x] Default web root verified
- [x] Custom website deployed
- [x] Website verified using `curl`
- [x] Website verified using browser
- [x] Automatic startup configured
- [x] Firewall rule configured
- [x] Firewall enabled
- [x] Deployment validated