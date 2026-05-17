---
title: Storage Strategy
sidebar_label: Storage Strategy
hide_title: true
id: whitepaper_elf_13
---

# Storage Strategy

## Data Storage and Storage Strategy

Data storage is a collection of virtual volumes. In the ZBS model, data storage and storage strategy are coupled together, which means that the virtual volumes contained in a data storage have the same storage strategy.

## One-way Awareness Relationship Between ELF and Data Storage

ELF resources related to storage include the virtual volumes corresponding to virtual machines, virtual volume snapshots, virtual machine snapshots, and ISO images used. These resources all correspond to ZBS storage objects, but these storage objects are managed independently by ZBS and cannot be automatically recognized or directly used by ELF unless they are actively imported into ELF (in fact, recorded in ELF's MongDB). The relationship between the two is shown in the following figure:

![](../assets/elf-white-paper/image11.png)

## ELF Storage Strategy

In ELF, users only need to focus on compute workloads and do not need to care which ZBS data storage a storage resource belongs to. However, in ZBS, data storage and storage strategy are coupled, and storage strategy, as an attribute of data storage, adds unnecessary complexity for ELF users. To simplify user operations, ELF also introduces the concept of "storage strategy". ELF uses its own storage strategies to manage the creation of virtual volumes and determine the data storage they belong to.

Currently, ELF storage strategies only support iSCSI data storage by default, and can automatically create or delete data storage as needed, allowing users to focus more on the compute workload layer. Users can create different storage strategies in ELF according to their business needs.

### Storage Strategy Options

In addition to the name and description, ELF storage strategies support the following options, which include basic strategies and advanced strategies.

1. Basic strategy:
   - Number of replicas
   - Thin provisioning enabled

2. Advanced strategy:
   - Number of stripes
   - Stripe size

ELF provides a default storage strategy named "default" with the following settings:

- Number of replicas: 2

- Thin provisioning enabled: Yes

- Number of stripes: 8

- Stripe size: 256 KiB

### Automatic Management of Virtual Volumes

Automatic management of virtual volumes is a major component of the ELF storage strategy. When creating a virtual volume, users only need to care about the storage strategy corresponding to the virtual volume. ELF creates the virtual volume according to the specified storage strategy and automatically places it into a data storage that matches the strategy.

In ELF, one storage strategy corresponds to one or more iSCSI data storages. Since an iSCSI data storage can contain up to 256 LUNs, when creating a virtual volume, if the number of available iSCSI data storage LUNs under that strategy reaches the limit, ELF will automatically create a new iSCSI data storage for that storage strategy and place the virtual volume into the newly created iSCSI data storage. When a virtual volume is deleted, ELF will actively reclaim the LUN ID under its corresponding iSCSI data storage for use by subsequently created virtual volumes.
