---
title: NFS datastore
sidebar_label: NFS datastore
hide_title: true
id: whitepaper_elf_17
---

# NFS datastore

Similar to iSCSI, ELF provides RESTful APIs for exports, Inodes, and snapshots according to the NFS resource structure. The features supported by these RESTful APIs are as follows:

1. Export: Create, delete, edit, query. Supports specifying an IP address allowlist for accessing the export. The ZBS access layer validates the client's IP address, and requests from source IPs that do not match the allowlist rules are rejected.

2. Inode: Create, delete, edit, query, move, rename, clone, upload, rebuild from snapshot, and query file (NFS file) read/write performance. An additional API is provided for batch querying Inode names.

3. Snapshot: Create, delete, edit, query, move, roll back.
