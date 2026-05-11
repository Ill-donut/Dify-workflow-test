# Release Notes Style Guide

**Document type:** `release_notes`
**Language pair:** Simplified Chinese → English
**Scope:** Translation style rules for product release notes, covering tense, voice, sentence structure, and section-specific conventions.

---

## Rule 1 — What's New and Improvements: Use Simple Present Tense

All entries in the **What's New** and **Improvements** sections must use simple present tense. Do not use past tense or future tense.

**Correct:**
- Supports enabling Boost mode in SMTX OS (ELF) active-active clusters.
- Displays the storage overprovisioning ratio.
- Provides port connectivity test with alerts for abnormal ports.

**Incorrect:**
- Added support for enabling Boost mode in SMTX OS (ELF) active-active clusters. *(past tense — wrong)*
- Will display the storage overprovisioning ratio. *(future tense — wrong)*

---

## Rule 2 — Document Title: Use "What's in this release"

The document title must be "What's in this release" (sentence case). Do not use "Release Update Notes" or other variations.

**Correct:**
- title: What's in this release
- # What's in this release

**Incorrect:**
- title: Release Update Notes
- # Release Update Notes

---

## Rule 3 — Author Field: Use Sentence Case

The author field must use sentence case: "SmartX documentation team". Do not capitalize "Documentation Team".

**Correct:**
- author: SmartX documentation team

**Incorrect:**
- author: SmartX Documentation Team

---

## Rule 4 — Sidebar Label: Use "What's in this release"

The sidebar label must be "What's in this release" (sentence case). Do not use "Release Update Notes".

**Correct:**
- sidebar_label: What's in this release

**Incorrect:**
- sidebar_label: Release Update Notes

---

## Rule 5 — Section Headings: Use Sentence Case

All section headings (## and ### levels) must use sentence case. Capitalize only the first word and proper nouns.

**Correct:**
- ## What's new
- ## Resolved issues
- ### Block storage
- ### Networking
- ### Operations and management

**Incorrect:**
- ## New
- ## Fixed Issues
- ### Block Storage
- ### Network
- ### Operations and Maintenance Management

---

## Rule 6 — Section Subheadings: Use Sentence Case

All subheadings within sections (### level) must use sentence case. Capitalize only the first word and proper nouns.

**Correct:**
- ### Block storage
- ### Networking
- ### Operations and management

**Incorrect:**
- ### Block Storage
- ### Network
- ### Operations and Maintenance Management

---

## Rule 7 — Product Name: Use "Netswift" Instead of "Wangxun"

When referring to NICs from Netswift (formerly Wangxun), use "Netswift". Do not use "Wangxun".

**Correct:**
- Supports Netswift 10GbE NICs of the txgbe series.
- Supports SR-IOV passthrough and PCI passthrough for Netswift NICs.

**Incorrect:**
- Supports Wangxun 10 GbE NICs (txgbe series).
- Supports SR-IOV passthrough and PCI passthrough for Wangxun NICs.

---

## Rule 8 — Resolved Issues: Use Descriptive Statement + Resolution Clause

All entries in the **Resolved issues** section must follow this structure:
1. A descriptive statement explaining the issue (what could happen, under what conditions)
2. A resolution clause: "The issue has been resolved in this release."

Do not start with "Fixed the issue where...".

**Correct:**
- The `elf-vm-monitor` service might fail to start due to an initialization error in host high availability configuration under rare circumstances. The issue has been resolved in this release.
- In clusters with Boost mode enabled, double-write issues might occur after a virtual machine was rebuilt via HA due to host failures. The issue has been resolved in this release.

**Incorrect:**
- Fixed the issue where, in very rare cases, abnormal initialization of host high availability configuration information might cause the `elf-vm-monitor` service to fail to start.
- Fixed the issue where, in clusters with Boost mode enabled, double writes might occur after a VM was rebuilt by HA due to a host exception.

---

## Rule 9 — Resolved Issues Section Heading: Use "Resolved issues"

The section heading for resolved issues must be "Resolved issues" (sentence case). Do not use "Fixed Issues".

**Correct:**
- ## Resolved issues

**Incorrect:**
- ## Fixed Issues

---

## Rule 10 — What's New Section Heading: Use "What's new"

The section heading for new features must be "What's new" (sentence case). Do not use "New".

**Correct:**
- ## What's new

**Incorrect:**
- ## New

---

## Rule 11 — Networking Section Heading: Use "Networking"

When referring to the networking section, use "Networking" as the heading. Do not use "Network".

**Correct:**
- ### Networking

**Incorrect:**
- ### Network

---

## Rule 12 — Operations and Management Section Heading: Use "Operations and management"

When referring to the operations and management section, use "Operations and management" (sentence case). Do not use "Operations and Maintenance Management".

**Correct:**
- ### Operations and management

**Incorrect:**
- ### Operations and Maintenance Management