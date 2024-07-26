---
title: STP Configuration
type: docs
---

# STP Configuration

## Spanning Tree Protocol Variants

|  Protocol   | Standard | Resources Needed | Convergence | Tree Calculation |
| :---------: | :------: | :--------------: | :---------: | :--------------: |
|     STP     |  802.1D  |       Low        |    Slow     |    All VLANs     |
|    PVST+    |  Cisco   |       High       |    Slow     |     Per VLAN     |
|    RSTP     |  802.1w  |      Medium      |    Fast     |    All VLANs     |
| Rapid PVST+ |  Cisco   |    Very high     |    Fast     |     Per VLAN     |
|    MSTP     |  802.1s  |  Medium or high  |    Fast     |   Per Instance   |

## Spanning Tree Mode Selection

Cisco IOS use PVST+ as default mode.

```txt
Switch(config)# spanning-tree mode {stp | pvst | rapid-pvst | mst}
```

## Bridge Priority Setup

Bridge priority only allows to be in multiple of 4096.

```txt
Switch(config)# spanning-tree vlan <vlan_id> root {primary | secondary}
% or
Switch(config)# spanning-tree vlan <vlan_id> priority <value>
```

## STP Cost Settings

```txt
Switch(config)# interface <interface>
Switch(config-if)# spanning-tree vlan <vlan_id> cost <value>
```

## STP Port States Overview

|   Status   | Receive BPDU | Send BPDU | Learn MAC | Forwarding | Duration                                   |
| :--------: | :----------: | :-------: | :-------: | :--------: | :----------------------------------------- |
|  Disabled  |   &#x2718;   | &#x2718;  | &#x2718;  |  &#x2718;  | Until no shutdown                          |
|  Blocking  |   &#x2714;   | &#x2718;  | &#x2718;  |  &#x2718;  | Until topology changed                     |
| Listening  |   &#x2714;   | &#x2714;  | &#x2718;  |  &#x2718;  | Forward Delay (default 15s)                |
|  Learning  |   &#x2714;   | &#x2714;  | &#x2714;  |  &#x2718;  | Forward Delay (default 15s)                |
| Forwarding |   &#x2714;   | &#x2714;  | &#x2714;  |  &#x2714;  | Until shutdown or not root/designated port |

## STP Enhancements

### PortFast Configuration

> &#x26a0;&#xfe0f;**Warning:** PortFast should only be enabled on ports connected to a single host. Connecting hubs, concentrators, switches, bridges, etc., to this interface when PortFast is enabled can cause temporary bridging loops.

Allow a port to enter from blocking to forwarding state immediately, bypassing the listening and learning states.

1. Configure PortFast on a switch port

   ```txt
   Switch(config)# interface <interface>
   Switch(config-if)# spanning-tree portfast
   ```

2. Enable PortFast on all non-trunking interfaces

   ```txt
   Switch(config)# spanning-tree portfast default
   ```

### BPDU Guard Configuration

If BPDU guard is enabled, it puts the port in an `err-disabled` state when receiving a BPDU.

```txt
Switch(config)# interface <interface>
Switch(config-if)# spanning-tree bpduguard enable
```

### Root Guard Configuration

If there is a superior BPDU received on the port, root guard does not take the BPDU into account and so puts the port into `root inconsistent` state.

```txt
Switch(config)# interface <interface>
Switch(config-if)# spanning-tree guard root
```

### Verify STP Configuration

```txt
Switch# show spanning-tree
Switch# show spanning-tree vlan <vlan_id>
Switch# show spanning-tree detail
```
