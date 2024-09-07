---
title: VLAN Configuration
type: docs
---

# VLAN Configuration

## VLAN Setup

### Create VLAN

```txt
[edit]
user@hostname# set vlans <vlan_name> vlan-id <vlan_num>
```

### Trunk Port Configuration

```txt
[edit]
user@hostname# set interfaces <interface> unit 0 family ethernet-switching interface-mode trunk
user@hostname# set interfaces <interface> unit 0 family ethernet-switching vlan members <vlan_list>
```

> `<vlan_list>` should be in the format of `[<vlan_name> <vlan_name> <vlan_name>]`.

### Access Port Configuration

```txt
[edit]
user@hostname# set interfaces <interface> unit 0 family ethernet-switching interface-mode access
user@hostname# set interfaces <interface> unit 0 family ethernet-switching vlan members <vlan_name>
```

## L3 Switch Configuration

### Create VLAN on L3 Switch

```txt
[edit]
user@hostname# set vlans <vlan_name> vlan-id <vlan_num>
```

### Configure IRB

Integrated routing and bridging (IRB) provides simultaneous support for Layer 2 bridging and Layer 3 routing on the same interface.

```txt
user@hostname# set interfaces irb unit <vlan_num> family inet address <ip_address>/<subnet_mask>
user@hostname# set vlans <vlan_name> l3-interface irb.<vlan_num>
```

### Set the Default Gateway

```txt
[edit]
user@hostname# set routing-options static route 0.0.0.0/0 next-hop <ip_address>
```
