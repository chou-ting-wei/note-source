---
title: LACP Configuration
type: docs
---

# LACP Configuration

## Create Aggregated Ethernet Interface

```txt
[edit]
user@hostname# set chassis aggregated-devices ethernet device-count 10
user@hostname# set interfaces ae0 aggregated-ether-options lacp active
```

## Assign Physical Interfaces

```txt
[edit]
user@hostname# set interfaces <interface> ether-options 802.3ad ae0
user@hostname# delete interfaces <interface> unit 0
user@hostname# delete protocols rstp interface <interface>
```

## Configure the Aggregated Ethernet Interface

```txt
[edit]
user@hostname# set interfaces ae0 unit 0 family ethernet-switching interface-mode trunk
user@hostname# set interfaces ae0 unit 0 family ethernet-switching vlan members <vlan_list>
```

## Verify EtherChannel Configuration

```txt
user@hostname> show interfaces terse
```

```
Interface               Admin Link Proto    Local                 Remote
[...]
ge-0/1/0                up    up
ge-0/1/0.0              up    up   aenet    --> ae0.0
ge-0/1/1                up    up
ge-0/1/1.0              up    up   aenet    --> ae0.0
[...]
```

```txt
user@hostname> show interfaces ae0
```

```
Physical interface: ae0, Enabled, Physical link is Down
  Interface index: 674, SNMP ifIndex: 566
  Link-level type: Ethernet, MTU: 1514, Speed: Unspecified, BPDU Error: None,
  Ethernet-Switching Error: None, MAC-REWRITE Error: None, Loopback: Disabled,
  Source filtering: Disabled, Flow control: Disabled, Minimum links needed: 1,
  [...]
```
