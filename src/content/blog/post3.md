---
title: "DHCP Overview"
description: "Introduction to DHCP"
pubDate: "Sep 12 2022"
heroImage: "/dhcp.webp"
badge: "Demo badge"
tags: ["DHCP","Networking"]
---

In the earlier days, IP assignment to the devices within a network was static. Means we would have to go into a device and manually assign an IP address to it. All we would have to do this to all the devices in the network. Clearly this method has the following disadvantages:

1. Imagine there are 200 devices in the network. Now when we manually assign IPs to the devices, it is a clear waste of time.
2. We would also have to keep track of the IPs that are assigned in order to avoid IP conflict in the future.

Note: IP conflict is when two or more devices have the same IP address within a network.

In order to have a better way to assign IPs to the devices, DHCP was introduced. DHCP or Dynamic Host Configuration Protocol is a service that assigns devices an IP address in a network without any manual intervention. This way of assigning IPs is known as dynamic assignment. Along with IP address, DHCP also offers things like the subnet mask, defualt gateway and DNS server's IP, lease time etc.

### Steps involved in DHCP

#### 1. DHCP Discover

- When a device (client) first connects to the network and needs an IP address, it broadcasts a DHCPDISCOVER message to all devices on the network.
- This message is sent to the network's broadcast address (subnet mask - `255.255.255.255`) because the client doesn't have an IP address yet and doesn't know the IP address of the DHCP server.
- The destination IP address in this packet will be the broadcast address of the network. This message will be a broadcast message, so the message will be delivered to all the devices in the network. 
- DHCP server will be one of the devices in the network. Upon receiving this message, it will do the next step. All other devices will simply drop this broadcast message.

#### 2. DHCP Offer

- When a DHCP server receives the DHCPDISCOVER message, it responds with a DHCPOFFER message.
- This message contains an available IP address, subnet mask, default gateway, lease duration, and other configuration details.
- The DHCPOFFER is sent as a unicast message to the MAC address of the requesting device or as a broadcast if the client hasn't yet obtained an IP.

#### 3. DHCP Request

- After receiving one or more offers from DHCP servers, the client selects one offer (usually the first one received) and broadcasts a DHCPREQUEST message to indicate its acceptance of the chosen IP address and configuration parameters.
- This broadcast request also serves as a notification to other DHCP servers that their offers were not selected, so they can keep those IP addresses available in their pools.

#### 4. DHCP Acknowledgement

- The selected DHCP server responds with a DHCPACK message to confirm the IP address lease and provide any additional configuration details.
- At this point, the client configures its network interface with the assigned IP address and other settings, allowing it to communicate on the network.
- If the server cannot assign the IP (e.g., if it's no longer available), it might respond with a DHCPNAK (Negative Acknowledgment), and the process restarts.
