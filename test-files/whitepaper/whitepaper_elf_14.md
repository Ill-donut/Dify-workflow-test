---
title: Virtual Machine High Availability
sidebar_label: Virtual Machine High Availability
hide_title: true
id: whitepaper_elf_14
---

# Virtual Machine High Availability

Virtual machine high availability is an advanced VM feature designed to ensure that VMs remain recoverable and available even in extreme environments.

The following diagram shows the components and implementation principles of the entire virtual machine high availability solution. The core decision logic is to use the Job Center and VM Monitor components to check the iSCSI storage heartbeat and MongoDB heartbeat separately, and use that as the basis for VM high availability.

![](../assets/elf-white-paper/image2.png)

**Guarantees**

- A VM with HA protection enabled will be rebuilt to a healthy node in the cluster and restarted under certain conditions.

- If HA recovery is triggered for a VM, two identical VMs must not exist in the same cluster at the same time due to network jitter or any other reason, so as to avoid data corruption.

- The HA mechanism does not depend on the physical clock.

**Trigger Criteria**

- When the cluster is healthy, HA is triggered if one host experiences a power outage, the storage network cable is unplugged, `ifdown` is run on the storage network, the file system becomes read-only, or the host is shut down.
- Unplugging a non-storage network cable, such as the management network cable, does not trigger HA.
- When the running state of a VM with HA protection enabled is inconsistent with the state recorded in the database, HA is triggered to restore the VM to the state recorded in the database, for example when the `qemu` process is killed. An active shutdown initiated inside the Guest OS does not trigger HA.
- If Boost mode is enabled for the cluster, storage service failures trigger HA.
- If, in the cluster's high-availability failure scenarios, you set whether VM network failure scenarios trigger HA to Yes, HA is triggered when a VM network failure occurs.
- If, in the cluster's high-availability failure scenarios, you set whether VM operating system failure scenarios trigger HA to Yes, HA is triggered when the VM operating system bluescreens, the kernel crashes, or the operating system fails to start after HA is triggered.

**Behavior**

- VMs with HA protection enabled will automatically trigger rebuild, recovery, hot migration, or restart in the cluster to ensure high availability.

- If a node is isolated due to a network failure or special circumstances, all VMs on that node will first be paused, and if pausing fails, the VMs will be forcibly shut down.

- If a node is isolated due to a storage network failure, all VMs on the node will first be paused, and HA scheduling will be triggered to power them on on other nodes. Some VMs may fail to be scheduled onto other nodes due to insufficient remaining cluster resources and will remain paused. After the storage network returns to normal, VMs with HA enabled on that node that are in the paused state will automatically recover to the state before HA was triggered, without being restarted.

- If the storage network of the entire cluster becomes unavailable due to a storage switch failure or other reasons, causing all nodes to be isolated, all VMs on the nodes will be paused, and because there are no normally running nodes in the cluster, VMs will not be scheduled to other nodes either. After the storage network returns to normal, VMs with HA enabled on each node that are in the paused state will automatically recover to the state before HA was triggered, without being restarted.

- If a node is isolated due to a storage network failure, all VMs on the node are paused, and VMs on the node successfully recover and power on on other nodes after HA is triggered, then when the faulty node returns to normal, the cluster will automatically clean up the locally paused VMs on that node.

- After a VM with HA protection enabled fails to recover its state 13 times, it will be marked according to its current actual state and recovery operations will stop. The interval between the first 5 recovery attempts is 10s, after the 5th attempt it is 60s, and after the 10th attempt it is 100s. The maximum duration of VM recovery state is 650s.

- In an ELF active-active cluster, if VM placement group rules are not specifically configured, HA scheduling will follow a preferred-availability-zone-first mode. That is, when node resources in the preferred availability zone are sufficient for VM startup, the node in the preferred availability zone will always be selected as the HA destination when HA is triggered.
- If HA is triggered due to a VM network failure, the corresponding behavior will be triggered according to the selected HA action. Two actions are supported: **live migrate VM** and **rebuild VM**. When **live migrate VM** is selected, if there is no schedulable host in the cluster, the VM will remain running on its current host, and the corresponding virtual NIC will display a network failure prompt.
- If the VM operating system fails to start after HA is triggered, the VM will be restarted on its current host.

**Performance**

When a VM with high availability enabled in the cluster fails, high availability will be triggered within a certain time. The specific times are shown in the following table.

<table>
<thead>
  <tr>
    <th colspan="2" rowspan="2"><strong>Failure Scenario</strong></th>
    <th colspan="3"><strong>Failure Detection Sensitivity</strong></th>
  </tr>
  <tr>
    <th><strong>Standard (default)</strong></th>
    <th><strong>Higher</strong></th>
    <th><strong>High</strong></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Host exception</td>
    <td>Power outage, storage network exception</td>
    <td>130 s</td>
    <td>100 s</td>
    <td>60 s</td>
  </tr>
  <tr>
    <td>File system read-only</td>
    <td>85 s</td>
    <td>85 s</td>
    <td>85 s</td>
  </tr>
  <tr>
    <td colspan="2">VM state exception</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td colspan="2">VM network failure</td>
    <td>65 s</td>
    <td>45 s</td>
    <td>35 s</td>
  </tr>
  <tr>
    <td colspan="2">VM operating system failure</td>
    <td>120 s</td>
    <td>60 s</td>
    <td>30 s</td>
  </tr>
</tbody>
</table>

> **Note**:
>
> When the system detects that the VM state does not match the expected state, it immediately restores the VM state, so the HA trigger time is not considered.

<!-- order:12 -->
