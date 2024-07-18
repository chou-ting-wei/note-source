---
title: 2. VLAN Configuration
type: docs
---

# VLAN Configuration

## Create VLAN

```txt
switch# configure terminal
switch(config)# vlan vlan-num
switch(config-vlan)# name vlan-name (optional)
```

## Assign Port to VLAN

```txt
switch(config)# interface type interface_number
switch(config-if)# switchport mode access
switch(config-if)# switchport access vlan vlan-num
```

## Available VLAN Ranges in Cisco IOS

| VLANs     | Range    | Usage                                                                                                                  |
| :-------- | :------- | :--------------------------------------------------------------------------------------------------------------------- |
| 0, 4095   | Reserved | For system use only. You cannot see or use these VLANs.                                                                |
| 1         | Normal   | Cisco default. You can use this VLAN but you cannot delete it. Cisco will use this VLAN to send Control Plane Traffic. |
| 2-1001    | Normal   | For Ethernet VLANs. You can create, use, and delete these VLANs.                                                       |
| 1002-1005 | Normal   | You cannot delete VLANs 1002-1005.                                                                                     |
| 1006-4094 | Extended | For Ethernet VLANs only.                                                                                               |

## Configure Trunk Link

```txt
switch(config)# interface type interface_number
switch(config-if)# switchport trunk encapsulation {isl|dot1q|negotiate}
switch(config-if)# switchport mode trunk
switch(config-if)# switchport trunk allowed vlan {vlan-list|except vlan-list|all}
```

## Modify Existing Trunk Link

```txt
switch(config-if)# switchport trunk allowed vlan {add|remove} vlan-list
```

## Create VLAN on Router/L3 Switch

```txt
switch(config)# vlan vlan-num
switch(config-if)# name vlan-name (optional)
```

## Configure VLAN Interface

```txt
switch(config)# interface vlan vlan-num
switch(config-if)# ip address ip-address subnet-mask
```

## Enable Routing on L3 Switch

```txt
switch(config)# ip routing
```

## Configure Native VLAN

```txt
switch(config)# interface type interface_number
switch(config-if)# switchport trunk encapsulation dot1q
switch(config-if)# switchport trunk native vlan vlan-num
```

## Verify VLAN Configuration
```txt
switch# show vlan brief
switch# show vlan id vlan-num
switch# show interface vlan vlan-num
```