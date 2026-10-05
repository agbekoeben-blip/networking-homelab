# Project 1: Small Business Network

## Project Overview

This project involves designing and configuring a basic network for a fictional small business called BrightTech Solutions.

The company has two departments:

- Administration: 5 computers
- Sales: 8 computers

The goal is to build a network that allows the computers to communicate while developing practical skills in network design, IP addressing, device configuration, connectivity testing, and troubleshooting.

## Learning Objectives

Through this project, I will practice:

- Identifying the roles of common networking devices
- Designing a basic network topology
- Configuring IPv4 addresses
- Understanding subnet masks and default gateways
- Configuring basic router and switch connectivity
- Testing connectivity using tools such as ping
- Troubleshooting common network connectivity problems
- Documenting network configurations and troubleshooting steps

## Tools

- Cisco Packet Tracer
- GitHub
- Windows Command Line

## Network Requirements

BrightTech Solutions currently has two departments:

| Department | Number of Computers |
|---|---:|
| Administration | 5 |
| Sales | 8 |

Further network requirements and configurations will be added as the project progresses.

## Network Topology

## Network Topology

The initial BrightTech Solutions network consists of one Cisco 1941 router,
one Cisco 2960 switch, five Administration PCs, and eight Sales PCs.

![BrightTech Initial Network Topology](screenshots/initial-working-topology.png)

## IP Addressing

The network uses the private IPv4 network `192.168.10.0/24`.

- Subnet Mask: `255.255.255.0`
- Network Address: `192.168.10.0`
- Broadcast Address: `192.168.10.255`
- Usable Host Range: `192.168.10.1 - 192.168.10.254`
- Default Gateway: `192.168.10.1`

### IP Addressing Table

| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| Router | 192.168.10.1 | 255.255.255.0 | N/A |
| Admin-PC1 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| Admin-PC2 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| Admin-PC3 | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| Admin-PC4 | 192.168.10.13 | 255.255.255.0 | 192.168.10.1 |
| Admin-PC5 | 192.168.10.14 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC1 | 192.168.10.20 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC2 | 192.168.10.21 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC3 | 192.168.10.22 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC4 | 192.168.10.23 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC5 | 192.168.10.24 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC6 | 192.168.10.25 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC7 | 192.168.10.26 | 255.255.255.0 | 192.168.10.1 |
| Sales-PC8 | 192.168.10.27 | 255.255.255.0 | 192.168.10.1 |

## DHCP Configuration

After verifying the network using static IPv4 addressing, the network was upgraded to use DHCP for automatic client configuration.

Router0 was configured as the DHCP server for the `192.168.10.0/24` network.

The addresses from `192.168.10.1` through `192.168.10.49` were reserved for network infrastructure and other devices that may require static addressing.

DHCP clients receive addresses beginning at `192.168.10.50`.

### DHCP Configuration

The following Cisco IOS configuration was used:

    ip dhcp excluded-address 192.168.10.1 192.168.10.49

    ip dhcp pool BRIGHTTECH
     network 192.168.10.0 255.255.255.0
     default-router 192.168.10.1

After changing the PCs from static addressing to DHCP, all 13 computers successfully received IPv4 configurations automatically.

The DHCP leases were verified using:

    show ip dhcp binding

The router assigned addresses from `192.168.10.50` through `192.168.10.62` to the 13 client computers.

![DHCP Bindings](screenshots/dhcp-bindings.png)

## Configuration

Configuration steps will be documented as devices are configured.

## Testing and Troubleshooting

After configuring the router and assigning static IPv4 addresses to the PCs, connectivity was verified using ICMP ping tests.

The following tests were successfully completed:

- Admin-PC3 to the default gateway (`192.168.10.1`)
- Admin-PC5 to Sales-PC1 (`192.168.10.20`)
- Sales-PC8 to Admin-PC1 (`192.168.10.10`)

All tests returned four successful replies with 0% packet loss.

These tests confirmed that devices within the `192.168.10.0/24` network could communicate successfully through the switch and that the PCs could reach the router's LAN interface.

## Switch Management

After configuring DHCP, the Cisco 2960 switch was configured with a management IP address.

The switch was assigned:

- Hostname: `SW1`
- Management Interface: `VLAN 1`
- Management IP Address: `192.168.10.2`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.10.1`

The following Cisco IOS configuration was used:

    hostname SW1

    interface vlan 1
     ip address 192.168.10.2 255.255.255.0
     no shutdown

    ip default-gateway 192.168.10.1

The management interface was verified using:

    show ip interface brief

The output confirmed that VLAN 1 was `up/up` with the IP address `192.168.10.2`.

Connectivity to the switch management interface was successfully tested from an end device using:

    ping 192.168.10.2

The switch does not require an IP address to perform normal Layer 2 frame forwarding. The management IP address allows administrators to communicate with and manage the switch over the IP network.

## What I Learned

During the initial network configuration, I learned how to:

- Design a basic LAN using a router, switch, and end devices.
- Connect different Ethernet devices using straight-through cables.
- Configure a router interface with an IPv4 address.
- Enable a Cisco router interface using the `no shutdown` command.
- Verify router interfaces using `show ip interface brief`.
- Assign static IPv4 addresses, subnet masks, and default gateways to end devices.
- Test connectivity using the `ping` command.
- Understand that devices on the same subnet communicate through the switch without requiring the router.
- Understand that a default gateway is used when a host needs to communicate with another network.
- Understand the purpose of DHCP in reducing manual IP configuration.
- Configure a Cisco router to provide DHCP services.
- Create a DHCP address pool.
- Exclude addresses from a DHCP pool for infrastructure devices.
- Configure DHCP clients.
- Verify DHCP leases using `show ip dhcp binding`.
- Understand the DHCP DORA process: Discover, Offer, Request, and Acknowledge.
- - Understand why a Layer 2 switch can forward traffic without an IP address.
- Understand the difference between switching traffic and management traffic.
- Configure a hostname on a Cisco switch.
- Configure a Switch Virtual Interface (SVI).
- Assign a management IPv4 address to a Layer 2 switch.
- Configure a switch default gateway.
- Verify switch interfaces using `show ip interface brief`.
- Test connectivity to a switch management interface using ping.
