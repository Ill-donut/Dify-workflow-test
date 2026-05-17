---
title: Network Management
sidebar_label: Network Management
hide_title: true
id: whitepaper_elf_12
---

# Network Management

## Virtual Distributed Switch

The ELF Virtual Distributed Switch (Virtual Distributed Switch - VDS) is an abstract virtual switch concept used to manage virtual switches on multiple hosts (in ELF, implemented based on the open source Open vSwitch). This enables unified configuration and management of virtual switches on multiple hosts on one hand, and ensures network consistency when virtual machines migrate between different hosts on the other.

In practice, the ELF Virtual Distributed Switch can also be regarded as an extension of the physical switch on the server host. As shown in the figure below, the ELF Virtual Distributed Switch manages the host physical network ports and the virtual network ports of virtual machines. One virtual network port of a virtual machine corresponds to one virtual port of the virtual switch, and one or more physical network ports of the host serve as uplink ports (Uplink-Port) of the virtual switch.

![](../assets/elf-white-paper/elf-network-overview.png)

<!-- This figure is also used on the network page in the Web console manual -->

The virtual switch can create multiple virtual ports (it is recommended not to exceed 1024 to ensure service quality), which are used to connect the virtual network ports of virtual machines. One or more virtual network ports can be bound at the same time to enable communication between virtual machines and external networks. One physical network port of a host can belong to only one virtual switch, but a virtual switch can bind multiple physical ports. In this case, the physical ports are bound to each other. The ELF Virtual Distributed Switch is implemented based on OVS (Open vSwitch), so by default the ELF Virtual Distributed Switch uses the OVS Bond binding type. If the storage network has RDMA enabled, the virtual distributed switch associated with the storage network uses the OVS Bond binding type.

- **OVS Bond**

  OVS Bond supports the following bonding modes:

  - active-backup: active/standby mode.
  - balance-slb: balances traffic based on the packet Source MAC + VLAN Tag.
  - balance-tcp: balances traffic based on the packet L2, L3, and L4 headers. This mode requires 802.3ad (LACP) to be configured on the physical switch.

- **Linux Bond**
  
  Linux Bond supports the following bonding modes:

  - active-backup: active/standby mode.
  - balance-xor: forwards packets through different physical ports according to a hash value calculated from the source MAC address and destination MAC address of the packet. This mode requires the physical switch to be configured with static EtherChannel; otherwise, MAC address flapping may occur.
  - 802.3ad: balances traffic based on the packet L2, L3, and L4 headers. This mode requires 802.3ad (LACP) to be configured on the physical switch.

## Virtual Networks

Based on the connectivity jointly defined by the virtual distributed switch and the VLAN ID, ELF abstracts the concept of "virtual network". For the different requirements of management, storage, and virtual machines, ELF defines three types of virtual networks:

1. Management network: There is exactly one. It is mainly used for Web and SSH connections, and has no special performance requirements; 100 Mbps is sufficient. Physically, it may be mixed with the business network, but more often it is separated from the business network.

2. Storage network: There is exactly one. In ZBS, it is also called the data network. It is dedicated to storage support, is physically isolated, cannot communicate with external networks, cannot access other networks, and has bonding requirements. Because it is physically isolated, VLAN is generally not needed.

3. Virtual machine network: The network on which virtual machines run. There may be multiple virtual machine networks according to business requirements. A virtual machine can connect to different virtual machine networks through multiple different virtual network ports, and there are VLAN and bonding requirements. When a virtual machine migrates between different hosts using the same storage, the virtual machine network ensures that the network is not interrupted during migration, and the network database does not need to be reconfigured.

Technically speaking, these three networks are the same, but they differ in logical roles. The management network and storage network do not support users creating virtual machines on them.

## Manage Virtual Distributed Switches

Network management supports creating, editing, and deleting virtual distributed switches, but the distributed virtual switches that belong to the management network and storage network are subject to the following rules:

1. Because of the importance of the storage network, the virtual distributed switch to which it belongs is read-only, meaning editing or deleting is not supported, but creating virtual machine networks under this virtual distributed switch is not restricted (not recommended).

2. The virtual distributed switch to which the management network belongs can be edited but cannot be deleted.

## Manage Virtual Networks

Virtual machine networks can be created under any virtual distributed switch, and editing and deletion are supported. The prerequisite for deleting a virtual machine network is that the network is not being used by virtual machines, virtual machine templates, or virtual machine snapshots; otherwise, the deletion operation cannot be performed. Editable items for a virtual machine network include: network name, VLAN ID, and QoS policy.

Because of its management properties, the management network only supports editing operations and differs slightly from virtual machine networks. Its editable items include: VLAN ID, gateway, subnet mask, management IP of each host, MTU, and QoS policy.

The storage network only supports editing MTU and QoS policy.
