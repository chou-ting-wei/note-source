---
title: LACP Configuration
type: docs
---

# LACP Configuration

## EtherChannel Modes Relation

| Channel Mode  |    on    |  Active  | Passive  | Desirable |   Auto   |
| :-----------: | :------: | :------: | :------: | :-------: | :------: |
|    **on**     |  Static  | &#x26A0; | &#x26A0; | &#x26A0;  | &#x26A0; |
|  **Active**   | &#x26A0; |   LACP   |   LACP   | &#x2718;  | &#x2718; |
|  **Passive**  | &#x26A0; |   LACP   | &#x2718; | &#x2718;  | &#x2718; |
| **Desirable** | &#x26A0; | &#x2718; | &#x2718; |   PAgP    |   PAgP   |
|   **Auto**    | &#x26A0; | &#x2718; | &#x2718; |   PAgP    | &#x2718; |

> &#x2718;: EtherChannel would not be set up.  
> &#x26A0;: Dangerous (EtherChannel will be set up on ONLY ONE side).

## Setting LACP System Priority

```txt
Switch(config)# lacp system-priority <priority_value>
```

## Setting LACP Port Priority

```txt
Switch(config)# int <interface>
Switch(config-if)# lacp port-priority <priority_value>
```

## Setting Load Balance Method

```txt
Switch(config)# port-channel load-balance <method>
```

```
method:
   src-port       Source port number
   dst-port       Destination port number
   src-dst-port*  Source and destination port number
   src-ip         Source IP address
   dst-ip         Destination IP address
   src-dst-ip*    Source and destination IP address
   src-mac        Source MAC address
   dst-mac        Destination MAC address
   src-dst-mac*   Source and destination MAC address
* XOR of two values
```

## Assign an Interface

```txt
Switch(config)# int <interface>
Switch(config-if)# channel-group <channel_num> mode <channel_mode>
Switch(config-if)# channel-protocol {lacp | pagp}
```

```
channel_mode:
  desirable  Enable PAgP unconditionally
  auto       Enable PAgP only if a PAgP device is detected
  active     Enable LACP unconditionally
  passive    Enable LACP only if an LACP device is detected
  on         Enable Etherchannel only
```

## Config Guidelines

Individual interface config does not affect the port-channel interface.

- Change EtherChannel setting after creation
  ```txt
  Switch(config)# interface port-channel 5
  Switch(config-if)# switchport mode trunk
  Switch(config-if)# switchport trunk allowed vlan 28,420
  ```
- Avoiding misconfiguration with EtherChannel
  ```txt
  Switch(config)# spanning-tree etherchannel guard misconfig (Enabled by default)
  ```

## Verify EtherChannel Configuration

```txt
Switch# show interfaces port-channel <identifier>
Switch# show etherchannel summary
Switch# show etherchannel port-channel
Switch# show interfaces <interface> etherchannel
```
