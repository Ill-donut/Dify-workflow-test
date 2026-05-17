---
title: iSCSI Data Storage
sidebar_label: iSCSI Data Storage
hide_title: true
id: whitepaper_elf_16
---

# iSCSI Data Storage

For the iSCSI protocol, according to the storage resource structure, ELF provides RESTful APIs for Target, LUN, and snapshot respectively. The functions supported by these RESTful APIs are as follows:

1. Target: create, delete, edit, query. It supports validating the client's IP address at the ZBS access layer by specifying a list of IP addresses allowed to access the Target. Requests from source IPs that do not match the rules in the whitelist will be rejected;

2. LUN: create, delete, edit, query, move, clone, upload, rebuild from snapshot, and query LUN read/write performance;

3. Snapshot: create, delete, edit, query, move, rollback.
