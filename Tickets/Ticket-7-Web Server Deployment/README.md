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

-   Update the package repository.
-   Install the Nginx web server.
-   Verify the service status.
-   Troubleshoot service startup failures.
-   Identify processes using network ports.
-   Resolve web server port conflicts.
-   Deploy a custom static website.
-   Verify website accessibility using the browser and command line.
-   Configure automatic service startup.
-   Configure firewall rules for HTTP/HTTPS access.
-   Validate the complete deployment.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Update Package Repository

```bash
sudo apt update