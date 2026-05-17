---
title: NFS Data Storage
sidebar_label: NFS Data Storage
hide_title: true
id: whitepaper_elf_17
---

# NFS Data Storage

Similar to iSCSI, according to the NFS resource structure, ELF separately provides RESTful
APIs for Export, Inode, and snapshots. The functions supported by these RESTful APIs are as follows:

1. Export: create, delete, edit, query. It supports specifying a list of IP addresses allowed to access the Export, so that the client IP address is verified at the ZBS access layer. Requests from source IPs that do not match the whitelist rules will be rejected;

2. Inode: create, delete, edit, query, move, rename, clone, upload, rebuild from snapshot, and query read/write performance of files (NFS File). In addition, an API for batch querying Inode names is provided;

3. Snapshot: create, delete, edit, query, move, rollback.
