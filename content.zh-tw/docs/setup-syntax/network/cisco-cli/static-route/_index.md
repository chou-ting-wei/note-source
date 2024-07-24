---
title: Static Route
type: docs
---

# Static Route

## Administrative Distance

Trustworthiness of the route source: lower values indicate more preferred route sources.

|    Route Source     | Administrative Distance |
| :-----------------: | :---------------------: |
|      Connected      |            0            |
|       Static        |            1            |
| EIGRP Summary Route |            5            |
|    External BGP     |           20            |
|   Internal EIGRP    |           90            |
|        IGRP         |           100           |
|        OSPF         |           110           |
|         RIP         |           120           |
|   External EIGRP    |           170           |
|    Internal BGP     |           200           |

## Configure a Static Route

```txt
Router(config)# ip route <ip_address> <subnet_mask> {ip-address | exit-intf}
```

## Viewing the IP Routing Table

```txt
Router# show ip route
```

## Configure Default Static Route

```txt
Router(config)# ip route 0.0.0.0 0.0.0.0 {ip-address | exit-intf}
```
