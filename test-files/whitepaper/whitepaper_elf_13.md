---
title: Storage policies
sidebar_label: Storage policies
hide_title: true
id: whitepaper_elf_13
---

# Storage policies

## Datastores and storage policies

A datastore is a collection of virtual volumes. In ZBS, datastores and storage policies are coupled; all virtual volumes in a datastore share the same storage policy.

## ELF's one-way awareness relationship with datastores

Storage-related resources in ELF include virtual volumes associated with virtual machines, virtual volume snapshots, VM snapshots, and ISO images. All of these resources correspond to storage objects in ZBS. However, these storage objects are managed independently by ZBS and cannot be automatically detected or directly used by ELF unless they are actively imported into ELF (which effectively means they are recorded in ELF's MongoDB). The relationship is illustrated in the diagram below:

![](../assets/elf-white-paper/image11.png)

## ELF storage policies

In ELF, you only need to focus on compute workloads, without worrying about which ZBS datastore a storage resource belongs to. However, in ZBS, datastores and storage policies are coupled, and exposing storage policy as a datastore attribute would introduce unnecessary complexity for ELF users. To simplify operations, ELF introduces its own concept of "storage policies." ELF manages virtual volume creation through storage policies at its own layer, which determines the datastore a virtual volume is placed in.

Currently, ELF storage policies support only iSCSI datastores by default. Datastores can be automatically created or deleted as needed, allowing you to focus on the compute layer. You can create different storage policies in ELF based on your business requirements.

### Storage policy options

In addition to name and description, ELF storage policies support the following options, divided into basic policies and advanced policies.

1. Basic policies: number of replicas, thin provisioning.
2. Advanced policies: number of stripes, stripe size.

ELF provides a default storage policy named "default" with the following settings: number of replicas: 2, thin provisioning: Yes, number of stripes: 8, stripe size: 256 KiB.

### Automatic virtual volume management

Automatic virtual volume management is a key component of ELF storage policies. When creating a virtual volume, you only need to specify the storage policy. ELF creates the virtual volume according to the specified storage policy and automatically places it in a datastore that matches the policy.

In ELF, each storage policy has one or more corresponding iSCSI datastores. Because a single iSCSI datastore can hold a maximum of 256 LUNs, when the LUN limit is reached for all available iSCSI datastores under a given policy, ELF automatically creates a new iSCSI datastore for that storage policy and places the new virtual volume in it. When a virtual volume is deleted, ELF actively reclaims the LUN ID under its corresponding iSCSI datastore, making it available for future virtual volume creation.
