---
title: Version Supporting Information
author: SmartX Documentation Team
hide_title: true
id: release_notes_03
sidebar_label: Version Supporting Information
---


# Version Supporting Information

## Supporting Information for Virtualization Platforms and Server Types

<table>
  <thead>
    <tr>
        <th><strong>Virtualization Platform</strong></th>
        <th><strong>Server CPU Type</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td rowspan="5">ELF</td>
        <td>Intel x86_64 chip</td>
    </tr>
    <tr>
        <td>AMD x86_64 chip</td>
    </tr>
    <tr>
        <td>Hygon x86_64 chip</td>
    </tr>
    <tr>
       <td>Kunpeng AArch64 chip</td>
    </tr>
    <tr>
       <td>Phytium AArch64 chip</td>
    </tr>
    <tr>
        <td rowspan="2">VMware ESXi</td>
        <td>Intel x86_64 chip</td>
    </tr>
    <tr>
        <td>AMD x86_64 chip</td>
    </tr>
  </tbody>
</table>

## Supporting Information for SMTX OS and CloudTower Versions

The management service of SMTX OS is provided by CloudTower. This version of SMTX OS cluster supports management only by CloudTower 4.5.0 or later.

## Supporting Information for SMTX OS and Other Product Versions

SMTX OS can be used together with other SmartX products, but only some versions of each product support use with the current version of SMTX OS. See the release notes of the corresponding product for the version support relationship between the two products.

- Everoute
- SMTX Kubernetes service
- SMTX File Storage
- SMTX Backup and Disaster Recovery
- Observability Platform
- Inspection Center
- Upgrade Center


## Supporting Information for Virtualization Platforms and Application Scenarios

### Virtualization Platform

<table>
<thead>
  <tr>
    <th><strong>Platform Type</strong></th>
    <th><strong>Specific Version</strong></th>
    <th><strong>Deployment Method</strong></th>
    <th><strong>Storage Protocol</strong></th>
    <th><strong>Remarks</strong></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>ELF</td>
    <td>-</td>
    <td>Host deployment</td>
    <td>iSCSI</td>
    <td>
       <p>For the Guest OS supported by it, see <em>SMTX OS Virtual Machine Service Compatibility Guide</em> released with the version.</p>
       <p>Use SMTX VMTools <code>3.2.2</code>.</p></td>
  </tr>
  <tr>
    <td rowspan="2">VMware ESXi</td>
    <td><ul>
      <li><p>ESXi 7.0b</p></li>
      <li><p>ESXi 7.0 U1</p></li>
    </ul></td>
    <td>SCVM deployment</td>
    <td>NFS</td>
    <td>No VAAI-NAS plugin needs to be installed.</td>
  </tr>
  <tr>
    <td><ul>
      <li><p>ESXi 7.0 U2</p></li>
      <li><p>ESXi 7.0 U3f</p></li>
      <li><p>ESXi 7.0 U3g</p></li>
      <li><p>ESXi 8.0 U1a</p></li>
      <li><p>ESXi 8.0 U2</p></li>
      <li><p>ESXi 8.0 U3</p></li>
    </ul></td>
    <td>SCVM deployment</td>
    <td>NFS</td>
    <td>Use VAAI-NAS plugin <code>2.1-4</code>.</td>
  </tr>
</tbody>
</table>


### VDI Scenario

In VDI scenarios, SMTX OS can be used with Horizon View and XenDesktop. The supported versions are as follows. In this case, SMTX OS can run only in the SCVM of an ESXi 7.0b host, and VAAI is not supported when a desktop pool is created.

<table>
<thead>
  <tr>
    <th><strong>VDI</strong></th>
    <th><strong>Version</strong></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="7">Horizon View</td>
    <td>6.2.3</td>
  </tr>
  <tr>
    <td>7.1</td>
  </tr>
  <tr>
    <td>7.3.1</td>
  </tr>
  <tr>
    <td>7.3.2</td>
  </tr>
  <tr>
    <td>7.8</td>
  </tr>
  <tr>
    <td>7.9</td>
  </tr>
  <tr>
    <td>7.10</td>
  </tr>
  <tr>
    <td rowspan="4">XenDesktop</td>
    <td>7.8</td>
  </tr>
  <tr>
    <td>7.17</td>
  </tr>
  <tr>
    <td>7.18</td>
  </tr>
  <tr>
    <td>7.19</td>
  </tr>
</tbody>
</table>
