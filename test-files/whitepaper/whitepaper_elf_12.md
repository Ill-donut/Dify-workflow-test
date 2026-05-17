---
title: Network management
sidebar_label: Network management
hide_title: true
id: whitepaper_elf_12
---

# Network management

## Virtual distributed switch

ELF virtual distributed switch (VDS) is an abstract virtual switch concept used to manage virtual switches across multiple hosts (implemented in ELF based on the open-source Open vSwitch). This allows unified configuration and management of virtual switches on multiple hosts, and ensures network consistency when virtual machines migrate between different hosts.

In practice, ELF virtual distributed switch can also be viewed as an extension of physical switches onto server hosts. As shown in the diagram below, ELF virtual distributed switch manages the physical NICs of hosts and the virtual ports of virtual machines. Each virtual port of a virtual machine corresponds to one virtual port on the virtual switch, and one or more physical NICs of the host serve as uplink ports (Uplink-Port) of the virtual switch.

![](../assets/elf-white-paper/elf-network-overview.png)

<!-- 这张图也被 Web 控制台手册的网络页面所使用 -->

A virtual switch can create multiple virtual ports (no more than 1,024 is recommended to ensure quality of service) for connecting to virtual machine virtual ports. It can bind one or more virtual ports simultaneously for communication between virtual machines and external networks. One physical NIC of a host can belong to only one virtual switch, but a virtual switch can bind multiple physical ports, in which case those physical ports are in a bonding relationship. ELF VDS is based on OVS (Open vSwitch), so ELF virtual distributed switch uses OVS Bond as the default bonding type. If the storage network has RDMA enabled, the virtual distributed switch associated with the storage network uses OVS Bond as the bonding type.

- **OVS Bond** supports: active-backup, balance-slb (traffic balanced by source MAC + VLAN tag), balance-tcp (traffic balanced by L2/L3/L4 headers; requires 802.3ad LACP on physical switch).
- **Linux Bond** supports: active-backup, balance-xor (forwards via different ports based on source/destination MAC hash; requires static EtherChannel on physical switch, otherwise MAC address flapping may occur), 802.3ad (traffic balanced by L2/L3/L4 headers; requires LACP).

## Virtual network

Based on the connectivity defined jointly by the virtual distributed switch and VLAN ID, ELF abstracts the concept of a "virtual network." To meet the different needs of management, storage, and virtual machines, ELF defines three types of virtual networks:

1. Management network: There is exactly one. Primarily used for web and SSH connectivity, with no special performance requirements; 100 Mbps is sufficient. Physically, it may share the same network as the service network, but more often it is kept separate.
2. Storage network: There is exactly one. Also referred to as the data network in ZBS. Dedicated to storage, it is physically isolated; it cannot communicate with external networks or access other networks, and requires bonding. Because it is physically isolated, VLAN is generally not required.
3. VM network: The network where virtual machines run. Multiple VM networks may exist depending on business requirements. A virtual machine can connect to different VM networks through multiple different virtual ports, with support for VLAN and bonding. When a virtual machine migrates between hosts using the same storage, the VM network ensures network continuity during migration without requiring reconfiguration of the network database.

Technically, these three network types are identical; they differ only in their logical roles. Creating virtual machines is not supported on management networks or storage networks.

## Managing virtual distributed switches

Network management supports creating, editing, and deleting virtual distributed switches. However, the VDS to which the management network and storage network belong are subject to the following rules:

1. Due to the importance of the storage network, the VDS to which it belongs is read-only; editing and deleting are not supported. However, creating VM networks under this VDS is not restricted (though not recommended).
2. The VDS to which the management network belongs can be edited but not deleted.

## Managing virtual networks

VM networks can be created under any VDS, and support editing and deletion. A VM network can be deleted only if it is not in use by any virtual machine, VM template, or VM snapshot; otherwise, deletion cannot be performed. Editable fields for VM networks include: network name, VLAN ID, and QoS policy.

The management network, due to its management role, supports only editing. Unlike VM networks, its editable fields include: VLAN ID, gateway, subnet mask, the management IP of each host, MTU, and QoS policy.

The storage network supports editing only the MTU and QoS policy.
