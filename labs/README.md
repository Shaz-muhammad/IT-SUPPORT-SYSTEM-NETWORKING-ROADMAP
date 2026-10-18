Networking Labs

This folder contains my Cisco Packet Tracer networking labs, configuration notes, and practical learning exercises.

Labs

- Basic LAN Configuration
- VLAN Configuration
- Router Interface Configuration
- Static Routing
- Dynamic Routing — RIP
- Dynamic Routing — EIGRP
- IPv4 Subnetting — FLSM and VLSM


Networking Commands Reference

A collection of Cisco IOS commands used while practising network configuration, routing, subnetting, VLANs, and troubleshooting in Cisco Packet Tracer.

1. Basic Router Configuration

enable
configure terminal
hostname R1
no ip domain-lookup
enable secret class
service password-encryption
banner motd #Authorized Access Only#

2. Basic Switch Configuration

enable
configure terminal
hostname SW1
no ip domain-lookup
enable secret class

3. Fast Ethernet Interface Configuration

Configure router interfaces and assign IPv4 addresses.

enable
configure terminal

interface fastEthernet 0/0
ip address <IP-address> <subnet-mask>
no shutdown
exit

interface fastEthernet 0/1
ip address <IP-address> <subnet-mask>
no shutdown
exit

Example:

interface fastEthernet 0/0
ip address 21.0.0.1 255.0.0.0
no shutdown

4. Serial Interface Configuration

Use these commands only when your topology has serial links and your router has the required serial interfaces.

interface serial 0/0
ip address <IP-address> <subnet-mask>
no shutdown
exit

Configure a clock rate on the DCE end only:

interface serial 0/0
clock rate 64000
no shutdown

Check the serial controller, if supported:

show controllers serial 0/0

Note: Serial interface names depend on the installed module and router model.

5. Static Routing

Configure a route to a remote network.

Syntax:

ip route <destination-network> <subnet-mask> <next-hop-IP>

Example:

ip route 22.0.0.0 255.0.0.0 10.0.0.2

Configure a default route:

ip route 0.0.0.0 0.0.0.0 <next-hop-IP>

Configure a route using an exit interface:

ip route <destination-network> <subnet-mask> <exit-interface>

Remove a static route:

no ip route <destination-network> <subnet-mask> <next-hop-IP>

Verify routes:

show ip route
show running-config

6. RIP Dynamic Routing

Configure RIP version 2 on each participating router.

enable
configure terminal
router rip
version 2
no auto-summary
network <network-address>
exit

Example:

router rip
version 2
no auto-summary
network 10.0.0.0
network 21.0.0.0
exit

Verify RIP:

show ip route
show ip protocols
show running-config

Note: Add the appropriate "network" statements for the directly connected networks that should participate in RIP.

7. EIGRP Dynamic Routing

Configure EIGRP with autonomous system number 100.

enable
configure terminal
router eigrp 100
no auto-summary
network <network-address> <wildcard-mask>
exit

Example:

router eigrp 100
no auto-summary
network 11.0.0.0 0.255.255.255
network 23.0.0.0 0.255.255.255
exit

Verify EIGRP:

show ip route
show ip protocols
show ip eigrp neighbors
show ip eigrp topology

Note: The EIGRP autonomous system number and wildcard masks must match the topology. Configure the appropriate network statements on every participating router.

8. VLAN Configuration

Create a VLAN on a switch.

enable
configure terminal
vlan 10
name SALES
exit

vlan 20
name HR
exit

Assign a switch port to VLAN 10:

interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
no shutdown
exit

Assign another port to VLAN 20:

interface fastEthernet 0/2
switchport mode access
switchport access vlan 20
no shutdown
exit

Verify VLAN configuration:

show vlan brief
show interfaces status
show running-config

Optional: VLAN Trunk Configuration

Use this when your topology requires a trunk link between switches or between a switch and a router.

interface fastEthernet 0/24
switchport mode trunk
no shutdown
exit

Verify trunk links:

show interfaces trunk

Note: Trunk commands and supported options depend on the switch model.

9. IPv4 Addressing and Subnetting (FLSM/VLSM)

Practise calculating:

- Network address
- Subnet mask and CIDR prefix
- Number of required hosts
- Usable host range
- Broadcast address
- Point-to-point subnet allocation

Common subnet masks:

CIDR| Subnet Mask| Usable Hosts
/8| 255.0.0.0| 16,777,214
/16| 255.255.0.0| 65,534
/24| 255.255.255.0| 254
/25| 255.255.255.128| 126
/26| 255.255.255.192| 62
/27| 255.255.255.224| 30
/28| 255.255.255.240| 14
/29| 255.255.255.248| 6
/30| 255.255.255.252| 2

Assign the correct IP address and subnet mask to each router interface and PC according to the subnetting plan.

10. PC Network Configuration

In Packet Tracer, select the PC and open Desktop → IP Configuration.

Enter:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server, if required

The default gateway should normally be the IP address of the router interface serving that LAN.

11. Interface Verification

Check interface status and IP addresses:

show ip interface brief
show interfaces
show running-config

Enable an interface that is administratively shut down:

configure terminal
interface fastEthernet 0/0
no shutdown

Disable an interface when needed:

interface fastEthernet 0/0
shutdown

12. Connectivity Testing

Test connectivity to another device:

ping <destination-IP>

Trace the path to a destination from a router:

traceroute <destination-IP>

On a Windows PC in Packet Tracer, use:

ping <destination-IP>
tracert <destination-IP>
ipconfig

13. Configuration and Routing Verification

show running-config
show startup-config
show ip interface brief
show ip route
show ip protocols
show interfaces
show vlan brief

These commands help verify interface status, saved configuration, routing tables, routing protocols, and VLAN assignments.

14. Save the Router or Switch Configuration

Save the running configuration to startup configuration:

copy running-config startup-config

Alternatively:

write memory

15. Common Troubleshooting Checklist

- Check that cables are connected to the correct ports.
- Confirm that interface IP addresses and subnet masks are correct.
- Use "no shutdown" on interfaces that should be active.
- Verify that PCs have the correct default gateway.
- Check the routing table using "show ip route".
- Confirm that RIP or EIGRP has the correct network statements.
- Verify VLAN membership using "show vlan brief".
- Check trunk configuration when VLANs must cross a trunk link.
- Use "ping" to identify where connectivity fails.
- Save the configuration after successful changes.

Learning Outcomes

Through these Packet Tracer exercises, I have practised:

- Basic LAN connectivity
- Router and switch configuration
- IPv4 addressing and subnetting
- Static routing
- RIP and EIGRP dynamic routing
- VLAN creation and port assignment
- Multiple-LAN connectivity
- Network verification and troubleshooting

Note: Commands are provided as a learning reference. Interface names, routing statements, addresses, and optional features must be adjusted to match each topology and the capabilities of the selected Cisco device.

