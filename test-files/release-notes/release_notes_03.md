---
title: Compatibility
author: SmartX documentation team
hide_title: true
id: release_notes_03
sidebar_label: Compatibility
---

# Compatibility

## Compatibility between virtualization platform and server architecture

<table>
  <thead>
    <tr>
        <th><strong>Virtualization platform</strong></th>
        <th><strong>Server CPU architecture</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td rowspan="5">ELF</td>
        <td>Intel x86_64</td>
    </tr>
    <tr>
        <td>AMD x86_64</td>
    </tr>
    <tr>
        <td>Hygon x86_64</td>
    </tr>
    <tr>
       <td>Kunpeng AArch64</td>
    </tr>
    <tr>
       <td>Phytium AArch64</td>
    </tr>
    <tr>
        <td rowspan="2">VMware ESXi</td>
        <td>Intel x86_64</td>
    </tr>
    <tr>
        <td>AMD x86_64</td>
    </tr>
  </tbody>
</table>

## Compatibility between SMTX OS and CloudTower

The SMTX OS functions and services are managed by CloudTower. SMTX OS 6.2.0 is compatible with CloudTower 4.5.0 or later.

## Compatibility between SMTX OS and other SmartX products

SMTX OS is compatible with other SmartX products, but only certain versions of each product are compatible with SMTX OS 6.2.0.You can refer to the specific product release notes for the compatibility between that product and SMTX OS.

- Everoute
- SMTX Kubernetes Service
- SMTX File Storage
- SMTX Backup and Disaster Recovery
- Observability
- Inspector
- Upgrade Center

## Compatibility between virtualization platforms and VDI scenarios

### Virtualization platforms

<table>
<thead>
  <tr>
    <th><strong>Virtualization platform</strong></th>
    <th><strong>Version</strong></th>
    <th><strong>Deployment</strong></th>
    <th><strong>Storage protocol</strong></th>
    <th><strong>Notes</strong></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>ELF</td>
    <td>-</td>
    <td>Deployed on host</td>
    <td>iSCSI</td>
    <td>
       <p>Refer to *SMTX OS Virtual Machine Service Compatibility Guide* for supported guest operating systems. </p>
       <p>SMTX VMTools <code>3.2.2</code> is required for the deployment. </p></td>
  </tr>
  <tr>
    <td rowspan="2">VMware ESXi</td>
    <td><ul>
      <li><p>ESXi 7.0b</p></li>
      <li><p>ESXi 7.0 U1</p></li>
    </ul></td>
    <td>Deployed on SCVM</td>
    <td>NFS</td>
    <td>No VAAI-NAS plugin is required. </td>
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
    <td>Deployed on SCVM</td>
    <td>NFS</td>
    <td>VAAI-NAS plugin <code>2.1-4</code> is required for the deployment. </td>
  </tr>
</tbody>
</table>

### VDI scenarios

In VDI scenarios, SMTX OS can be used with Horizon View and XenDesktop, with supported versions listed below. In this case, SMTX OS can only run on the SCVM on ESXi 7.0b hosts, and VAAI is not supported when creating desktop pools.

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

