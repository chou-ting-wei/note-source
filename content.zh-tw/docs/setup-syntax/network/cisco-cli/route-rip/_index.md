---
title: 4. Static Route/RIP
type: docs
---

# Static Route

## Administrative Distance

| Route Source        | Administrative Distance |
| :------------------ | :---------------------- |
| Connected           | 0                       |
| Static              | 1                       |
| EIGRP Summary Route | 5                       |
| External BGP        | 20                      |
| Internal EIGRP      | 90                      |
| IGRP                | 100                     |
| OSPF                | 110                     |
| RIP                 | 120                     |
| External EIGRP      | 170                     |
| Internal BGP        | 200                     |

## Configure a Static Route

```txt
Router(config)# ip route <network_address> <subnet_mask> {ip-address | exit-intf}
```

## Viewing the IP Routing Table

```txt
Router# show ip route
Codes: L - local, C - connected, S - static, R - RIP , M - mobile, B - BGP
D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
* - candidate default, U - per-user static route, o - ODR
P - periodic downloaded static route
```

## Configure a Default Static Route

```txt
Router(config)# ip route 0.0.0.0 0.0.0.0 {ip-address | exit-intf}
```

## Enable RIP

```txt
Router(config)# router rip
Router(config-router)#
```

## Start RIP routing

```txt
Router(config-router)# network <subnet>
```

## Propagate a Default Route

```txt
Router(config)# ip route 0.0.0.0 0.0.0.0 {ip-address | exit-intf}
Router(config)# router rip
Router(config-router)# default-information originate
```

## Enable RIPv2

```txt
Router(config)# router rip
Router(config-router)# version 2
```

## Disable Auto Summarization

```txt
Router(config)# router rip
Router(config-router)# no auto-summary
```

## Configure Passive Interface

1. Passive all and no specific

```txt
Router(config)# router rip
Router(config-router)# passive-interface default
Router(config-router)# no passive-interface <interface_type> <interface_number>
```

2. Passive specific

```txt
Router(config-router)# passive-interface <interface_type> <interface_number>
```
