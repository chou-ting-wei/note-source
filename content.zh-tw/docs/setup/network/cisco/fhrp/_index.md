---
title: FHRP Configuration
type: docs
---

# FHRP Configuration

## Enable HSRP Version 2

```txt
Router(config)# int <interface>
Router(config-if)# standby version 2
```

## Set the HSRP Virtual IP Address

```txt
Router(config-if)# standby <group_num> ip <ip_address>
```

## Configure HSRP Priority

```txt
Router(config-if)# standby <group_num> priority <priority_value>
```

## Configure HSRP Preemption

```txt
Router(config-if)# standby <group_num> preempt
```
