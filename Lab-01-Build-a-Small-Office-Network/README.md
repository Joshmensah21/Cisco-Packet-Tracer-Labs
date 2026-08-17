# Lab 01 – Build a Small Office Network

![Category](https://img.shields.io/badge/Category-Networking%20%2F%20LAN%20Configuration-blue)
![Date](https://img.shields.io/badge/Date%20Completed-19%2F07%2F2026-brightgreen)
![Tool](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-orange)

## 🎯 Objective
The aim of this project was to build a Local Area Network (LAN) similar to one found in a typical office environment. The learning outcome of this lab was to understand the core components required to connect multiple devices within a small network, as well as the fundamental configuration needed to enable reliable network communication.

## 📐 Network Design
A small office topology was designed consisting of a router, a switch, and 3 host PCs interconnected using Copper Straight-Through cables.

### Hardware & Topology
* **Devices Used:**
  * 1x Cisco Router
  * 1x Cisco Switch
  * 3x Host PCs
* **Topology:** 
  * Host PCs are connected directly to switch access ports.
  * The switch is uplinked to the router's `GigabitEthernet 0/0` interface.
* **Cabling:** 
  * Copper Straight-Through cables across all connections.

## ⚙️ Configuration

### 1. Static IP Addressing Scheme
Each device on the network was manually assigned a static IPv4 address within the `192.168.1.0/24` subnet.

| Device Name | IP Address | Subnet Mask | Default Gateway | Connection Port |
| :--- | :--- | :--- | :--- | :--- |
| **Router** | `192.168.1.1` | `255.255.255.0` | N/A | `Gi0/0` |
| **PC-0** | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` | Switch Port |
| **PC-1** | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` | Switch Port |
| **PC-2** | `192.168.1.12` | `255.255.255.0` | `192.168.1.1` | Switch Port |

### 2. Router Interface Activation
The router interface was brought online via the Command Line Interface (CLI):

```text
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```

## 🔍 Verification & Troubleshooting

### Troubleshooting Interface Issues
Initial status checks using `show ip interface brief` reported that `GigabitEthernet0/0` was `down / down`.

* **Root Cause:** Incorrect cabling/port assignment between the switch and the router.
* **Resolution:** Re-verified cable connections, ensuring proper port alignment between switch and router interfaces.
* **Verification:** Re-running the command confirmed the interface status changed to `up / up`.

```text
Router# show ip interface brief
Interface              IP-Address      OK? Method Status                  Protocol
GigabitEthernet0/0     192.168.1.1     YES manual up                      up
```

### End-to-End Connectivity Testing
Ping tests were executed from the PC command prompt terminals to verify network reachability:
* **PC-0 -> Default Gateway (`192.168.1.1`):** Successful
* **PC-0 -> PC-1 (`192.168.1.11`):** Successful

## 💡 Key Concepts Learned
* **IP Addressing & Subnetting:** Understanding how host IP addresses and subnet masks (`255.255.255.0`) define local network boundaries and default gateway routing logic.
* **Switching vs. Routing:** Differentiating layer 2 traffic forwarding across switch ports from layer 3 boundary handling at the router interface.
* **Static Configuration:** Understanding manual host configuration vs. dynamic assignment (DHCP).
* **CLI Interface Management:** Practicing essential Cisco IOS commands (`no shutdown`, `show ip interface brief`).
* **Physical Layer Troubleshooting:** Diagnosing `down / down` interface states by isolating cable types and interface port selections.

## 📸 Screenshots

### Figure 1 – Network Topology
![Network Topology](screenshots/01_network_topology.png)
*The completed network showing the router, switch, 3 PCs, and physical cabling connections.*

### Figure 2 – Router Interface Verification
![Router Verification](screenshots/02_router_interface_verification.png)
*Output of `show ip interface brief` confirming interface status and protocol are `up/up`.*

### Figure 3 – Connectivity Tests
![Connectivity Tests](screenshots/03_ping_connectivity_tests.png)
*Successful ICMP ping results between host PCs and the default gateway router.*

## 📝 Reflection
This lab helped me understand how key network components—switches, routers, IP addresses, and subnet masks—interoperate to facilitate communications within a small network. Gaining hands-on experience troubleshooting the `down/down` interface issue reinforced the importance of layer 1/layer 2 verification in real-world networking tasks.
