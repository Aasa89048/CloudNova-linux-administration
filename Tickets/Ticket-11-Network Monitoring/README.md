# Ticket 11 -- Network Troubleshooting

## Scenario

A production Linux application server experienced network connectivity
issues that prevented access to external services, software repositories,
and remote APIs. As the Linux Administrator, the issue needed to be
diagnosed by verifying network interfaces, IP addressing, routing, DNS
configuration, and overall network connectivity to restore normal server
communication.

------------------------------------------------------------------------

## Description

Diagnose and verify the Linux server's network configuration by checking
network interfaces, IP address assignment, routing information, DNS
resolution, and Internet connectivity. Confirm that the server can
communicate with both local and external networks while documenting all
findings.

------------------------------------------------------------------------

## Objectives

-   Verify network interfaces.
-   Check the assigned IP address.
-   Identify the default gateway.
-   Verify routing information.
-   Test connectivity to the local gateway.
-   Test Internet connectivity.
-   Verify DNS name resolution.
-   Review DNS configuration.
-   Inspect active network connections.
-   Document all network information.

------------------------------------------------------------------------

# Implementation

## Step 1 -- Verify Network Interfaces

```bash
ip link show
```

This command displays all network interfaces available on the system
along with their operational state.

Verified:

- Active network interface
- Interface status (UP/DOWN)
- Link state

Result:

```text
Interface: ens33
Status: UP
```

------------------------------------------------------------------------

## Step 2 -- Check IP Address Configuration

```bash
ip addr show
```

or

```bash
ip a
```

This command displays the IP configuration assigned to each network
interface.

Verified:

- IPv4 address
- Subnet mask
- Interface associated with the address

Result:

```text
IP Address : 192.168.229.131
Subnet     : /24
Interface  : ens33
```

------------------------------------------------------------------------

## Step 3 -- Verify Routing Table

```bash
ip route
```

The routing table determines where network traffic is sent. It identifies
the default gateway used to reach external networks.

Verified:

- Default gateway
- Connected network
- Source IP

Result:

```text
Default Gateway : 192.168.229.2
Network         : 192.168.229.0/24
```

------------------------------------------------------------------------

## Step 4 -- Test Local Network Connectivity

```bash
ping -c 4 192.168.229.2
```

The `ping` command sends ICMP Echo Requests to another device. Testing
the default gateway verifies communication with the local network.

Expected result:

```text
4 packets transmitted
4 received
0% packet loss
```

This confirms the server can successfully communicate with the gateway.

------------------------------------------------------------------------

## Step 5 -- Test Internet Connectivity

```bash
ping -c 4 8.8.8.8
```

Google's public DNS server (`8.8.8.8`) is commonly used to verify
Internet connectivity because it is highly available.

Successful replies confirm:

- Internet access is working
- Routing is functioning correctly

------------------------------------------------------------------------

## Step 6 -- Verify DNS Resolution

```bash
ping -c 4 google.com
```

or

```bash
getent hosts google.com
```

These commands verify that domain names can be translated into IP
addresses.

Successful output confirms that DNS resolution is functioning correctly.

------------------------------------------------------------------------

## Step 7 -- Review DNS Configuration

```bash
cat /etc/resolv.conf
```

This file contains the DNS servers configured for the system.

Verified:

- Configured nameserver
- DNS configuration

Example:

```text
nameserver 192.168.229.2
```

------------------------------------------------------------------------

## Step 8 -- Inspect Active Network Connections

```bash
ss -tuln
```

The `ss` utility displays network sockets currently in use.

Options used:

- `-t` → Display TCP sockets
- `-u` → Display UDP sockets
- `-l` → Show only listening services
- `-n` → Display numeric IP addresses and port numbers

This command helps verify which services are actively listening for
incoming network connections without performing DNS lookups.

------------------------------------------------------------------------

## Step 9 -- Verify Network Service

```bash
systemctl status NetworkManager
```

Verified that the NetworkManager service was running correctly and
managing the network interfaces.

If required:

```bash
sudo systemctl restart NetworkManager
```

This restarts the networking service after configuration changes.

------------------------------------------------------------------------

## Outcome

Successfully verified the Linux server's network configuration and
confirmed proper operation of network interfaces, IP addressing,
routing, DNS resolution, and Internet connectivity. The server was able
to communicate with both local and external networks without errors.

------------------------------------------------------------------------

## Network Overview

```text
                    Internet
                        │
                        │
                 Default Gateway
                 192.168.229.2
                        │
                        │
          -----------------------------
                        │
                  Ubuntu Server
                Hostname: prod-web-01
                        │
               Interface: ens33
                        │
            IP: 192.168.229.131/24
```

------------------------------------------------------------------------

## Network Information

| Item | Value |
|------|-------|
| Hostname | prod-web-01 |
| Network Interface | ens33 |
| Interface Status | UP |
| IPv4 Address | 192.168.229.131 |
| Network | 192.168.229.0/24 |
| Default Gateway | 192.168.229.2 |

------------------------------------------------------------------------

## Key Linux Concepts Demonstrated

- Network interfaces
- IPv4 addressing
- Routing tables
- Default gateway
- ICMP connectivity testing
- DNS resolution
- DNS configuration
- Network sockets
- NetworkManager
- TCP/IP networking

------------------------------------------------------------------------

## Linux Utilities Used

- ip
- ping
- getent
- cat
- ss
- systemctl

------------------------------------------------------------------------

## Skills Demonstrated

### Linux Administration

- Network configuration verification
- Routing verification
- DNS troubleshooting
- Interface management

### System Administration

- Network diagnostics
- Connectivity testing
- Service verification
- DNS validation

### Troubleshooting

- Interface verification
- Gateway connectivity testing
- Internet connectivity validation
- DNS troubleshooting
- Network socket inspection

------------------------------------------------------------------------

## Verification Checklist

- [x] Network interface verified
- [x] IP address confirmed
- [x] Default gateway identified
- [x] Routing table verified
- [x] Local network connectivity tested
- [x] Internet connectivity verified
- [x] DNS resolution verified
- [x] DNS configuration reviewed
- [x] Active network connections inspected
- [x] Network service verified