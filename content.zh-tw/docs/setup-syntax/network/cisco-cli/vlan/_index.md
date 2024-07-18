---
title: 2. VLAN Configuration
type: docs
---

# VLAN Configuration

## Create VLAN

```txt
Switch# configure terminal
Switch(config)# vlan <vlan_num>
Switch(config-vlan)# name <vlan_name> (optional)
```

## Assign Port to VLAN

The interface is in a specific vlan, switch would forwards network traffic from those the same vlan to this interface.

```txt
Switch(config)# interface <interface>
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan <vlan_num>
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

The interface would allowes some vlans, and switch would forwards network traffic from those allowed vlans.

```txt
Switch(config)# interface <interface>
Switch(config-if)# switchport trunk encapsulation {isl | dot1q | negotiate}
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan {<vlan_list> | except <vlan_list> | all}
```

## Modify Existing Trunk Link

```txt
Switch(config-if)# switchport trunk allowed vlan {add | remove} <vlan_list>
```

## Create VLAN on Router/L3 Switch

```txt
Switch# configure terminal
Switch(config)# vlan <vlan_num>
Switch(config-vlan)# name <vlan_name> (optional)
```

## Configure VLAN Interface

```txt
Switch(config)# interface vlan <vlan_num>
Switch(config-if)# ip address <ip_address> <subnet_mask>
```

## Enable Routing on L3 Switch

```txt
Switch(config)# ip routing
```

## Configure Native VLAN

When a trunk interface transmit packet with its native VLAN, it will send the packet untagged.

```txt
Switch(config)# interface <interface>
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport trunk native vlan <vlan_num>
```

## Verify VLAN Configuration

```txt
Switch# show vlan brief
Switch# show vlan id <vlan_num>
Switch# show interface vlan <vlan_num>
```
