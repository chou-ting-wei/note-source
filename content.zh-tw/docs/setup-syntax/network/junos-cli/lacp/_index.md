---
title: LACP Configuration
type: docs
---

# LACP Configuration

## Create Aggregated Ethernet Interface

```txt
[edit]
user@hostname# set interfaces ae0 aggregated-ether-options lacp active
```

## Assign Physical Interfaces

```txt
[edit]
user@hostname# set interfaces <interface> ether-options 802.3ad ae0
```

## Configure the Aggregated Ethernet Interface

```txt
[edit]
user@hostname# set interfaces ae0 unit 0 family ethernet-switching port-mode trunk
user@hostname# set interfaces ae0 unit 0 family ethernet-switching vlan members <vlan_list>
```
