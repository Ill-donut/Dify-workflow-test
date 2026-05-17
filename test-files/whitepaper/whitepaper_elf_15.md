---
title: Datastores
sidebar_label: Datastores
hide_title: true
id: whitepaper_elf_15
---

# Datastore

A datastore is the basic unit of data protection and storage policies. Each datastore contains a set of objects sharing the same data protection policy. Datastores provide services through standard protocols; ZBS currently supports iSCSI and NFS storage communication protocols, and ELF provides corresponding RESTful API support for both. As mentioned in the SMTX OS virtual machine service storage policies section, ZBS storage objects in ELF are not automatically detected by the SMTX OS virtual machine service. In most cases, you can independently manage cluster datastores through the RESTful APIs provided by ELF without directly accessing ZBS's programmable interface.
