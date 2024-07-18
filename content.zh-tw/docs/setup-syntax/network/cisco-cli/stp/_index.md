---
title: 3. STP Configuration
type: docs
---

# STP Configuration

## Spanning Tree Protocol Variants

| Protocol    | Standard | Resources Needed | Convergence | Tree Calculation |
| :---------- | :------- | :--------------- | :---------- | :--------------- |
| STP         | 802.1D   | Low              | Slow        | All VLANs        |
| PVST+       | Cisco    | High             | Slow        | Per VLAN         |
| RSTP        | 802.1w   | Medium           | Fast        | All VLANs        |
| Rapid PVST+ | Cisco    | Very high        | Fast        | Per VLAN         |
| MSTP        | 802.1s   | Medium or high   | Fast        | Per Instance     |

## Spanning Tree Mode Selection

```txt
switch(config)# spanning-tree mode {stp | pvst | rapid-pvst | mst}
```

## Bridge Priority Setup

```txt
switch(config)# spanning-tree vlan <vlan_id> root {primary | secondary}
% or
switch(config)# spanning-tree vlan <vlan_id> priority <value>
```

## STP Cost Settings

```txt
switch(config)# interface <interface_type> <interface_number>
switch(config-if)# spanning-tree vlan <vlan_id> cost <value>
```

## STP Port States Overview

| Status     | Receive BPDU | Send BPDU | Learn MAC | Forwarding | Duration                                   |
| :--------- | :----------- | :-------- | :-------- | :--------- | :----------------------------------------- |
| Disabled   | X            | X         | X         | X          | Until no shutdown                          |
| Blocking   | O            | X         | X         | X          | Until topology changed                     |
| Listening  | O            | O         | X         | X          | Forward Delay (default 15s)                |
| Learning   | O            | O         | O         | X          | Forward Delay (default 15s)                |
| Forwarding | O            | O         | O         | O          | Until shutdown or not root/designated port |

## STP Timer Settings

```txt
switch(config)# spanning-tree vlan <vlan_id> root primary diameter <size>
```

## PortFast Configuration

> &#x26a0;&#xfe0f;**Warning:** PortFast should only be enabled on ports connected to a single host. Connecting hubs, concentrators, switches, bridges, etc., to this interface when PortFast is enabled can cause temporary bridging loops.

1. Configure PortFast on a switch port

   ```txt
   switch(config)# interface <interface>
   switch(config-if)# spanning-tree portfast
   ```

2. Enable PortFast on all non-trunking interfaces

   ```txt
   switch(config)# spanning-tree portfast default
   ```

## BPDU Guard Configuration

```txt
switch(config)# interface <interface>
switch(config-if)# spanning-tree bpduguard enable
```

## Root Guard Configuration

```txt
switch(config)# interface <interface>
switch(config-if)# spanning-tree guard root
```

## STP Configuration Verification
```txt
switch# show spanning-tree
switch# show spanning-tree vlan <vlan_id>
switch# show spanning-tree detail
```