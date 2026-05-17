---
title: Data Storage
sidebar_label: Data Storage
hide_title: true
id: whitepaper_elf_15
---

# Data Storage

Data storage is a basic unit of data protection and storage policies. Each data storage contains a set of objects with the same data protection policy. Data storage provides services through standard protocols. Currently, ZBS supports
iSCSI and NFS storage communication protocols, and ELF provides corresponding RESTful API support for these two protocols. In the SMTX OS
virtual machine service storage policy section, it has already been mentioned that ZBS storage objects in ELF are not automatically recognized by the SMTX OS
virtual machine service. In most cases, users can independently manage cluster data storage through the RESTful API provided by ELF without directly accessing the programmable interface of ZBS.
