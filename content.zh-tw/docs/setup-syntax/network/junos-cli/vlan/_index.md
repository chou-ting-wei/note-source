---
title: VLAN Configuration
type: docs
---

# VLAN Configuration

## VLAN Setup

### Create VLAN

```txt
[edit]
user@hostname# set vlans vlan<vlan_num> vlan-id <vlan_num>
```

### Trunk Port Configuration

```txt
[edit]
user@hostname# set interfaces <interface> unit 0 family ethernet-switching interface-mode trunk
user@hostname# set interfaces <interface> unit 0 family ethernet-switching vlan members <vlan_list>
```

> `<vlan_list>` should be in the format of `[<vlan_num> <vlan_num> <vlan_num>]`.

### Access Port Configuration

```txt
[edit]
user@hostname# set interfaces <interface> unit 0 family ethernet-switching interface-mode access
user@hostname# set interfaces <interface> unit 0 family ethernet-switching vlan members <vlan_num>
```

## L3 Switch Configuration

### Configure VLAN Interface

```txt
[edit]
user@hostname# set interfaces vlan.<vlan_num> family inet address <ip_address>/<subnet_mask>
```

### Set the Default Gateway

```txt
[edit]
user@hostname# set routing-options static route 0.0.0.0/0 next-hop <ip_address>
```
