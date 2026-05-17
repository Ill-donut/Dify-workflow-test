---
title: iSCSI datastore
sidebar_label: iSCSI datastore
hide_title: true
id: whitepaper_elf_16
---

# iSCSI datastore

For the iSCSI protocol, ELF provides RESTful APIs for targets, LUNs, and snapshots according to the storage resource structure. The features supported by these RESTful APIs are as follows:

1. Target: Create, delete, edit, query. Supports specifying an IP address allowlist for accessing the target. The ZBS access layer validates the client's IP address, and requests from source IPs that do not match the allowlist rules are rejected.

2. LUN: Create, delete, edit, query, move, clone, upload, rebuild from snapshot, and query LUN read/write performance.

3. Snapshot: Create, delete, edit, query, move, roll back.
